# ChatGPT Sandbox Toolchain Research

Date: 2026-07-26

Purpose: determine whether a ChatGPT-hosted implementation worker can be provisioned with the Rust and Redis tooling required by SignalGuard RS without relying on the worker's public shell network.

## Scope and caveat

The measurements below were made in the current ChatGPT container sandbox. A separately spawned web worker may receive a fresh or slightly different sandbox, so every worker must run a no-write preflight before touching the product repository.

The sandbox is ephemeral. Installing or extracting tools in one sandbox does not make them persistent in later workers.

## Observed sandbox baseline

- Debian GNU/Linux 13 (`trixie`), x86-64.
- Root user with working passwordless `sudo`.
- Approximately 39 GiB free disk and 5.9 GiB RAM during the probe.
- Present: Git, curl, wget, tar, unzip, GCC, Clang, Make, CMake, pkg-config, Node.js, npm, Python and Go.
- Initially absent: `rustup`, `rustc`, `cargo`, `rustfmt`, `clippy-driver`, Docker/Podman, `redis-server`, `redis-cli`, and `gh`.
- Public shell DNS/IP egress was unavailable. The environment advertised `NETWORK=caas_packages_only`.

## Built-in CAAS package-mirror route

The image contains:

`/usr/local/init_scripts/caas_package_mirror.sh`

It is disabled unless:

`CAAS_PACKAGE_MIRROR_BOOTSTRAP=1`

When enabled, it rewrites Debian APT and npm configuration to internal Artifactory endpoints using credentials already supplied through environment variables. It intentionally exits with status `42` after a successful bootstrap, so callers must accept exit codes `0` and `42`.

The bootstrap itself worked during the probe, but the internal Artifactory host returned HTTP `503 Service Temporarily Unavailable` for APT/npm/PyPI/Docker registry requests. Therefore this route is fast when the internal service is healthy, but it is not sufficient as the only provisioning mechanism.

No Artifactory credential value was copied into this document or a repository file.

## GitHub Actions artifact bridge

A reversible experiment proved this path:

1. A temporary workflow ran on a GitHub-hosted Ubuntu runner.
2. The runner packaged tool binaries into a GitHub Actions artifact.
3. The GitHub connector downloaded that artifact.
4. ChatGPT automatically mounted the downloaded file under `/mnt/data`.
5. The current ChatGPT sandbox extracted and executed the tools.

The temporary experiment branch was force-reset to current `connector/main` after the probes. No experimental workflow or result file remains in the branch.

### Hosted-runner tool versions observed

- `rustc 1.97.1`
- `cargo 1.97.1`
- `rustfmt 1.9.0-stable`
- `clippy 0.1.97`
- Redis server and CLI `7.0.15`
- Docker Engine `28.0.4`
- Docker Compose `2.38.2`

### Portable Redis bundle

The artifact contained:

- `redis-server`;
- `redis-cli`;
- the missing `liblzf.so.1` runtime dependency;
- wrappers that set a bundle-local `LD_LIBRARY_PATH`.

The compressed Redis bundle was approximately 1.2 MiB.

Executed successfully in the Debian 13 ChatGPT sandbox:

- `redis-server --version`;
- `redis-cli --version`;
- server startup bound to `127.0.0.1` on a high port with persistence disabled;
- `PING` -> `PONG`;
- `MSET` and ordered `MGET`, including a missing middle element;
- a Lua script containing `SET` and `SADD`.

Portable Redis archive SHA-256 from the final artifact:

`b9a42462f418b539d22cd8d15c68df203f0fd197a9adf870abe1a1b1c77d389f`

### Portable Rust bundle

The complete hosted-runner stable toolchain directory was packaged as `rust-toolchain.tar.zst`.

- Uncompressed toolchain size on the runner: approximately 624 MiB.
- Compressed archive size: approximately 195 MiB.
- Outer GitHub artifact size: `205493323` bytes.
- GitHub artifact digest: `sha256:1b9e32dc6249ae5a72c036d59f5a2a4ae1c5434d5a135c71d160fb7d2d74b126`.
- Rust toolchain archive SHA-256: `c6e8c684764fce5ec517031722148b8db672cd6d9344751691940e8df2d5b65b`.

After extraction in the Debian 13 ChatGPT sandbox, these commands succeeded using only bundle-local `PATH` and `LD_LIBRARY_PATH`:

