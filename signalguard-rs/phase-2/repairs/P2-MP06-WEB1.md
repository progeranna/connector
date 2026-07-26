# SignalGuard RS P2-MP06-WEB1 — ChatGPT Web Worker Pilot

## Purpose

Execute P2-MP06 through a fresh ChatGPT web worker rather than local Codex, using the verified portable Rust/Redis bootstrap artifact and an atomic Git tree commit.

This contract supersedes only the execution environment and delivery mechanism of P2-MP06-C2. The product scope and semantics from the original P2-MP06, C1, and C2 contracts remain binding.

## Immutable references

- Original P2-MP06 contract: `signalguard-rs/phase-2/prompts/P2-MP06.md`
- Continuation C1: `signalguard-rs/phase-2/repairs/P2-MP06-C1.md`
- Continuation C2: `signalguard-rs/phase-2/repairs/P2-MP06-C2.md`
- Product repository: `progeranna/signalguard-rs`
- Assigned branch: `p2/mp06-bulk-redis-state`
- Exact product base and required initial remote branch head: `1447a3ccb2fa3020738cd2dd3f8d145be6cd202a`
- Current PR base: `refactor/data-boundaries`
- Required product commit message: `perf(api): load dashboard market states in bulk`

## Stop the local executor

The local Codex P2-MP06 task must be stopped before this worker begins.

The web worker must not read, copy, reconstruct, import, or depend on uncommitted files from:

`/Users/anion/Desktop/work/git-signalguard-rs/worktrees/p2-mp06`

Implement independently from the exact source contained in the bootstrap artifact.

## Verified bootstrap artifact

- Connector repository: `progeranna/connector`
- Workflow run ID: `30220162842`
- Artifact ID: `8636970817`
- Artifact name: `signalguard-P2-MP06-WEB6-30220162842`
- Artifact ZIP SHA-256: `ab12f92e7835dd4e5c56878c6a3fad7e1ddac8c97f8e1e9152778140792372ac`
- Inner bootstrap archive SHA-256: `8afe14a493ae1170f7fe595993e9f268c12f0d91187027257c7d056e194e96b8`
- Product source SHA embedded in manifest: `1447a3ccb2fa3020738cd2dd3f8d145be6cd202a`
- Artifact expiry: 2026-07-29T21:01:10Z

The artifact contains:

- stable `rustc`, `cargo`, `rustfmt`, and Clippy;
- exact Cargo dependencies vendored from the assigned `Cargo.lock`;
- exact product source at the assigned base;
- portable Redis server and CLI;
- checksums and a manifest.

Docker is intentionally omitted from this pilot bundle. P2-MP06 does not require a nested Docker daemon. Docker/Compose acceptance remains in product GitHub CI.

## Mandatory no-write preflight

No product GitHub write is allowed before all preflight checks pass.

1. Use the GitHub connector to download artifact ID `8636970817` from `progeranna/connector`.
2. Confirm the downloaded ZIP exists in `/mnt/data`.
3. Require ZIP SHA-256:

   `ab12f92e7835dd4e5c56878c6a3fad7e1ddac8c97f8e1e9152778140792372ac`

4. Unzip it and require the inner `.tar.zst` SHA-256:

   `8afe14a493ae1170f7fe595993e9f268c12f0d91187027257c7d056e194e96b8`

5. Extract the inner archive.
6. Run `bootstrap.sh`, taking only its final stdout line as the generated environment-file path. The checksum lines printed before it are expected.
7. Source the generated environment file.
8. Read `metadata/MANIFEST.json` and require the exact product SHA and branch from this contract.
9. Run:

   - `rustc --version`
   - `cargo --version`
   - `rustfmt --version`
   - `cargo clippy --version`
   - `cargo metadata --locked --offline --no-deps`

10. Create a disposable, correctly formatted Rust crate and require:

   - `cargo fmt --all --check`
   - `cargo check --offline`
   - `cargo clippy --offline --all-targets -- -D warnings`
   - `cargo test --offline`

11. Start the portable Redis server on a random loopback high port with persistence disabled and require:

   - `PING` -> `PONG`;
   - ordered `MGET` with a missing middle value;
   - Lua `SET` plus `SADD`.

12. In the embedded product workspace, require:

   `cargo check --locked --offline --all-targets --all-features`

The embedded `preflight.sh` has a known disposable-crate formatting defect and must not be used as a single opaque command. Execute the equivalent corrected preflight described above. Do not modify tracked product files during preflight.

## Product scope

Only these product paths may change:

- `src/storage/redis.rs`
- `src/api/handlers.rs`
- `tests/redis_cache.rs`

