# P2-MP04 validated API contract repair

- Original contract: `signalguard-rs/phase-2/prompts/P2-MP04.md` at connector commit `5d0950bf1f6cbcb30e637773c7c273a291586001`.
- Continuation contract: `signalguard-rs/phase-2/repairs/P2-MP04-C1.md` at connector commit `5d0950bf1f6cbcb30e637773c7c273a291586001`.
- Repair contract: `signalguard-rs/phase-2/repairs/P2-MP04-R1.md` at connector commit `1a4ae7e01d51c15072e9b2d19bd5dfe756eb9308`.

Repository: `progeranna/signalguard-rs`  
Worktree: `/Users/anion/Desktop/work/git-signalguard-rs/worktrees/p2-mp04`  
Branch: `p2/mp04-api-contract`  
Base: `1a226b5b5661a2b99dabec579aeeecf8b0e4be85`  
Implementation commit: `0a02f5bbb7b30bec96a5137c328169d857894150`  
Repair commit: `ccbf8967bfaafab51a2785883d666eae80aba7de`  
PR: https://github.com/progeranna/signalguard-rs/pull/21 (draft, base `refactor/data-boundaries`)

## Scope and source

The checked artifact is `contracts/web-console.openapi.json`, OpenAPI 3.0.3. DTOs and request/query types in `src/api/dto.rs` derive `schemars::JsonSchema`; `src/api/contract.rs` collects those generated schemas, normalizes OpenAPI 3.0 nullable unions/reference wrappers, and assembles deterministic route metadata. `schemars` is the focused schema dependency because it mechanically derives component fields from typed Rust definitions without handler annotations or runtime changes.

The exporter is `src/bin/export-api-contract.rs`:

- write: `cargo run --quiet --bin export-api-contract -- --write`
- check: `cargo run --quiet --bin export-api-contract -- --check`

The checked artifact is generated, not hand-maintained. Byte equality, deterministic generation, isolated intentional drift failure, and two no-write checks are covered by `api::contract` tests and exporter checks.

## Endpoint inventory

- `GET /health`
- `GET /runtime/mode`
- `POST /runtime/mode`
- `GET /pipeline/health`
- `GET /dashboard/summary?mode` (`mode` optional, `demo|live`)
- `GET /symbols`
- `GET /market/{symbol}/state` (`symbol` required path parameter)
- `GET /market/{symbol}/health` (`symbol` required path parameter)
- `GET /market/{symbol}/timeline?mode` (`symbol` required, `mode` optional)
- `GET /anomalies?symbol&limit` (both optional)

`GET /metrics` is explicitly excluded from JSON schemas and documented in `x-signalguard-metrics` as Prometheus text with content type `text/plain; version=0.0.4; charset=utf-8`.

The error schema is `ApiErrorResponse` with required `error` and `message`. Published reachable status responses are the existing handler statuses: `400`, `403`, `404`, `409`, `500`, and `503`, attached only to operations that can reach them.

OpenAPI 3.0 nullable referenced dashboard `state` and `health` use `allOf: [{"$ref": ...}]` plus `nullable: true`. Option response fields are required and nullable; Option request fields are optional and nullable, matching Serde absence and explicit JSON null behavior. Decimal fields are strings, UUIDs use `format: uuid`, timestamps use `format: date-time`, enums and arrays/nested objects are derived and tested.

## Compatibility and route proof

`web/src/features/dashboard/api-contract.test.ts` contains one reusable unknown/narrow-structural `validateCompatibility` validator. The real artifact passes. Isolated cloned fixtures are rejected through validator failure for parameter name, requiredness, nullability, enum mutation, and required-property removal. It also verifies mode/symbol placement, additive schema compatibility, nullable dashboard state/health, market decimal strings, timeline arrays/date-times, anomaly severity, runtime mode request/response, and metrics disposition.

Backend tests in `src/api/contract.rs` prove all declared paths and methods, including GET+POST runtime mode, actual query/path names, `symbol`, metrics disposition, schema formats/enums/arrays/nested objects, required-nullable responses, optional-nullable requests, artifact equality, deterministic bytes, and isolated drift failure.

## Gates

Local Rust gates passed: `cargo fmt --all`, `cargo fmt --all --check`, `cargo check --all-targets --all-features`, `cargo clippy --all-targets --all-features -- -D warnings`, `cargo test --all-targets --all-features` (375 passed, 3 pre-existing environment-dependent ignored), and `git diff --check`.

Local frontend gates passed: `npm ci`, focused compatibility test (6 passed), `npm run test:run` (23 files, 289 tests passed), `npm run typecheck`, `npm run lint`, `npm run build`, and `npm run bundle:check`.

Forbidden-path proof passed against the exact base: `src/api/handlers.rs`, `src/storage/redis.rs`, `tests/redis_cache.rs`, and `web/src/features/dashboard/types.ts` are unchanged. No runtime endpoint, serialization, status-code, database/cache, frontend query, view-model, or presentation behavior was modified.

Exact-head CI run: `30273482153`, conclusion `success` for repair head `ccbf8967bfaafab51a2785883d666eae80aba7de`; Rust and frontend jobs passed. The prior failed candidate run was `30268071440`.
