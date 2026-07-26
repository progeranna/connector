# SignalGuard RS P2-MP06-WEB1-C1 — Recovery and Atomic Delivery

## Purpose

Continue the existing P2-MP06-WEB1 execution in the same ChatGPT web-worker sandbox after a delivery-only failure.

The implementation is not to be repeated. The remote product branch remains unchanged at the exact assigned base.

This contract supersedes only the failed final gate-evidence and GitHub tree-delivery steps of `P2-MP06-WEB1.md`. All original implementation scope and semantics remain binding.

## Exact product state

- Repository: `progeranna/signalguard-rs`
- Branch: `p2/mp06-bulk-redis-state`
- Exact required remote head and sole commit parent: `1447a3ccb2fa3020738cd2dd3f8d145be6cd202a`
- Required commit message: `perf(api): load dashboard market states in bulk`
- PR base: `refactor/data-boundaries`

The Orchestrator independently re-verified that the remote branch is identical to the base: ahead `0`, behind `0`.

## Same-sandbox requirement

Continue only in the same web-worker sandbox that contains:

- final workspace: `/mnt/data/signalguard-p2-mp06-web1-env/workspace`
- exact base copy: `/mnt/data/signalguard-p2-mp06-web1-base`
- environment file: `/mnt/data/signalguard-p2-mp06-web1-env/env.sh`
- bootstrap artifact: `/mnt/data/signalguard-P2-MP06-WEB6-bootstrap.zip`

If any required final or base file is missing, stop without product write. Do not reconstruct the implementation from chat, the rejected blobs, another worker, or local Codex.

## Required unchanged final-file identities before gates

Require these SHA-256 values:

- `src/storage/redis.rs`: `e1cbf55afebedc5303fb22f658738b2a5ca150b7ab62241f1931c1b0a4f0c3b9`
- `src/api/handlers.rs`: `7a4ce8dfd3e4c9209398327ba923a3dab75b6e324ba4a6dc897316b04d509d73`
- `tests/redis_cache.rs`: `643c4a2b932407ed6ecc262f246b1809877ea358b26c6ffd78fedbad3365e0ef`

Require these Git blob SHA values using `git hash-object --no-filters <path>` outside any repository:

- `src/storage/redis.rs`: `ffa0d0214bc7e56fe41ae8460121746808b1c774`
- `src/api/handlers.rs`: `b1b65ab38004642b9500abfb4eb45cc4fe6508e9`
- `tests/redis_cache.rs`: `289adc8de9d1b3fe3bb1b06be997312f9097ed50`

Do not reuse any previously created GitHub blob object unless its returned SHA exactly equals the corresponding local `git hash-object` result.

## Repeat the complete formal gate cycle

Source:

`/mnt/data/signalguard-p2-mp06-web1-env/env.sh`

Create a fresh evidence directory:

`/mnt/data/p2-mp06-web1-recovery-gates`

Run every gate separately. Use `set -o pipefail`, pipe each command through `tee` into its own log file, and check the real command exit status. A truncated combined log is not acceptable.

### Formatting and compile gates

From the final workspace:

1. `cargo fmt --all`
2. `cargo fmt --all --check`
3. `cargo check --locked --offline --all-targets --all-features`
4. `cargo clippy --locked --offline --all-targets --all-features -- -D warnings`
5. `cargo test --locked --offline --all-targets --all-features`

After `cargo fmt --all`, require the three final SHA-256 and Git blob SHA values to remain exactly those listed above. If formatting changes any file, stop without product write and report the new hashes.

### Focused gates

Run and preserve separate logs for the focused bulk-cache and dashboard-handler tests required by P2-MP06-WEB1, including:

- empty input;
- BTCUSDT and ETHUSDT in both orders;
- missing first, middle, and last values;
- malformed JSON;
- embedded-symbol mismatch;
- in-memory bulk behavior;
- dashboard state and health mapping;
- absent dashboard state.

Do not claim focused coverage unless the exact test names and pass counts are present in the logs.

### Real Redis gates

Start the bundled Redis server on a fresh random loopback high port with persistence disabled and a fresh temporary data directory. Export the exact `REDIS_URL` used by the tests.

Run and preserve separate logs for:

- `cargo test --locked --offline --test redis_cache -- --ignored --test-threads=1`
- the dedicated ignored P2-MP06 bulk-read Redis test/filter, when separately available;
- `cargo test --locked --offline --lib atomic_market_state_write -- --ignored --test-threads=1`

Require Redis cleanup after the tests.

### Scope and hygiene evidence

Regenerate and preserve:

- exact changed-path inventory against `/mnt/data/signalguard-p2-mp06-web1-base`;
- whitespace/diff validation;
- forbidden-path inventory;
- secret scan;
- byte-for-byte proof that the P2-MP05 Lua script remains unchanged.

Only these paths may differ:

- `src/storage/redis.rs`
- `src/api/handlers.rs`
- `tests/redis_cache.rs`

Stop without product write if any gate fails, is skipped, has a missing log, or changes the expected final hashes.

## Correct atomic GitHub delivery

### 1. Re-verify remote state

Immediately before any GitHub object creation, require:

- branch `p2/mp06-bulk-redis-state` still equals `1447a3ccb2fa3020738cd2dd3f8d145be6cd202a`;
- ahead `0`, behind `0`.

### 2. Compute the exact base tree locally

Use only the exact base copy, never the modified workspace.

If `/mnt/data/p2-treecalc` exists, remove and recreate it from `/mnt/data/signalguard-p2-mp06-web1-base`.

Initialize a temporary Git repository there, add the exact base files, and compute the root tree SHA.

Avoid persistent global configuration. For every Git command in that repository use a command-local safe-directory option, for example:

`git -c safe.directory=/mnt/data/p2-treecalc -C /mnt/data/p2-treecalc ...`

The base-tree calculation must not modify the final workspace.

### 3. Create and verify blobs

For each of the three final files:

1. recompute local Git blob SHA with `git hash-object --no-filters`;
2. create one GitHub blob through the connector;
3. require the connector-returned blob SHA to equal the local Git blob SHA exactly.

Expected values:

- `ffa0d0214bc7e56fe41ae8460121746808b1c774`
- `b1b65ab38004642b9500abfb4eb45cc4fe6508e9`
- `289adc8de9d1b3fe3bb1b06be997312f9097ed50`

Ignore any prior unreferenced blob objects whose SHA differs.

### 4. Create the tree with the correct connector schema

Call `GitHub.create_tree` using exactly:

- `repository_full_name`: `progeranna/signalguard-rs`
- `base_tree_sha`: the exact root tree SHA computed from the base copy
- `tree_elements`: an array containing exactly three entries

Each tree element must contain:

- `path`: the exact authorized repository path
- `mode`: `100644`
- `type`: `blob`
- `sha`: the verified matching GitHub blob SHA

Do not use fields named `tree` or `base_tree`.

### 5. Create the commit but do not move the branch yet

Create exactly one commit with:

- tree: the new tree SHA;
- sole parent: `1447a3ccb2fa3020738cd2dd3f8d145be6cd202a`;
- message: `perf(api): load dashboard market states in bulk`.

Before updating any ref, fetch and inspect the newly created commit by SHA. Require:

- exact sole parent;
- exact commit message;
- exactly the three authorized changed paths;
- no generated or unexpected path.

A created but unreferenced invalid commit is harmless; stop without branch update if any verification fails.

### 6. Move the branch non-force

Only after commit verification, call `GitHub.update_ref` with:

- branch: `p2/mp06-bulk-redis-state`
- SHA: the verified new commit
- `force: false`

Then require:

- ahead by exactly `1` from the assigned base;
- behind by `0` from the assigned base;
- exactly one commit;
- exactly three changed paths;
- exact commit message.

Do not amend, rebase, reset, merge, or force-update any branch.

## PR, CI, and report

After successful branch publication:

1. Open one draft PR into `refactor/data-boundaries`.
2. Title: `perf(api): load dashboard market states in bulk`.
3. Do not merge.
4. Wait for exact-head product CI.
5. Stop and report if any CI job fails.
6. Only after green exact-head CI, create:

   `signalguard-rs/phase-2/reports/P2-MP06/<PRODUCT-HEAD-SHA>.md`

The report must include:

- recovery contract identity;
- preserved final SHA-256 and Git blob SHA values;
- one log path and exit status per repeated gate;
- Redis URL/port redacted to loopback identity only;
- base tree SHA;
- three matching local/GitHub blob SHA pairs;
- created tree SHA;
- created commit SHA and parent verification;
- non-force ref update evidence;
- PR URL;
- exact-head CI run and conclusion.

Do not modify connector status, control, prompts, repairs, reviews, proofs, integration records, or another report.

## Required final response

Return only:

- same-sandbox path verification;
- preserved SHA-256 and Git blob SHA verification;
- repeated focused/full/Redis gate summary with log paths;
- exact base tree SHA;
- three local/GitHub blob SHA pairs;
- created tree SHA;
- product commit SHA and parent/message/path verification;
- non-force ref update result;
- product branch comparison result;
- draft PR URL;
- exact-head CI run ID and conclusion;
- connector report path and commit SHA;
- any blocker.
