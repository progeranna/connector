# P3-W4-BRIDGE01 — Backend semantic health facts

Status: `P3_W4_BRIDGE01_IMPLEMENTATION_AUTHORIZED`

## Worker mode

Dedicated local Codex implementation worker.

Use the `$rust-development` skill.

This is the first semantic Wave 4 bridge. It is a narrow backend/API-contract implementation from the independently accepted Checkpoint 2R product.

The worker may use the authenticated local checkout, shell, Cargo, Node/npm, Docker and local test infrastructure required by the validation profile.

Do not use a GitHub-web-only worker for implementation.

## Required connector authority

Before product work, fetch and read completely from `progeranna/connector`:

- `signalguard-rs/phase-3/control/CURRENT_EXECUTION.md`
- `signalguard-rs/phase-3/control/STATUS.md`
- `signalguard-rs/phase-3/control/MICRO_PHASE_LEDGER.md`
- `signalguard-rs/phase-3/control/IMPLEMENTATION_SEQUENCE.md`
- `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-RERUN-AFTER-R4.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-AFTER-R4/23656c9b93a24bfc20ba8f417275564bb5b5d240.md`
- `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-RERUN-AFTER-R4-REVIEW.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-AFTER-R4-REVIEW/23656c9b93a24bfc20ba8f417275564bb5b5d240.md`

Required current state:

`P3_W4_BRIDGE01_IMPLEMENTATION_AUTHORIZED`

Checkpoint acceptance authority:

- review contract publication commit: `43fcd00c899d01dbf13f1e4b7f0d69735d6d0fbb`
- review contract blob: `44702b5fee9a34ea25d9372d9b6726ff027fb1cd`
- accepted review report publication commit: `c7a5be7aa935f952fc386d373c380b2220da8fe1`
- accepted review report blob: `96d5e3c2d7cf6b0965f69954f1f8249678b44dce`
- accepted terminal status: `P3_CHECKPOINT_2R_RERUN_AFTER_R4_ACCEPTED`

The implementation must stop if any authority identity above is missing, rewritten, or inconsistent with current control.

## Exact product base

Product repository:

`progeranna/signalguard-rs`

Target branch:

`refactor/dashboard-modules`

Immutable implementation base:

`23656c9b93a24bfc20ba8f417275564bb5b5d240`

Expected base tree:

`d8c0289a05b3646b3abc7056bd269b927e61d5c4`

Expected ordered parents of the base merge:

1. `7dab5647d322339f5bd9d0514e5178522d5181c0`
2. `79abb161e7a731df7077d49b44481eaaf25bf762`

Before creating a worker branch, fetch the authenticated remote and prove:

- `origin/refactor/dashboard-modules` resolves exactly to the immutable base;
- its tree is exact;
- its ordered parents are exact;
- compare from immutable base to target is identical, zero ahead, zero behind, zero changed files.

Any target drift is a hard blocker. Do not silently rebase this contract onto a newer target.

## Required branch and product commit

Create exactly one worker branch from the immutable base:

`p3/w4-bridge01-semantic-health-facts`

Create exactly one product commit:

`feat(api): expose semantic health facts`

Do not squash several implementation commits after the fact. The worker result must naturally be one cohesive product commit.

Do not create a PR and do not merge. Independent review and GitHub-web integration are separate later workers.

## Exact writable lease

Only these product paths may change:

```text
src/config.rs
src/health/scoring.rs
src/api/dto.rs
src/api/handlers.rs
src/api/demo_data.rs
src/api/contract.rs
contracts/web-console.openapi.json
```

Directly matching Rust tests embedded in or already colocated with those exact modules are part of the lease.

No other production or test path is writable.

If a necessary change appears to require another path, stop and report the blocker rather than expanding scope.

## Forbidden adjacent scope

Do not modify:

- any `web/` source, tests, schemas, Zod models, adapters, JSX, CSS or assets;
- endpoint paths or route identity;
- detector algorithms or detector source files;
- database schema, SQL, migrations or persistence behavior;
- runtime switching behavior unrelated to fact exposure;
- ticker code, text, selectors, CSS or animation ownership;
- dependencies, package manifests or lockfiles;
- Cargo dependency manifests unless already unchanged by this bridge;
- public Replay exposure;
- Demo/Live ownership or isolation rules;
- bundle budgets;
- modal behavior, routing or Checkpoint 2R recovery code.

Do not begin Bridge02, P3-MP21…P3-MP30, dialog work or any later phase.

## Current backend facts that must remain authoritative

The accepted base already has backend-owned health configuration and evaluation primitives:

- `HealthScoreSettings` owns base score, severity penalties, stale-data penalty, recent-anomaly window and status thresholds;
- detector configuration owns `stale_data_ms_threshold` and detector thresholds;
- `HealthEvaluation` owns score, status, evaluation time, signals and penalties;
- health penalties already carry penalty, anomaly type/severity, observed value, threshold value and event time;
- `DashboardHealthSummary` and `MarketHealthResponse` already expose part of this information;
- Demo dashboard health is evaluated through the same health-scoring implementation using injected health/detector settings.

Bridge01 must extend these existing authorities. Do not create a second scoring engine or a frontend-oriented duplicate source of truth.

## Required semantic result

The backend must publish enough additive, typed facts for Bridge02 and Wave 4 to render Data Age, System/Market health and tooltips without inventing thresholds, arithmetic or issue selection in the frontend.

### 1. Add authoritative delayed Data Age threshold

Add one runtime health configuration value named:

`delayed_after_ms`

Use environment variable:

`SIGNALGUARD_HEALTH_DELAYED_AFTER_MS`

Default value:

`2500`

The existing detector stale threshold remains the one and only authoritative stale boundary:

`DetectorSettings::stale_data_ms_threshold`

Do not create a second independent stale configuration value.

Required effective invariant after all settings are loaded:

```text
0 <= delayed_after_ms <= stale_data_ms_threshold
```

Because the type is unsigned, the lower bound is structural; the implementation must explicitly validate the upper bound and return a clear configuration error naming the relevant environment settings when violated.

Boundary tests must cover at least:

- `delayed_after_ms = 0` accepted;
- `delayed_after_ms = stale_data_ms_threshold` accepted;
- `delayed_after_ms > stale_data_ms_threshold` rejected;
- default `2500` with default stale `5000` accepted.

Do not change the meaning or default of the existing stale detector threshold.

### 2. Publish Data Age thresholds as facts

Every public semantic health representation used by Dashboard summary / market health must expose the actual effective values required to classify Data Age:

- `delayed_after_ms` from health settings;
- `stale_after_ms` derived directly from `DetectorSettings::stale_data_ms_threshold`.

Frontend code must not need to know the defaults or reconstruct these values later.

The existing `last_event_age_ms` signal remains the observed age authority.

### 3. Publish health status boundaries as facts

Expose explicit score boundaries with semantic names:

- `degraded_below_score` = current `healthy_min_score`;
- `unhealthy_below_score` = current `degraded_min_score`.

Preserve the current classification semantics:

```text
score >= healthy_min_score                    => healthy
degraded_min_score <= score < healthy_min_score => degraded
score < degraded_min_score                    => unhealthy
```

Do not duplicate or fork classification logic. Facts must come from the same `HealthStatusThresholds` used by scoring.

### 4. Preserve evaluation time

`evaluated_at` is already backend-owned and must remain the exact evaluation time authority.

The additive semantic facts exposed by both Dashboard summary health and market-health detail must carry or directly reference that exact evaluation timestamp. Do not substitute browser time, serialization time or a second `Utc::now()` value after scoring.

### 5. Deterministic primary issue

Add a backend-derived optional `primary_issue` for each health evaluation/public health representation.

It must be selected only from the evaluation's actual `penalties` and must never be synthesized from unrelated frontend/presentation state.

Selection must be deterministic. Use this exact precedence:

1. larger `penalty` first;
2. if tied, severity rank `critical > warning > info > None`;
3. if tied, newer `event_time` first, with `None` after a concrete time;
4. if tied, lexicographically smaller anomaly type string first, with `None` after a concrete anomaly type;
5. if still tied, lexicographically smaller `reason` first.

If there are no penalties, `primary_issue` must be `null` / `None`.

The selected primary issue must preserve the exact same facts as the corresponding penalty; do not recalculate a conflicting copy.

### 6. Enrich penalty measurement semantics

Preserve all existing penalty fields and add typed semantic facts sufficient for truthful Observed / Threshold / Exceeded-by presentation.

For each penalty expose:

- existing `penalty`;
- existing `observed_value`;
- existing `threshold_value`;
- additive `unit`;
- additive `comparison`;
- additive `exceeded_by`.

Use typed serialized enum/string values, not display-copy strings.

Required units for current anomaly families:

- price move: `percent`;
- spread spike: `percent`;
- trade burst: `trades_per_minute`;
- stale data: `milliseconds`;
- quote stuck: `milliseconds`;
- event lag spike: `milliseconds`;
- depth sequence gap: `sequence_increment`.

Required comparisons:

- price move: `absolute_greater_than_or_equal`;
- all other currently thresholded anomaly families above: `greater_than_or_equal`.

For a penalty with both observed and threshold values:

```text
greater_than_or_equal:
    exceeded_by = max(observed_value - threshold_value, 0)

absolute_greater_than_or_equal:
    exceeded_by = max(abs(observed_value) - threshold_value, 0)
```

If either observed or threshold is absent, `exceeded_by` must be absent and `unit`/`comparison` must still be semantically correct when the anomaly type makes them knowable.

Do not alter detector emission thresholds or anomaly detection algorithms in this bridge.

Tests must cover positive and negative price-move observations, equal-boundary arithmetic, normal greater-than arithmetic, and missing measurement values.

### 7. Exact source / mode / symbol identity

The new semantic health facts must be identity-safe.

For every Dashboard symbol health result and market-health response, a consumer must be able to verify the exact:

- public source (`demo` or `live`);
- public mode (`demo` or `live`);
- symbol.

Preserve all existing top-level `source` and `symbol` fields. Add the minimum additive typed identity fields/structure necessary so the semantic facts themselves cannot be detached and accidentally reused for a different mode or symbol.

Required invariant:

```text
semantic source == semantic mode == response/parent public source
semantic symbol == response/parent symbol
```

Do not introduce Replay as a public mode.

### 8. Dashboard summary and market-health consistency

The same backend semantic model must feed:

- `DashboardHealthSummary` inside `/api/dashboard/summary` (existing endpoint identity preserved);
- `MarketHealthResponse` from the existing market-health endpoint.

For the same source/symbol/settings/evaluation inputs, thresholds, primary-issue selection and measurement semantics must agree.

Do not implement two independently drifting DTO calculations.

### 9. Demo alignment and determinism

Demo must remain deterministic and source `demo`.

New semantic facts in Demo must be calculated from the actual `HealthScoreSettings` and `DetectorSettings` passed to Demo generation, including:

- effective `delayed_after_ms`;
- effective stale threshold;
- effective health score boundaries;
- health penalties and deterministic primary issue;
- semantic measurement metadata.

Do not hardcode the new semantic threshold facts to defaults inside Demo.

Do not present Demo data as Live, and do not use Live state as a fallback for Demo.

Existing deterministic Demo anomaly fixture payloads must not be opportunistically redesigned in this bridge. Change a fixture value only when necessary to satisfy the new semantic-contract consistency and cover it with a focused deterministic test.

### 10. Additive API compatibility

This bridge is additive.

Preserve:

- all existing endpoint paths and HTTP methods;
- existing fields and their meanings;
- existing source values;
- current Dashboard/market-health availability behavior;
- existing anomaly UUID identity;
- existing Demo/Live isolation;
- existing runtime mode-switch semantics.

Do not rename or remove an existing public field to make room for semantic facts.

Update the generated OpenAPI contract through the repository's existing contract generation path. Do not hand-edit generated JSON into a shape not produced by the Rust contract authority.

## Implementation structure constraints

Prefer one shared backend semantic-facts construction path used by Dashboard and market health.

A reasonable implementation may introduce leased-module structs/enums/helpers such as semantic health facts, measurement unit/comparison and primary-issue selection. Names inside Rust may differ where needed for idiomatic code, but serialized fields and semantics must remain unambiguous and covered by OpenAPI/serialization tests.

Do not move existing detector or domain code into the lease merely for convenience.

## Focused tests

At minimum add/extend focused tests for:

### Configuration

- delayed default;
- zero/equal/greater-than-stale validation boundaries;
- no stale-threshold default regression;
- health status threshold validation still works.

### Scoring/semantic helpers

- deterministic primary issue precedence across penalty, severity, event time, anomaly type and reason ties;
- no-primary-issue case;
- unit/comparison mapping for every currently supported anomaly family;
- `exceeded_by` arithmetic including negative price move and exact threshold equality;
- missing observed/threshold behavior;
- scoring/status results otherwise unchanged.

### DTO/API contract

- Dashboard health semantic serialization;
- market-health semantic serialization;
- exact source/mode/symbol identity;
- evaluated-at preservation;
- degraded/unhealthy threshold facts;
- Data Age thresholds;
- primary issue and measurement facts;
- OpenAPI required/nullable shape matches serialization.

### Demo

- deterministic repeated Demo summary output under fixed settings;
- changed injected delayed/stale/status settings are reflected in new semantic facts;
- source/mode/symbol identity remains Demo and exact;
- no Live fallback or endpoint identity change.

### Live/handler

