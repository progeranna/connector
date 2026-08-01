# SignalGuard RS Phase 3.5 — Status

Current state: `WAVE_2_COMPLETE_WAVE_3_MEASUREMENT_AUTHORIZED`

## Authoritative product state

- Product repository: `progeranna/signalguard-rs`
- Phase branch: `refactor/dashboard-modules`
- Immutable Phase 3.5 starting SHA: `c06082a97254bfa2f6ebd7e29a1ad753c4acc798`
- Current integrated phase head: `9c8aed635e57272fc834c1ddcdbc3dbf33cf4328`
- Phase 4 remains blocked until Checkpoint 3.5.

The phase branch resolves exactly to the current integrated head.

## Quantitative state

Phase 3.5 starting baseline:

- frontend: 42 test files, 607 tests;
- production JS raw: `761856` bytes;
- production JS gzip: `220163` bytes;
- largest/total JS budget: `761856` bytes;
- headroom: `0` bytes.

Current integrated state after Wave 2:

- frontend: 43 test files, 640 tests;
- TypeScript: pass;
- lint: pass with zero warnings;
- production build: pass;
- transformed modules: `714`;
- bundle check: pass;
- raw JS: `757217` bytes;
- Vite gzip display: `219.99 kB`;
- largest/total budget: `761856` bytes, unchanged;
- headroom: `4639` bytes;
- cumulative raw reduction: `4639` bytes.

Phase 3.5 minimum target remains `8192` raw bytes of total-JS headroom. Remaining reduction required is `3553` bytes. Wave 3 is required.

## Wave 0

Status: `COMPLETE`

- Consolidated inventory: `signalguard-rs/phase-3.5/inventory/P3.5-MP00/c06082a97254bfa2f6ebd7e29a1ad753c4acc798.md`
- Consolidation commit: `ab703e4a0ed3062360f0550c5a68efaa0e9929e7`
- Terminal disposition: `P3_5_MP00_COMPLETE_WAVE_1_AUTHORIZED`

Accepted audits:

- MP00A-WEB: static route and Recharts dependency graph;
- MP00B: duplicate implementation inventory;
- MP00C-WEB: dead-code/export/dependency inventory;
- MP00D: test-guard maintainability inventory.

## Wave 1

Status: `INTEGRATED`

Integration order:

`MP01 -> MP02 -> MP03`

Final Wave 1 head:

`4b90a9fe9e4ddda9b0b9411857e5d8b2c3685c69`

Integration report:

`signalguard-rs/phase-3.5/reports/P3.5-WAVE1/4b90a9fe9e4ddda9b0b9411857e5d8b2c3685c69.md`

Terminal disposition:

`P3_5_WAVE_1_INTEGRATION_COMPLETE`

- MP01: PR `#57`, CI `30700589902`, merge `93cb115a02509cc92384dc1746c761e2c875c8eb`, raw JS `760751`.
- MP02: PR `#58`, CI `30700795882`, merge `0d032bd3082e3351227387a45a17fe06cd1c3a21`, raw JS `760148`.
- MP03: PR `#59`, CI `30700972480`, merge `4b90a9fe9e4ddda9b0b9411857e5d8b2c3685c69`, raw JS `758875`.

Each actual merge tree was identical to its exact green PR merge-ref tree.

## Wave 2

Status: `INTEGRATED`

### MP04 — Dashboard market-health consolidation

- Integration PR: `#60`
- Tested merge ref: `e893437a7b6ca812c5d9f534064e84cfc554a116`
- CI run: `30703462034` — success
- Merge commit: `0027679f7a5b2cc783098b1d4a625e1638bee67d`
- Frontend: 43 files, 629 tests
- Raw JS: `757217` bytes
- Integration report: `signalguard-rs/phase-3.5/reports/P3.5-MP04-INTEGRATION/0027679f7a5b2cc783098b1d4a625e1638bee67d.md`
- Terminal disposition: `P3_5_MP04_INTEGRATION_COMPLETE`

