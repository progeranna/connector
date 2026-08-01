# SignalGuard RS Phase 3.5 — Status

Current state: `WAVE_3_MP08B_IMPLEMENTATION_AUTHORIZED`

## Authoritative product state

- Product repository: `progeranna/signalguard-rs`
- Phase branch: `refactor/dashboard-modules`
- Immutable Phase 3.5 starting SHA: `c06082a97254bfa2f6ebd7e29a1ad753c4acc798`
- Current integrated phase head: `9c8aed635e57272fc834c1ddcdbc3dbf33cf4328`
- Phase 4 remains blocked until Checkpoint 3.5.

The phase branch resolves exactly to the current integrated phase head.

## Quantitative state

Phase 3.5 starting baseline:

- frontend: `42` test files, `607` tests;
- production JS raw: `761856` bytes;
- production JS gzip: `220163` bytes;
- largest/total JS budget: `761856` bytes;
- headroom: `0` bytes.

Current integrated state after Wave 2:

- frontend: `43` test files, `640` tests;
- TypeScript: pass;
- lint: pass with zero warnings;
- production build: pass;
- transformed modules: `714`;
- raw JS: `757217` bytes;
- direct gzip: `219504` bytes;
- largest/total budget: `761856` bytes, unchanged;
- headroom: `4639` bytes;
- cumulative raw reduction: `4639` bytes.

The Phase 3.5 minimum target is `8192` raw bytes of total-JS headroom. The current integrated tree remains `3553` bytes short until an accepted Wave 3 implementation is merged.

## Wave 0

Status: `COMPLETE`

- Consolidated inventory: `signalguard-rs/phase-3.5/inventory/P3.5-MP00/c06082a97254bfa2f6ebd7e29a1ad753c4acc798.md`
- Consolidation commit: `ab703e4a0ed3062360f0550c5a68efaa0e9929e7`
- Terminal disposition: `P3_5_MP00_COMPLETE_WAVE_1_AUTHORIZED`

Accepted audits covered the static route/Recharts graph, duplicate implementations, dead exports/dependencies, and brittle test guards.

## Wave 1

Status: `INTEGRATED`

Integration order: `MP01 -> MP02 -> MP03`

- MP01 merge: `93cb115a02509cc92384dc1746c761e2c875c8eb`, PR `#57`, CI `30700589902`, raw JS `760751`.
- MP02 merge: `0d032bd3082e3351227387a45a17fe06cd1c3a21`, PR `#58`, CI `30700795882`, raw JS `760148`.
- MP03 merge and final Wave 1 head: `4b90a9fe9e4ddda9b0b9411857e5d8b2c3685c69`, PR `#59`, CI `30700972480`, raw JS `758875`.

Integration report:

`signalguard-rs/phase-3.5/reports/P3.5-WAVE1/4b90a9fe9e4ddda9b0b9411857e5d8b2c3685c69.md`

Each accepted actual merge tree was identical to its exact green PR merge-ref tree.

## Wave 2

Status: `INTEGRATED`

### MP04 — Dashboard market-health consolidation

- PR `#60`
- CI `30703462034`
- Merge `0027679f7a5b2cc783098b1d4a625e1638bee67d`
- Frontend `43/629`
- Raw JS `757217`
- Terminal disposition `P3_5_MP04_INTEGRATION_COMPLETE`

### MP05 — Confirmed dead exports and declarations

- PR `#61`
- CI `30710872784`
- Merge `21fec6d357b365a3710c8e7118a467564247dee6`
- Frontend `43/629`
- Raw JS `757217`
- Terminal disposition `P3_5_MP05_INTEGRATION_COMPLETE`

The accepted MP05 recovery retained `installControlledFetch` and `UiSmokeDialogRequirement` as exports after executable validation disproved modifier-only privatization.

### MP06A — Market-health and timeline test guards

