# P2-MP06-WEB2 Gate Evidence

- Delivery ID: `P2-MP06-WEB2`
- Overall required-gate status: **PASS**
- Product repository: `progeranna/signalguard-rs`
- Product branch: `p2/mp06-bulk-redis-state`
- Exact product base: `1447a3ccb2fa3020738cd2dd3f8d145be6cd202a`
- Final workspace: `/tmp/signalguard-web-worker/workspace`
- Evidence root: `/mnt/data/P2-MP06-WEB2-evidence`
- Execution rule: every accepted shell gate was executed with `set -o pipefail`; each row names its complete log and numeric exit-status file.

## Artifact and corrected explicit preflight

| Gate command | Log | Status file | Tests/result |
|---|---|---|---|
| `uname -a` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/000_os_arch.log` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/000_os_arch.status` | PASS; Linux x86_64 |
| `sha256sum -c` for the required artifact ZIP checksum | `/mnt/data/P2-MP06-WEB2-evidence/preflight/001_artifact_zip_sha.log` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/001_artifact_zip_sha.status` | PASS |
| `unzip -l /mnt/data/signalguard-P2-MP06-WEB6-30220162842.zip` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/002_artifact_zip_list.log` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/002_artifact_zip_list.status` | PASS |
| `unzip -q /mnt/data/signalguard-P2-MP06-WEB6-30220162842.zip` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/003_artifact_unzip.log` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/003_artifact_unzip.status` | PASS |
| `sha256sum -c` for the required inner archive checksum | `/mnt/data/P2-MP06-WEB2-evidence/preflight/004_inner_archive_sha.log` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/004_inner_archive_sha.status` | PASS |
| `tar --zstd -xf chatgpt-web-worker-bootstrap.tar.zst` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/005_inner_archive_extract.log` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/005_inner_archive_extract.status` | PASS |
| `sha256sum -c SHA256SUMS` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/006_bootstrap_payload_checksums.log` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/006_bootstrap_payload_checksums.status` | PASS |
| `python3` manifest identity assertions for request, mini-phase, repository, base SHA and branch | `/mnt/data/P2-MP06-WEB2-evidence/preflight/007_bootstrap_manifest_identity.log` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/007_bootstrap_manifest_identity.status` | PASS |
| `./bootstrap.sh` with final stdout line used as environment-file path | `/mnt/data/P2-MP06-WEB2-evidence/preflight/008_bootstrap_script.log` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/008_bootstrap_script.status` | PASS |
| `rustc --version` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/009_rustc_version.log` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/009_rustc_version.status` | PASS; rustc 1.97.1 |
| `cargo --version` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/010_cargo_version.log` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/010_cargo_version.status` | PASS; cargo 1.97.1 |
| `rustfmt --version` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/011_rustfmt_version.log` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/011_rustfmt_version.status` | PASS; rustfmt 1.9.0-stable |
| `cargo clippy --version` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/012_clippy_version.log` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/012_clippy_version.status` | PASS; clippy 0.1.97 |
| `cargo metadata --locked --offline --no-deps --format-version 1` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/013_cargo_metadata.log` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/013_cargo_metadata.status` | PASS |
| Create correctly formatted disposable Rust crate | `/mnt/data/P2-MP06-WEB2-evidence/preflight/014_disposable_create.log` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/014_disposable_create.status` | PASS |
| Disposable crate `cargo fmt --all --check` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/015_disposable_fmt_check.log` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/015_disposable_fmt_check.status` | PASS |
| Disposable crate `cargo check --offline` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/016_disposable_check.log` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/016_disposable_check.status` | PASS |
| Disposable crate `cargo clippy --offline --all-targets -- -D warnings` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/017_disposable_clippy.log` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/017_disposable_clippy.status` | PASS |
| Disposable crate `cargo test --offline` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/018_disposable_test.log` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/018_disposable_test.status` | PASS; 1 passed |
| Portable Redis `PING` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/020_redis_ping.log` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/020_redis_ping.status` | PASS; PONG |
| Portable Redis ordered `MGET` after setting first and last only | `/mnt/data/P2-MP06-WEB2-evidence/preflight/021_redis_mget_missing_middle.log` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/021_redis_mget_missing_middle.status` | PASS; ordered first / missing / last |
| Portable Redis Lua `SET` + `SADD`, followed by `GET` and `SISMEMBER` proof | `/mnt/data/P2-MP06-WEB2-evidence/preflight/022_redis_lua_set_sadd.log` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/022_redis_lua_set_sadd.status` | PASS |
| Exact embedded workspace `cargo check --locked --offline --all-targets --all-features` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/024_embedded_workspace_check_rerun.log` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/024_embedded_workspace_check_rerun.status` | PASS |
| Portable Redis `SHUTDOWN NOSAVE` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/025_redis_shutdown.log` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/025_redis_shutdown.status` | PASS |
| Portable Redis PID and listening-port cleanup proof | `/mnt/data/P2-MP06-WEB2-evidence/preflight/026_redis_cleanup_proof.log` | `/mnt/data/P2-MP06-WEB2-evidence/preflight/026_redis_cleanup_proof.status` | PASS |

Preflight execution notes, retained rather than hidden:

- `/mnt/data/P2-MP06-WEB2-evidence/preflight/019_redis_start.status` is `1` because the first startup wrapper checked the daemon PID file before it appeared. The server was already reachable; the required `PING`, ordered `MGET`, and Lua gates immediately passed, and cleanup passed.
- `/mnt/data/P2-MP06-WEB2-evidence/preflight/023_embedded_workspace_check.status` is `124` from the execution wrapper limit during compilation. The same exact command was rerun to completion as gate `024` and passed with numeric status `0`.

## Focused gates

| Gate command | Log | Status file | Tests/result |
|---|---|---|---|
| `cargo test --locked --offline --lib bulk_state -- --nocapture` | `/mnt/data/P2-MP06-WEB2-evidence/focused/002_bulk_cache_unit_tests_rerun.log` | `/mnt/data/P2-MP06-WEB2-evidence/focused/002_bulk_cache_unit_tests_rerun.status` | PASS; 8 passed, 0 failed |
| `cargo test --locked --offline --lib dashboard_summary_handler -- --nocapture` | `/mnt/data/P2-MP06-WEB2-evidence/focused/003_dashboard_handler_tests.log` | `/mnt/data/P2-MP06-WEB2-evidence/focused/003_dashboard_handler_tests.status` | PASS; 12 passed, 0 failed |
| `cargo test --locked --offline --lib dashboard_summary_accepts_demo_mode_query -- --nocapture` | `/mnt/data/P2-MP06-WEB2-evidence/focused/004_demo_dashboard_compatibility.log` | `/mnt/data/P2-MP06-WEB2-evidence/focused/004_demo_dashboard_compatibility.status` | PASS; 1 passed, 0 failed |

The first focused invocation is retained at `/mnt/data/P2-MP06-WEB2-evidence/focused/001_bulk_cache_unit_tests.*`; status `124` records an execution-wrapper limit while compilation was still running. The identical command completed as gate `002` with 8/8 passing.

Focused coverage includes empty input; BTCUSDT/ETHUSDT in both orders; duplicates; missing first, middle and last entries; malformed JSON; embedded-symbol mismatch; in-memory ordering and missing semantics; dashboard state/health attachment; anomaly isolation; absent dashboard state; Demo compatibility; and cache-error propagation.

## Full Rust gates

| Gate command | Log | Status file | Tests/result |
|---|---|---|---|
| `cargo fmt --all` | `/mnt/data/P2-MP06-WEB2-evidence/full/001_cargo_fmt_all.log` | `/mnt/data/P2-MP06-WEB2-evidence/full/001_cargo_fmt_all.status` | PASS |
| `cargo fmt --all --check` | `/mnt/data/P2-MP06-WEB2-evidence/full/002_cargo_fmt_all_check.log` | `/mnt/data/P2-MP06-WEB2-evidence/full/002_cargo_fmt_all_check.status` | PASS |
| `cargo check --locked --offline --all-targets --all-features` | `/mnt/data/P2-MP06-WEB2-evidence/full/003_cargo_check.log` | `/mnt/data/P2-MP06-WEB2-evidence/full/003_cargo_check.status` | PASS |
| `cargo clippy --locked --offline --all-targets --all-features -- -D warnings` | `/mnt/data/P2-MP06-WEB2-evidence/full/004_cargo_clippy.log` | `/mnt/data/P2-MP06-WEB2-evidence/full/004_cargo_clippy.status` | PASS; zero warnings accepted |
| `cargo test --locked --offline --all-targets --all-features` | `/mnt/data/P2-MP06-WEB2-evidence/full/005_cargo_test_all.log` | `/mnt/data/P2-MP06-WEB2-evidence/full/005_cargo_test_all.status` | PASS; library 369 passed, 3 ignored; all other non-ignored targets passed; 20 service-backed tests remained intentionally ignored for their dedicated gates |

## Isolated real-Redis gates

| Gate command | Log | Status file | Tests/result |
|---|---|---|---|
| Portable Redis startup with explicit readiness loop | `/mnt/data/P2-MP06-WEB2-evidence/redis/003_redis_start_retry.log` | `/mnt/data/P2-MP06-WEB2-evidence/redis/003_redis_start_retry.status` | PASS |
| Portable Redis `PING` | `/mnt/data/P2-MP06-WEB2-evidence/redis/004_redis_ping.log` | `/mnt/data/P2-MP06-WEB2-evidence/redis/004_redis_ping.status` | PASS; PONG |
| `REDIS_URL=redis://127.0.0.1:33917/ cargo test --locked --offline --test redis_cache -- --ignored --test-threads=1` | `/mnt/data/P2-MP06-WEB2-evidence/redis/005_redis_cache_ignored.log` | `/mnt/data/P2-MP06-WEB2-evidence/redis/005_redis_cache_ignored.status` | PASS; 8 passed, 0 failed |
| `REDIS_URL=redis://127.0.0.1:33917/ cargo test --locked --offline --test redis_cache bulk_market_state_read_uses_one_mget_and_preserves_order -- --ignored --test-threads=1` | `/mnt/data/P2-MP06-WEB2-evidence/redis/006_redis_bulk_read_filter.log` | `/mnt/data/P2-MP06-WEB2-evidence/redis/006_redis_bulk_read_filter.status` | PASS; 1 passed; Redis command statistics prove one `MGET` and zero `GET` commands |
| `REDIS_URL=redis://127.0.0.1:33917/ cargo test --locked --offline --lib atomic_market_state_write -- --ignored --test-threads=1` | `/mnt/data/P2-MP06-WEB2-evidence/redis/007_atomic_market_state_write.log` | `/mnt/data/P2-MP06-WEB2-evidence/redis/007_atomic_market_state_write.status` | PASS; 3 passed, 0 failed |
| Redis `DBSIZE` cleanup proof | `/mnt/data/P2-MP06-WEB2-evidence/redis/008_redis_db_empty.log` | `/mnt/data/P2-MP06-WEB2-evidence/redis/008_redis_db_empty.status` | PASS; dbsize 0 |
| Redis `SHUTDOWN NOSAVE` | `/mnt/data/P2-MP06-WEB2-evidence/redis/009_redis_shutdown.log` | `/mnt/data/P2-MP06-WEB2-evidence/redis/009_redis_shutdown.status` | PASS |
| Redis PID and listening-port cleanup proof | `/mnt/data/P2-MP06-WEB2-evidence/redis/010_redis_cleanup_proof.log` | `/mnt/data/P2-MP06-WEB2-evidence/redis/010_redis_cleanup_proof.status` | PASS |