No dependency, lockfile, frontend, CI, workflow, Docker, migration, documentation, or unrelated backend path may change.

## Required implementation

Implement:

`get_market_states(&[Symbol]) -> Result<Vec<(Symbol, Option<MarketState>)>, CacheError>`

Requirements:

- one Redis `MGET` or one actually executed bulk pipeline for all requested state keys;
- not parallel per-symbol `GET` calls;
- explicit symbol-to-result association;
- input-order preservation;
- correct empty input behavior;
- missing first, middle, or last values remain associated with the correct requested symbol;
- malformed JSON returns an error without shifting neighboring results;
- an embedded payload symbol that differs from the requested key returns an error;
- in-memory cache behavior remains correct;
- dashboard state and health mapping remain semantically unchanged;
- Redis key names and the P2-MP05 atomic Lua write remain unchanged.

The previously accepted decimal test intent remains binding:

- scale-0 fixtures representing numeric 100 and 200 must expect serialized strings `"100"` and `"200"`;
- do not change production decimal serialization.

Any Redis test command requiring an explicit result type must use the smallest correct type annotation in `tests/redis_cache.rs`. Do not change production code to satisfy test-only type inference.

## Required gates

Run all commands offline where Cargo supports it.

Focused tests must cover:

- empty input;
- BTCUSDT and ETHUSDT in both orders;
- missing first, middle, and last state;
- malformed JSON;
- embedded-symbol mismatch;
- in-memory cache behavior;
- dashboard state and health mapping;
- real-Redis bulk retrieval.

Full Rust gates:

- `cargo fmt --all`
- `cargo fmt --all --check`
- `cargo check --locked --offline --all-targets --all-features`
- `cargo clippy --locked --offline --all-targets --all-features -- -D warnings`
- `cargo test --locked --offline --all-targets --all-features`
- `git diff --check` equivalent against the embedded base files;
- changed-path and repository-hygiene inventory.

Real Redis gates:

- start portable Redis on a random loopback port;
- set the exact Redis URL expected by the tests;
- `cargo test --locked --offline --test redis_cache -- --ignored --test-threads=1`;
- any separately available focused ignored P2-MP06 bulk-read filter;
- `cargo test --locked --offline --lib atomic_market_state_write -- --ignored --test-threads=1`.

Stop without product write if any required gate fails or is skipped.

## Atomic GitHub delivery

The embedded source intentionally has no `.git` directory. Do not create a normal shell Git history and do not use the GitHub Contents API for product files.

After all gates pass:

1. Re-check that remote branch `p2/mp06-bulk-redis-state` still points exactly to `1447a3ccb2fa3020738cd2dd3f8d145be6cd202a`.
2. Re-check that only the three authorized files differ from the embedded base.
3. Fetch the exact base commit and obtain its tree SHA.
4. Create exactly one Git blob for each final changed file.
5. Create one Git tree based on the exact base tree, replacing only the three authorized paths.
6. Create exactly one product commit with parent:

   `1447a3ccb2fa3020738cd2dd3f8d145be6cd202a`

   and message:

   `perf(api): load dashboard market states in bulk`

7. Move only `p2/mp06-bulk-redis-state` to the new commit using a non-force ref update.
8. Verify:

   - branch ahead by exactly one commit;
   - behind by zero relative to the assigned base;
   - exactly the three authorized paths changed;
   - exact commit message;
   - no unexpected file or generated artifact.

Do not amend, rebase, merge, reset the phase branch, or force-update the product branch.

## PR and CI

- Open one draft PR into `refactor/data-boundaries`.
- Title: `perf(api): load dashboard market states in bulk`
- Do not merge.
- Wait for exact-head product CI.
- Stop and report if any product CI job fails.

## Connector report

Only after green exact-head product CI, create:

`signalguard-rs/phase-2/reports/P2-MP06/<PRODUCT-HEAD-SHA>.md`

The report must include bootstrap artifact identity and checksums, preflight evidence, exact changed paths, local offline gates, real-Redis gates, atomic Git tree delivery evidence, PR URL, and exact-head CI run.

Do not modify connector status, control, prompts, repairs, reviews, proofs, integration records, or another worker report.

## Required final response

Return only:

- web-worker sandbox OS and architecture;
- artifact ID, ZIP SHA-256, inner archive SHA-256, and manifest product SHA;
- preflight summary;
- embedded product workspace path;
- product branch and exact base SHA;
- product commit SHA;
- atomic commit/tree delivery summary;
- exact changed paths;
- bulk API signature and Redis strategy;
- focused/full Rust gate summary;
- real-Redis gate summary;
- draft PR URL;
- exact-head CI run ID and conclusion;
- connector report path and commit SHA;
- any blocker.