- existing Live source/symbol identity remains exact;
- settings passed by handlers are the authoritative values used in semantic facts;
- no endpoint-path behavior changes.

## Required validation profile

Execute `V-BACKEND-CONTRACT` from the authoritative ledger.

### Focused Rust validation

Run focused tests for the changed config/scoring/API/contract modules first.

Then run at repository root:

```bash
cargo fmt --all -- --check
cargo run --quiet --bin export-api-contract -- --check
cargo run --quiet --bin export-api-contract -- --validate
cargo check
cargo clippy --workspace --all-targets --all-features -- -D warnings
cargo test --workspace --all-targets --all-features
cargo test --test replay_e2e
docker compose config
docker compose --profile app config
bash -n scripts/demo-replay.sh
bash -n scripts/smoke.sh
git diff --check
```

Declared service-dependent ignored tests may remain ignored exactly as designed. Do not convert failures into ignores.

### Full frontend regression validation

Although the frontend has no write lease, API/OpenAPI changes must not break it.

From `web/` run:

```bash
node --test scripts/check-bundle-size.test.mjs
npm run test:run
npm run typecheck
npm run lint
npm run build
npm run bundle:check
```

Require:

- bundle-policy 25/25;
- no frontend test-file count regression from 44;
- no frontend test-count regression from 615;
- zero failures;
- typecheck pass;
- lint with zero warnings;
- production build pass;
- unchanged bundle budgets `409600 / 409600 / 414720`.

A frontend failure caused by the additive contract change is a Bridge01 blocker. Do not fix frontend code under this lease; Bridge02 remains separately sequenced.

## Exact-path and one-commit audit

Before completion prove:

- worker branch direct base is exactly `23656c9b93a24bfc20ba8f417275564bb5b5d240`;
- branch is exactly one commit ahead and zero behind that base;
- merge base is exact base;
- changed files are a subset of, and only justified members of, the exact writable lease;
- no `web/` path changed;
- no detector path changed;
- no dependency/lockfile/budget drift;
- worktree is clean after commit;
- no generated residue remains outside the intentionally committed OpenAPI artifact.

## Browser evidence

No browser screenshot acceptance is required for Bridge01 because this is a backend/API-contract bridge with no frontend write lease.

Do not use this absence of screenshot work to skip the full frontend regression gates.

## Connector implementation report

On complete success publish exactly:

`signalguard-rs/phase-3/reports/P3-W4-BRIDGE01/<WORKER_COMMIT_SHA>.md`

Connector commit message:

`docs(phase-3): publish W4 Bridge01 implementation`

The report must include:

- implementation contract publication commit/blob/status;
- exact base SHA/tree and target no-drift proof;
- worker branch/commit/tree/message/direct parent;
- exact changed-path list and per-file statistics;
- exact semantic API result, including serialized field names/enums actually implemented;
- delayed/stale configuration invariant and tests;
- health threshold facts;
- evaluated-at preservation;
- deterministic primary-issue algorithm and tests;
- unit/comparison/exceeded-by mapping and arithmetic tests;
- source/mode/symbol identity proof;
- Dashboard/market-health consistency proof;
- Demo determinism/runtime-setting alignment proof;
- OpenAPI generation/check/validation result;
- focused Rust tests and full Rust/global gates;
- full frontend regression results and counts;
- bundle results and unchanged limits;
- exact branch relation and clean-worktree evidence;
- confirmation of zero frontend writes, zero detector writes, no PR and no merge;
- confirmation Bridge02 and Wave 4 UI work did not begin.

Do not update `CURRENT_EXECUTION.md` or `STATUS.md` from the implementation worker.

## Blocker handling

On identity drift, necessary out-of-lease change, semantic ambiguity that cannot be resolved within the contract, deterministic gate failure or report-publication failure:

- do not broaden the lease;
- do not fix frontend or detector code;
- do not create a PR;
- preserve evidence;
- publish a blocker report only if current connector authority permits it;
- return the blocker marker.

## Continuation boundary

A successful implementation is not independently accepted and is not integrated.

After implementation success the only next permitted orchestration step is a separate independent GitHub-web Bridge01 implementation review, followed by a separate GitHub-web integration worker if accepted.

Bridge02 remains blocked until Bridge01 is reviewed, integrated and accepted.

Do not begin P3-MP21…P3-MP30 before both bridges are integrated.

## Terminal markers

On complete success return exactly:

`P3_W4_BRIDGE01_COMPLETE`

On blocker return exactly:

`P3_W4_BRIDGE01_BLOCKED_BY_SCOPE_OR_IDENTITY`