The first real-Redis startup attempt is retained at `/mnt/data/P2-MP06-WEB2-evidence/redis/001_redis_start.*`; the wrapper observed the same PID-file readiness race and returned `1`. It was cleaned successfully by gate `002`; no Redis test gate ran against that instance. Corrected startup gate `003` passed before all Redis tests.

## Scope, hygiene, secret and Lua-integrity gates

| Gate command | Log | Status file | Result |
|---|---|---|---|
| Baseline extracted-tree SHA-256 inventory | `/mnt/data/P2-MP06-WEB2-evidence/scope/000_base_tree.sha256` | `/mnt/data/P2-MP06-WEB2-evidence/scope/000_base_tree.status` | PASS |
| Current-tree SHA-256 inventory and exact changed-path assertion | `/mnt/data/P2-MP06-WEB2-evidence/scope/001_changed_path_inventory.log` | `/mnt/data/P2-MP06-WEB2-evidence/scope/001_changed_path_inventory.status` | PASS; exactly `src/api/handlers.rs`, `src/storage/redis.rs`, `tests/redis_cache.rs` |
| `git diff --no-index --check` equivalent against frozen base and final trees | `/mnt/data/P2-MP06-WEB2-evidence/scope/002_whitespace_diff_check.log` | `/mnt/data/P2-MP06-WEB2-evidence/scope/002_whitespace_diff_check.status` | PASS |
| Complete no-index diff and stat capture | `/mnt/data/P2-MP06-WEB2-evidence/scope/003_full_diff.log` | `/mnt/data/P2-MP06-WEB2-evidence/scope/003_full_diff.status` | PASS |
| Forbidden-path inventory assertion | `/mnt/data/P2-MP06-WEB2-evidence/scope/004_forbidden_path_inventory.log` | `/mnt/data/P2-MP06-WEB2-evidence/scope/004_forbidden_path_inventory.status` | PASS |
| High-confidence secret scan over changed files | `/mnt/data/P2-MP06-WEB2-evidence/scope/005_secret_scan.log` | `/mnt/data/P2-MP06-WEB2-evidence/scope/005_secret_scan.status` | PASS |
| Byte-for-byte P2-MP05 Lua-script extraction and equality assertion | `/mnt/data/P2-MP06-WEB2-evidence/scope/006_lua_integrity.log` | `/mnt/data/P2-MP06-WEB2-evidence/scope/006_lua_integrity.status` | PASS; both SHA-256 `01a0efcafae25cc866d6e620141806c9db04c58521cec2bf644acc4ed67094f7`, 607 bytes |
| Static bulk-strategy proof | `/mnt/data/P2-MP06-WEB2-evidence/scope/007_bulk_strategy_static_proof.log` | `/mnt/data/P2-MP06-WEB2-evidence/scope/007_bulk_strategy_static_proof.status` | PASS; one bulk call, `MGET`, zero mapper awaits, no per-symbol Redis loop |
| `GitHub.compare_commits` exact remote-branch identity check | `/mnt/data/P2-MP06-WEB2-evidence/scope/008_remote_branch_unchanged.log` | `/mnt/data/P2-MP06-WEB2-evidence/scope/008_remote_branch_unchanged.status` | PASS; ahead 0, behind 0, identical to base |

