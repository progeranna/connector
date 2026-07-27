# SignalGuard RS P2-MP06-WEB2 — Durable Web-Worker Replacement

## Purpose

Re-execute P2-MP06 in a fresh ChatGPT web-worker sandbox after WEB1 implementation state was lost before durable delivery.

WEB1 demonstrated that the portable Rust/Redis environment and complete gates work, but its final files were held only in ephemeral `/mnt/data`. WEB2 fixes that design: after all gates pass, the worker must store a deterministic compressed archive of the three final product files as small immutable base64 chunks in `progeranna/connector`.

The web worker must not write to the product repository. A separately controlled product-side GitHub Actions relay will reconstruct the escrow, independently verify it, repeat all product and Redis gates, create one commit, non-force push the assigned branch, and open the draft PR.

## Exact product state

- Product repository: `progeranna/signalguard-rs`
- Assigned product branch: `p2/mp06-bulk-redis-state`
- Exact assigned base and required initial remote branch head: `1447a3ccb2fa3020738cd2dd3f8d145be6cd202a`
- PR base: `refactor/data-boundaries`
- Required commit message: `perf(api): load dashboard market states in bulk`
- Delivery ID: `P2-MP06-WEB2`

The Orchestrator verified that the assigned branch remains identical to the exact base: ahead `0`, behind `0`, no commit and no PR.

## Binding implementation requirements

The original and continuation semantics remain binding:

- `signalguard-rs/phase-2/prompts/P2-MP06.md`
- `signalguard-rs/phase-2/repairs/P2-MP06-C1.md`
- `signalguard-rs/phase-2/repairs/P2-MP06-C2.md`
- `signalguard-rs/phase-2/repairs/P2-MP06-WEB1.md`

WEB2 supersedes WEB1-C1 and WEB1-C2 only as delivery/recovery mechanisms.

Implement independently from the exact base embedded in the bootstrap artifact. Do not reconstruct files from WEB1 chat text, inaccessible sandbox files, invalid unreferenced blobs, or the local Codex worktree.

## Verified bootstrap artifact

Use:

- connector repository: `progeranna/connector`
- workflow run ID: `30220162842`
- artifact ID: `8636970817`
- artifact name: `signalguard-P2-MP06-WEB6-30220162842`
- ZIP SHA-256: `ab12f92e7835dd4e5c56878c6a3fad7e1ddac8c97f8e1e9152778140792372ac`
- inner archive SHA-256: `8afe14a493ae1170f7fe595993e9f268c12f0d91187027257c7d056e194e96b8`
- embedded product SHA: `1447a3ccb2fa3020738cd2dd3f8d145be6cd202a`
- expiry: `2026-07-29T21:01:10Z`

The artifact contains portable Rust, exact vendored Cargo dependencies, exact base source, and portable Redis.

Run the corrected explicit preflight from WEB1 rather than the artifact's opaque `preflight.sh`.

## Authorized product paths

Modify only:

- `src/storage/redis.rs`
- `src/api/handlers.rs`
- `tests/redis_cache.rs`

Do not modify dependencies, lockfiles, frontend, CI, workflows, Docker, migrations, documentation, or another backend path.

## Required implementation

Implement:

`get_market_states(&[Symbol]) -> Result<Vec<(Symbol, Option<MarketState>)>, CacheError>`

Requirements:

- empty input returns an empty result without Redis access;
- one Redis `MGET` or one actually executed bulk pipeline for all requested state keys;
- no sequential or parallel per-symbol `GET` loop;
- explicit requested-symbol association;
- stable input order, including duplicate symbols;
- correct missing first, middle, and last positions;
- malformed JSON returns `CacheError::InvalidData` identifying the affected requested symbol;
- embedded-symbol mismatch returns `CacheError::InvalidData` identifying requested and embedded symbols;
- in-memory behavior has the same ordering and missing-state semantics;
- dashboard performs one bulk cache read after `list_symbols()` and no awaited cache read inside its summary loop;
- dashboard state and health remain attached to the correct symbol;
- absent state preserves null state and null health;
- Demo mode, public routes, API error mapping, Redis keys, and P2-MP05 atomic Lua write remain unchanged.

Decimal fixtures representing scale-0 numeric `100` and `200` must expect `"100"` and `"200"`. Production decimal serialization must not change.

Use the smallest explicit Redis command result type required in integration tests.

## Mandatory preflight and gates

No connector escrow write is allowed before implementation and all required gates pass.

Run:

- artifact checksum and manifest verification;
- Rust/Cargo/rustfmt/Clippy versions;
- locked offline Cargo metadata;
- correctly formatted disposable crate fmt/check/Clippy/test;
- portable Redis `PING`, ordered `MGET` with missing middle value, and Lua `SET + SADD`;
- exact embedded workspace `cargo check --locked --offline --all-targets --all-features`.

Focused tests must cover:

- empty input;
- BTCUSDT and ETHUSDT in both orders;
- duplicate symbol ordering;
- missing first, middle, and last values;
- malformed JSON;
- embedded-symbol mismatch;
- in-memory behavior;
- dashboard state and health mapping;
- absent dashboard state;
- real-Redis bulk retrieval.

Full gates:

- `cargo fmt --all`
- `cargo fmt --all --check`
- `cargo check --locked --offline --all-targets --all-features`
- `cargo clippy --locked --offline --all-targets --all-features -- -D warnings`
- `cargo test --locked --offline --all-targets --all-features`
- exact changed-path inventory;
- whitespace/diff check;
- forbidden-path inventory;
- secret scan;
- byte-for-byte proof that the P2-MP05 Lua script is unchanged.

Real Redis gates:

- `cargo test --locked --offline --test redis_cache -- --ignored --test-threads=1`
- dedicated bulk-read ignored test/filter;
- `cargo test --locked --offline --lib atomic_market_state_write -- --ignored --test-threads=1`
- Redis cleanup proof.

Run every gate separately with `set -o pipefail`, preserve one log and one numeric exit-status file per command, and stop if any required gate fails, is skipped, or lacks evidence.

## Durable escrow protocol

The worker must not call any product-repository write action.

After all gates pass and the three final files are frozen:

### 1. Create deterministic archive

From the final workspace create:

`/mnt/data/P2-MP06-WEB2-product-files.tar.zst`

The archive must contain exactly:

- `src/storage/redis.rs`
- `src/api/handlers.rs`
- `tests/redis_cache.rs`

Use deterministic tar metadata:

- sorted paths;
- mtime epoch zero;
- owner and group zero;
- numeric owner;
- zstd compression.

Example shape:

`tar --sort=name --mtime='@0' --owner=0 --group=0 --numeric-owner -I 'zstd -19 -T0' -cf ... src/storage/redis.rs src/api/handlers.rs tests/redis_cache.rs`

Verify the archive extracts to exactly the three authorized paths and reproduces every final file SHA-256 and Git blob SHA.

### 2. Base64 and chunk

Create a single-line base64 representation and split it into chunks of exactly 8192 characters except the final chunk.

Chunk names:

- `0000.b64`
- `0001.b64`
- and so on, zero-padded to four digits.

No chunk may contain a newline.

### 3. Upload chunks to connector

Upload every chunk sequentially with `GitHub.create_file` to:

`signalguard-rs/phase-2/web-deliveries/P2-MP06-WEB2/chunks/<CHUNK-NAME>`

Repository: `progeranna/connector`

Branch: `main`

Commit message per chunk:

`delivery: escrow P2-MP06-WEB2 chunk <CHUNK-NAME>`

After every upload, fetch the created path from the resulting connector commit and require exact chunk content and exact character count.

Do not upload product source as visible Markdown, issue text, PR text, or chat output. Base64 chunks belong only in connector files and tool-call arguments.

### 4. Upload gate evidence summary

Create:

`signalguard-rs/phase-2/web-deliveries/P2-MP06-WEB2/GATES.md`

It must list every gate command, log path, exit-status path, test count, and result. It must not contain hidden reasoning or source-file contents.

### 5. Upload manifest last

Only after every chunk and `GATES.md` are durably verified, create:

`signalguard-rs/phase-2/web-deliveries/P2-MP06-WEB2/MANIFEST.json`

The manifest must be valid JSON with exactly these essential fields:

- `delivery_id`: `P2-MP06-WEB2`
- `gate_status`: `PASS`
- `product_repository`: `progeranna/signalguard-rs`
- `product_branch`: `p2/mp06-bulk-redis-state`
- `product_base_sha`: `1447a3ccb2fa3020738cd2dd3f8d145be6cd202a`
- `commit_message`: `perf(api): load dashboard market states in bulk`
- `archive_sha256`
- `archive_base64_length`
- `chunk_size`: `8192`
- `chunk_count`
- `chunk_prefix`: `signalguard-rs/phase-2/web-deliveries/P2-MP06-WEB2/chunks`
- `gates_path`: `signalguard-rs/phase-2/web-deliveries/P2-MP06-WEB2/GATES.md`
- `files`: exactly three objects, each containing `path`, `size_bytes`, `sha256`, and `git_blob`
- bootstrap artifact identity and checksums
- web-worker OS and architecture

Manifest commit message:

`delivery: finalize P2-MP06-WEB2 escrow`

Return the real connector commit SHA containing the manifest. That commit makes the whole delivery immutable for the relay.

## Product-side relay

A controlled workflow already exists only on temporary product branch:

`infra/p2-mp06-web-relay`

Workflow commit:

`867cae81b042d564cbc0d3207193d618d18e083a`

The worker must not trigger it and must not create a relay request. The Orchestrator will independently inspect the manifest/chunks and trigger the relay afterward.

The relay will:

- fetch escrow from the exact connector manifest commit;
- verify archive/chunk/file hashes;
- require the target branch still equals the exact base;
- repeat full Rust and real-Redis gates;
- require exactly three changed paths;
- create exactly one commit with the exact required message and parent;
- non-force push only `p2/mp06-bulk-redis-state`;
- open or reuse one draft PR into `refactor/data-boundaries`;
- record its result on the temporary relay branch.

## Required final response

Return only:

- web-worker OS and architecture;
- artifact ID and both artifact checksums;
- preflight summary;
- final workspace path;
- exact changed paths;
- bulk API signature and Redis strategy;
- focused/full/real-Redis gate summaries with evidence paths;
- final three file sizes, SHA-256 values, and Git blob SHAs;
- deterministic archive path, size, and SHA-256;
- base64 length, chunk size, chunk count;
- connector chunk prefix;
- `GATES.md` path and commit SHA;
- `MANIFEST.json` path and immutable connector commit SHA;
- confirmation that no product repository write occurred;
- any blocker.