### MP00C-R1 — Refreshed cleanup audit

- Exact audited SHA: `0027679f7a5b2cc783098b1d4a625e1638bee67d`
- Report: `signalguard-rs/phase-3.5/inventory/P3.5-MP00C-R1/0027679f7a5b2cc783098b1d4a625e1638bee67d.md`
- Report commit: `ccdf3b81cc543a594876065240f82049226faa52`
- Package deletion candidates: none
- Credible cycles: none

### MP05 — Confirmed dead exports and declarations

- Integration PR: `#61`
- Tested merge ref: `dd651aa823f0073bbc83210c6e667aa3493dd12d`
- CI run: `30710872784` — success
- Merge commit: `21fec6d357b365a3710c8e7118a467564247dee6`
- Frontend: 43 files, 629 tests
- Raw JS: `757217` bytes
- Integration report: `signalguard-rs/phase-3.5/reports/P3.5-MP05-INTEGRATION/21fec6d357b365a3710c8e7118a467564247dee6.md`
- Terminal disposition: `P3_5_MP05_INTEGRATION_COMPLETE`

The accepted MP05 recovery retained `installControlledFetch` and `UiSmokeDialogRequirement` as exports after executable validation disproved modifier-only privatization.

### MP06A — Market-health and timeline test guards

- Worker head: `9d6d287515bc7f2122b30bda85e96c08fd07ae25`
- Integration PR: `#63`
- Tested merge ref: `002202c2b1bc5fe459795f9135e15ffa4a9449a1`
- CI run: `30712369103` — success
- Merge commit: `bb3df51339ad4a7a3524fe4782fdc24069944160`
- Frontend: 43 test files, 634 tests
- Raw JS: `757217` bytes
- Integration report: `signalguard-rs/phase-3.5/reports/P3.5-MP06A-INTEGRATION/bb3df51339ad4a7a3524fe4782fdc24069944160.md`
- Terminal disposition: `P3_5_MP06A_INTEGRATION_COMPLETE`

### MP06B — Anomaly and symbol-detail test guards

Original immutable worker:

- Worker branch: `p35/mp06b-symbol-detail-test-guards`
- Worker head: `0fbc488476a5b0efb657f88a06f26aa67c620c7c`
- Original shared base: `21fec6d357b365a3710c8e7118a467564247dee6`
- Worker report: `signalguard-rs/phase-3.5/reports/P3.5-MP06B/0fbc488476a5b0efb657f88a06f26aa67c620c7c.md`

Failed current-base validation:

- PR `#64` — closed without merge;
- tested merge ref: `e923defbeeeebf7cf6bf7457b77be28898286c82`;
- CI run: `30712501382`;
- Rust and all 640 frontend tests passed;
- TypeScript failed on six test-fixture/mock diagnostics;
- validation report: `signalguard-rs/phase-3.5/reports/P3.5-MP06B-VALIDATION/e923defbeeeebf7cf6bf7457b77be28898286c82.md`;
- terminal disposition: `P3_5_MP06B_BLOCKED_BY_CURRENT_BASE_TYPECHECK`.

Accepted recovery:

- Recovery contract: `signalguard-rs/phase-3.5/prompts/P3.5-MP06B-R1.md`
- Recovery branch: `p35/mp06b-r1-symbol-detail-test-guards`
- Recovery merge commit: `1893a0dc193b837a8be26274d00fcb6cf83401da`
- First parent: `bb3df51339ad4a7a3524fe4782fdc24069944160`
- Second parent: `0fbc488476a5b0efb657f88a06f26aa67c620c7c`
- Recovery report: `signalguard-rs/phase-3.5/reports/P3.5-MP06B-R1/1893a0dc193b837a8be26274d00fcb6cf83401da.md`
- Recovery report commit: `12d12b67d3ad96ae6faa19ffecd4b1799fc1371c`
- Integration PR: `#65`
- Tested merge ref: `162fcb9f497aaacfc794163ee4c429a5c44394b7`
- CI run: `30713464533` — success
- Frontend: 43 test files, 640 tests
- TypeScript/lint/build/bundle: pass
- Raw JS: `757217` bytes
- Merge commit and current phase head: `9c8aed635e57272fc834c1ddcdbc3dbf33cf4328`
- Tested merge-ref and actual merge trees: identical
- Integration report: `signalguard-rs/phase-3.5/reports/P3.5-MP06B-INTEGRATION/9c8aed635e57272fc834c1ddcdbc3dbf33cf4328.md`
- Integration report commit: `5b28956bd59a96c786b830071abfc155a75c6325`
- Terminal disposition: `P3_5_MP06B_INTEGRATION_COMPLETE`