## Frozen archive and connector escrow integrity

| Gate command | Log | Status file | Result |
|---|---|---|---|
| Compute all final file sizes, SHA-256 and Git blob SHAs | `/mnt/data/P2-MP06-WEB2-evidence/delivery/001_final_file_identities.log` | `/mnt/data/P2-MP06-WEB2-evidence/delivery/001_final_file_identities.status` | PASS |
| Deterministic sorted epoch-zero numeric-owner zstd tar creation | `/mnt/data/P2-MP06-WEB2-evidence/delivery/002_archive_create.log` | `/mnt/data/P2-MP06-WEB2-evidence/delivery/002_archive_create.status` | PASS |
| Extract archive and assert exact three paths plus all file SHA-256/Git blob identities | `/mnt/data/P2-MP06-WEB2-evidence/delivery/003_archive_verify.log` | `/mnt/data/P2-MP06-WEB2-evidence/delivery/003_archive_verify.status` | PASS |
| Single-line base64 and 8,192-character chunk creation | `/mnt/data/P2-MP06-WEB2-evidence/delivery/004_base64_chunk_create.log` | `/mnt/data/P2-MP06-WEB2-evidence/delivery/004_base64_chunk_create.status` | PASS; length 18,012; 3 chunks |
| Concatenate chunks, decode, and byte-compare reconstructed archive | `/mnt/data/P2-MP06-WEB2-evidence/delivery/005_base64_decode_verify.log` | `/mnt/data/P2-MP06-WEB2-evidence/delivery/005_base64_decode_verify.status` | PASS |
| Fetch connector chunk `0000.b64` from returned commit and verify blob, 8,192 characters and zero newlines | `/mnt/data/P2-MP06-WEB2-evidence/delivery/006_chunk_0000_remote_verify.log` | `/mnt/data/P2-MP06-WEB2-evidence/delivery/006_chunk_0000_remote_verify.status` | PASS; commit `90f9b01758bff98b1c9b2193bdb6eef29acce076` |
| Fetch connector chunk `0001.b64` from returned commit and verify blob, 8,192 characters and zero newlines | `/mnt/data/P2-MP06-WEB2-evidence/delivery/007_chunk_0001_remote_verify.log` | `/mnt/data/P2-MP06-WEB2-evidence/delivery/007_chunk_0001_remote_verify.status` | PASS; commit `b2d1b481f9e6eb44d3ce8ed9a91fe7f6fbdc029e` |
| Fetch connector chunk `0002.b64` from returned commit and verify blob, 1,628 characters and zero newlines | `/mnt/data/P2-MP06-WEB2-evidence/delivery/008_chunk_0002_remote_verify.log` | `/mnt/data/P2-MP06-WEB2-evidence/delivery/008_chunk_0002_remote_verify.status` | PASS; commit `ac25d2265d1352ca477056a903da0e1b701806c1` |

No product-repository write action was invoked. No product blob, tree, commit, ref, branch, pull request, or product file was created through the GitHub connector.
