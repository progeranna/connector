# SignalGuard RS P2-MP06-WEB1-C2 — Base64 Blob Delivery

## Purpose

Continue the same P2-MP06-WEB1 web-worker execution after all implementation, focused, full Rust, real-Redis, and scope gates passed with complete preserved evidence.

This continuation is delivery-only. Do not reimplement code and do not repeat the full gate cycle unless an integrity check below fails.

## Exact product state

- Repository: `progeranna/signalguard-rs`
- Branch: `p2/mp06-bulk-redis-state`
- Exact required remote head and sole parent: `1447a3ccb2fa3020738cd2dd3f8d145be6cd202a`
- Required commit message: `perf(api): load dashboard market states in bulk`
- PR base: `refactor/data-boundaries`

The Orchestrator reverified the remote branch remains identical to the base: ahead `0`, behind `0`, no product commit or PR.

## Same-sandbox requirement

Continue only in the sandbox containing:

- `/mnt/data/signalguard-p2-mp06-web1-env/workspace`
- `/mnt/data/signalguard-p2-mp06-web1-base`
- `/mnt/data/signalguard-p2-mp06-web1-env/env.sh`
- `/mnt/data/p2-mp06-web1-recovery-gates`

Stop without product write if any path is missing.

## Preserved final identities

Require these SHA-256 and Git blob SHA values again immediately before delivery:

| Path | SHA-256 | Git blob SHA |
|---|---|---|
| `src/storage/redis.rs` | `e1cbf55afebedc5303fb22f658738b2a5ca150b7ab62241f1931c1b0a4f0c3b9` | `ffa0d0214bc7e56fe41ae8460121746808b1c774` |
| `src/api/handlers.rs` | `7a4ce8dfd3e4c9209398327ba923a3dab75b6e324ba4a6dc897316b04d509d73` | `b1b65ab38004642b9500abfb4eb45cc4fe6508e9` |
| `tests/redis_cache.rs` | `643c4a2b932407ed6ecc262f246b1809877ea358b26c6ffd78fedbad3365e0ef` | `289adc8de9d1b3fe3bb1b06be997312f9097ed50` |

Require all `.exit` files from the C1 recovery gate directory to contain `0` and all referenced log files to exist and be non-empty.

No code modification is authorized by C2.

## Existing exact GitHub blobs

The Orchestrator independently fetched and verified these exact unreferenced blobs already exist in `progeranna/signalguard-rs`:

- `src/storage/redis.rs`: `ffa0d0214bc7e56fe41ae8460121746808b1c774`
- `tests/redis_cache.rs`: `289adc8de9d1b3fe3bb1b06be997312f9097ed50`

Reuse those exact blob SHAs. Do not recreate them.

The only missing exact blob is:

- `src/api/handlers.rs`: `b1b65ab38004642b9500abfb4eb45cc4fe6508e9`

## Exact base64 transfer for handlers.rs

The GitHub connector supports `GitHub.create_blob` with `encoding: "base64"`. This is an exact machine transfer and is not chat transcription.

1. Generate a single-line base64 payload:

   `base64 -w0 /mnt/data/signalguard-p2-mp06-web1-env/workspace/src/api/handlers.rs > /mnt/data/p2-mp06-handlers.rs.b64`

2. Require:

   - source byte length: `51405`;
   - base64 byte length: `68540`;
   - no newline inside the base64 file.

3. Verify exact round trip before the connector call:

   - decoding the base64 file produces SHA-256 `7a4ce8dfd3e4c9209398327ba923a3dab75b6e324ba4a6dc897316b04d509d73`;
   - decoding and piping to `git hash-object --stdin` produces `b1b65ab38004642b9500abfb4eb45cc4fe6508e9`.

4. Read the entire base64 file as one string and call `GitHub.create_blob` with:

   - `repository_full_name`: `progeranna/signalguard-rs`
   - `encoding`: `base64`
   - `content`: the complete exact 68,540-character payload

5. Do not print or paste the base64 payload in the user-visible response. It belongs only in the tool-call argument.

6. Require the returned GitHub blob SHA to equal exactly:

   `b1b65ab38004642b9500abfb4eb45cc4fe6508e9`

Stop without tree or branch update if the payload is truncated, the tool rejects it, or the returned SHA differs.

## Tree creation

Use:

- base tree SHA: `7e9c73ec85084725aca0212d7d649dddcb7f1803`
- exactly three entries
- fields `tree_elements` and `base_tree_sha`

Tree entries:

1. `src/storage/redis.rs` → `ffa0d0214bc7e56fe41ae8460121746808b1c774`
2. `src/api/handlers.rs` → `b1b65ab38004642b9500abfb4eb45cc4fe6508e9`
3. `tests/redis_cache.rs` → `289adc8de9d1b3fe3bb1b06be997312f9097ed50`

Every entry must use:

- `mode`: `100644`
- `type`: `blob`

Call `GitHub.create_tree` only after all three exact blobs are confirmed.

## Commit and branch publication

1. Create exactly one commit with:

   - tree: the created tree SHA;
   - sole parent: `1447a3ccb2fa3020738cd2dd3f8d145be6cd202a`;
   - message: `perf(api): load dashboard market states in bulk`.

2. Before updating the branch, fetch the created commit and require:

   - exact sole parent;
   - exact message;
   - exactly the three authorized changed paths;
   - no generated or unexpected path.

3. Reverify the remote branch still equals the exact base.

4. Move only `p2/mp06-bulk-redis-state` with `force: false`.

5. Require after publication:

   - ahead `1`;
   - behind `0`;
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
5. Stop and report if CI fails.
6. After green CI, create:

   `signalguard-rs/phase-2/reports/P2-MP06/<PRODUCT-HEAD-SHA>.md`

The report must reference WEB1, C1, and C2; all preserved gate logs; the base64 round-trip evidence without including the payload; all three exact blob SHAs; tree SHA; commit SHA; non-force ref update; PR URL; and exact-head CI.

Do not modify connector status, control, prompts, repairs, reviews, proofs, integration records, or another report.

## Required final response

Return only:

- same-sandbox integrity result;
- preserved file hashes and gate-evidence integrity result;
- handlers source/base64 lengths and round-trip verification;
- three exact GitHub blob SHAs;
- created tree SHA;
- product commit SHA and parent/message/path verification;
- non-force ref update result;
- product branch comparison result;
- draft PR URL;
- exact-head CI run ID and conclusion;
- connector report path and commit SHA;
- any blocker.