The final MP06B diff contains exactly five leased test files. Three worker files remain byte-identical to the immutable worker. Only `DashboardPage.popup.test.tsx` and `SymbolDetailPage.test.tsx` contain the authorized TypeScript repairs. No production file changed.

## Wave 3

Status: `MEASUREMENT_AUTHORIZED_IMPLEMENTATION_BLOCKED`

Exact measurement base:

`9c8aed635e57272fc834c1ddcdbc3dbf33cf4328`

### MP07 — Route-level splitting experiment

Authorized only as a local, non-publishing measured experiment.

Required focus:

- lazy `/anomalies`;
- lazy `/symbols/:symbol` where contract-safe;
- deterministic loading boundary;
- direct deep links and navigation;
- initial JS and total JS before/after;
- full behavior and visual parity evidence.

Primary experiment paths:

- `web/src/app/router.tsx`;
- router/loading-boundary tests.

### MP08 — Timeline/Recharts boundary experiment

Authorized only as a local, non-publishing measured experiment.

Required focus:

- remove Recharts from the initial dependency graph where feasible;
- preserve timeline loading/error/empty/success states;
- preserve selected symbol and query ownership;
- prevent remount loops and duplicate requests;
- initial JS and total JS before/after;
- full behavior and visual parity evidence.

Primary experiment paths:

- `web/src/pages/DashboardPage.tsx`;
- `web/src/features/dashboard/TimelinePanel.tsx`;
- focused tests only as required by the experiment.

MP07 and MP08 experiments may run concurrently in isolated worktrees because their provisional primary paths do not overlap. No product branch, commit, push, PR, or production implementation is authorized until the Orchestrator reviews both measured reports and publishes exact implementation contracts/path leases.

### MP09 — Bundle policy refinement

Status: `BLOCKED_BY_MP07_MP08_INTEGRATION`

MP09 remains blocked until accepted MP07 and MP08 implementations are integrated. Any later policy change must retain total-JS non-regression and may lower, never raise, accepted limits.

## Phase 4

Status: `BLOCKED_BY_CHECKPOINT_3_5`

## Evidence boundary

For each accepted integration, the actual merge tree is directly compared with the exact green PR merge-ref tree. No merge is accepted when executable gates are skipped or failing.

The connected workflow lookup exposes pull-request-triggered runs. No separate push-run ID is claimed.

## Current authorization

Authorized:

- run MP07 and MP08 as isolated local measurement/prototype tasks against exact base `9c8aed635e57272fc834c1ddcdbc3dbf33cf4328`;
- use temporary uncommitted product changes only inside their dedicated worktrees;
- run full frontend, Rust, repository, and visual comparison gates needed to measure each prototype;
- publish measurement reports to the connector only after exact evidence review;
- update connector control files through the Orchestrator.

Not authorized:

- MP07 or MP08 product commit, branch publication, push, PR, or merge;
- MP09 implementation;
- Phase 4;
- bundle-budget increase;
- production feature, API, backend, generated-contract, product-copy, or visual changes;
- rebase, amend, reset, force-push, squash, or history rewrite;
- accepting initial-chunk reduction that increases total JS without explicit measured review;
- hiding regressions by moving code into async chunks.

## Next action

Publish exact local measurement contracts for MP07 and MP08 against:

`9c8aed635e57272fc834c1ddcdbc3dbf33cf4328`