- Worker `9d6d287515bc7f2122b30bda85e96c08fd07ae25`
- PR `#63`
- CI `30712369103`
- Merge `bb3df51339ad4a7a3524fe4782fdc24069944160`
- Frontend `43/634`
- Raw JS `757217`
- Terminal disposition `P3_5_MP06A_INTEGRATION_COMPLETE`

### MP06B — Anomaly and symbol-detail test guards

- Immutable worker `0fbc488476a5b0efb657f88a06f26aa67c620c7c`
- Failed validation PR `#64`, CI `30712501382`, closed without merge after current-base TypeScript failure
- Recovery merge `1893a0dc193b837a8be26274d00fcb6cf83401da`
- Integration PR `#65`
- CI `30713464533`
- Final Wave 2 merge and current integrated head `9c8aed635e57272fc834c1ddcdbc3dbf33cf4328`
- Frontend `43/640`
- Raw JS `757217`
- Terminal disposition `P3_5_MP06B_INTEGRATION_COMPLETE`

For every accepted Wave 2 integration, the actual merge tree was identical to its exact green PR merge-ref tree.

## Wave 3

Exact measurement and implementation base:

`9c8aed635e57272fc834c1ddcdbc3dbf33cf4328`

### MP07 — Route-level splitting

Status: `MEASUREMENT_ACCEPTED_NO_IMPLEMENTATION`

- Measurement contract: `signalguard-rs/phase-3.5/prompts/P3.5-MP07-MEASURE.md`
- Measurement report: `signalguard-rs/phase-3.5/inventory/P3.5-MP07-MEASURE/9c8aed635e57272fc834c1ddcdbc3dbf33cf4328.md`
- Report commit: `0d730ba71db664969c16b3524514b8f9d7430ff7`
- Review: `signalguard-rs/phase-3.5/reports/P3.5-MP07-MEASUREMENT-REVIEW/9c8aed635e57272fc834c1ddcdbc3dbf33cf4328.md`
- Review commit: `a17784563d7ab28fb5918e19bdca283418d53e52`
- Best initial prototype: R3 combined route boundaries
- R3 initial raw: `752364` bytes
- R3 total raw: `758842` bytes
- Total delta: `+1625` bytes
- Terminal disposition: `P3_5_MP07_MEASUREMENT_ACCEPTED_NO_ROUTE_IMPLEMENTATION`

All measured route splits improved initial cost but increased total JS. No MP07 implementation is authorized.

### MP08 — Lazy Timeline/Recharts boundary

Status: `MEASUREMENT_ACCEPTED_NO_IMPLEMENTATION`

- Measurement contract: `signalguard-rs/phase-3.5/prompts/P3.5-MP08-MEASURE.md`
- Measurement report: `signalguard-rs/phase-3.5/inventory/P3.5-MP08-MEASURE/9c8aed635e57272fc834c1ddcdbc3dbf33cf4328.md`
- Report commit: `169da4aa959f41963d4b401b5718b8ec986927e0`
- Review: `signalguard-rs/phase-3.5/reports/P3.5-MP08-MEASUREMENT-REVIEW/9c8aed635e57272fc834c1ddcdbc3dbf33cf4328.md`
- Review commit: `976824a3e8c4e08f608457f898e884dd5f4b865a`
- Preferred architecture: C2 lazy `TimelineChartRenderer` with normalized API
- C2 initial raw: `390828` bytes
- C2 total raw: `758069` bytes
- Total delta: `+852` bytes
- Terminal disposition: `P3_5_MP08_MEASUREMENT_ACCEPTED_NOT_IMPLEMENTATION_AUTHORIZED`

C2 remains the preferred ownership boundary for any renderer extraction, but lazy Recharts splitting is not authorized because it increases total JS.

### MP08B — Recharts-free native SVG Timeline

Status: `IMPLEMENTATION_AUTHORIZED`

Measurement:

- Contract: `signalguard-rs/phase-3.5/prompts/P3.5-MP08B-MEASURE.md`
- Contract commit: `0958b9a73fdabf6e6fa37f88e7ac93ac0028347c`
- Report: `signalguard-rs/phase-3.5/inventory/P3.5-MP08B-MEASURE/9c8aed635e57272fc834c1ddcdbc3dbf33cf4328.md`
- Report commit: `1e6d9f37aa61b11f6c5c40169af44aa5d21820a0`
- Accepted candidate: S2 native SVG renderer plus pure geometry helper
- Measured frontend: `44` files, `643` tests
- Measured raw JS: `395624` bytes
- Measured direct gzip: `113042` bytes
- Measured raw reduction: `361593` bytes
- Measured headroom: `366232` bytes
- Recharts and measured transitive production graph: absent
- Frontend, Rust, Docker Compose, script, browser, and screenshot-comparison gates: passed with recorded limitations and bounded visual differences

Measurement review:

- Review: `signalguard-rs/phase-3.5/reports/P3.5-MP08B-MEASUREMENT-REVIEW/9c8aed635e57272fc834c1ddcdbc3dbf33cf4328.md`
- Review commit: `94906eb77fc14aca68d55726fc4218657f1b6d82`
- Terminal disposition: `P3_5_MP08B_MEASUREMENT_ACCEPTED_IMPLEMENTATION_AUTHORIZED`

Implementation authorization:

- Contract: `signalguard-rs/phase-3.5/prompts/P3.5-MP08B.md`
- Contract commit: `be72d7cac8115de5387ce8899aa4f134a3189c9b`
- Worker class: local Codex implementation worker
- Required skill: `$rust-development`
- Assigned branch: `p35/mp08b-native-svg-timeline`
- Required single commit: `refactor(ui): replace Recharts timeline with native SVG`
- Exact writable lease: ten renderer/helper/test/package paths defined in the contract
- Product PR and merge: forbidden to worker

The accepted bounded visual differences are a straight polyline instead of Recharts monotone interpolation, slight native-SVG tick-position differences, and CSS-sized labels for mobile readability. No other visual or product change is authorized.

### MP09 — Bundle policy refinement

Status: `BLOCKED_BY_MP08B_INTEGRATION`

MP09 may start only after MP08B is independently reviewed, validated on an exact current-base PR merge ref, merged, and tree-verified. MP09 may distinguish initial and total metrics and lower limits; it may not raise limits or weaken total-JS protection.

## Phase 4

Status: `BLOCKED_BY_CHECKPOINT_3_5`

## Evidence boundary

For every accepted integration, the Orchestrator requires exact current-base PR merge-ref CI and directly compares the tested merge-ref tree with the actual normal merge tree. No merge is accepted when a required executable, browser, visual, lease, or bundle gate is skipped or failing.

The connected workflow lookup exposes pull-request-triggered runs. No separate push-run ID is claimed without direct evidence.

## Current authorization

Authorized:

- execute only `P3.5-MP08B` as a local Codex implementation worker against exact base `9c8aed635e57272fc834c1ddcdbc3dbf33cf4328`;
- create and push exactly one product commit on `p35/mp08b-native-svg-timeline`;
- modify only the ten exact leased paths;
- remove `recharts` and its unused lockfile graph;
- implement the accepted S2 native SVG renderer and pure geometry helper;
- run every required frontend, repository, browser/runtime, screenshot, bundle, dependency, diff, and lease gate;
- publish and verify the required connector implementation report.

Not authorized:

- MP07 route-splitting implementation;
- MP08 lazy-Recharts implementation;
- MP08B worker PR or merge;
- edits outside the exact MP08B lease;
- `DashboardPage.tsx`, router, API, backend, generated-contract, bundle-budget, CI, product-copy, route, popup, or Phase 4 changes;
- any new chart/runtime dependency;
- bundle-budget increase or weakened gate;
- rebase, amend, reset, squash, force-push, or history rewrite;
- MP09 before MP08B integration;
- Phase 4 before Checkpoint 3.5.

## Next action

Execute:

`signalguard-rs/phase-3.5/prompts/P3.5-MP08B.md`