- `rustc --version`;
- `cargo --version`;
- `rustfmt --version`;
- `cargo clippy --version`;
- `cargo fmt --all --check`;
- `cargo check --all-targets`;
- `cargo clippy --all-targets -- -D warnings`;
- `cargo test`;
- `cargo run --quiet` for a newly created local crate.

The compiled probe printed the expected value `6`.

This proves that `cargo`, `rustfmt`, `clippy` and `rustc` can be provisioned without public shell egress.

## Cargo dependency constraint

A compiler bundle alone is not enough for SignalGuard RS. Cargo still needs every crate selected by `Cargo.lock`.

Two viable approaches:

1. Use the internal Cargo Artifactory mirror when it is healthy, configured through Cargo source replacement and an ephemeral credential provider.
2. On GitHub Actions, check out the exact product SHA and run `cargo vendor`; include the resulting vendor directory and generated Cargo source-replacement config in the toolchain artifact. The worker can then build and test with `--offline`.

The second route avoids dependency on both public shell egress and transient Artifactory availability. A bundle must be generated from the exact reviewed `Cargo.lock` and identified by product SHA plus toolchain version.

Credentials must never be committed, echoed, embedded in artifact names, or included in reports.

## Docker findings

The current ChatGPT sandbox had no Docker socket or daemon and lacked the capabilities normally needed for nested rootful Docker. Cgroup v2 was mounted read-only, and direct mount operations failed.

User namespaces were available, but the image lacked the usual rootless-container prerequisites, including `newuidmap`, `newgidmap`, RootlessKit/slirp4netns, and fuse-overlayfs. `/dev/fuse` was absent.

Therefore:

- installing only the Docker CLI is easy but does not provide a working daemon;
- nested rootful Docker should be treated as unavailable;
- rootless Docker or Podman is theoretically possible after provisioning additional binaries, but remains fragile under the sandbox's cgroup, networking and storage constraints;
- SignalGuard Redis tests should use the directly executed portable `redis-server` bundle;
- Docker Compose configuration checks and container-level acceptance tests should remain in GitHub Actions.

## GitHub delivery constraint and solution

Public shell Git/GitHub access may remain unavailable even after installing compilers. A web worker must not fall back to one-file-at-a-time Contents API commits.

The GitHub connector exposes the primitives required for one atomic multi-file product commit:

1. create one blob per final changed file;
2. create one tree using the assigned base tree;
3. create one commit with the exact assigned parent SHA;
4. move only the assigned branch ref with a non-force update;
5. verify the resulting diff and commit count.

This avoids the fragmented-commit failure previously observed in web workers.

## Recommended provisioning hierarchy

### Tier 1 — internal package mirror

Use the built-in CAAS bootstrap, retry APT, install Rust packages and Redis directly, and verify versions. Fastest path when Artifactory is healthy.

### Tier 2 — verified portable artifact

Download a SHA-pinned artifact containing:

- Rust toolchain;
- portable Redis;
- exact `cargo vendor` dependency tree for the assigned product SHA;
- bootstrap and verification scripts;
- checksums and a manifest.

This is the reliable fallback and was proven for Rust execution and Redis execution.

### Tier 3 — GitHub-hosted gates

Keep Docker/Compose and any remaining environment-dependent acceptance tests in GitHub Actions. Do not make a web-worker delivery depend on nested Docker.

## Required no-write worker preflight

Before product modification, a candidate web worker should prove all of the following:

1. inspect OS, architecture, disk, memory and tool availability;
2. obtain the approved bootstrap artifact;
3. verify artifact and inner-file SHA-256 values;
4. run Rust version checks;
5. compile, format, lint and test a disposable crate;
6. start portable Redis on a random loopback port;
7. pass `PING`, ordered `MGET` and Lua checks;
8. confirm exact product source SHA and offline dependency availability;
9. demonstrate an atomic connector tree commit on a disposable experiment branch;
10. reset the experiment branch and report no product writes.

Only after this preflight succeeds should a web worker receive an implementation contract.

## Conclusion

The absence of Rust and Redis in the default web-worker image is not an absolute blocker.

- Rust, Cargo, rustfmt and Clippy are portable through a GitHub Actions artifact; this was executed and verified in the ChatGPT sandbox.
- Redis is portable as a very small bundle and was executed with the operations required by SignalGuard tests.
- Cargo dependencies must be vendored or supplied by a healthy internal mirror.
- Docker should not be required inside the web worker; keep Docker gates in GitHub Actions.
- Atomic GitHub tree commits must replace Contents API per-file delivery.
- Tool installation remains per-sandbox and must begin with a no-write preflight.
