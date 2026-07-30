# SignalGuard RS Phase 3.5 — Status

Current state: `WAVE_1_EXECUTION_AUTHORIZED`

## Authoritative product baseline

- Product repository: `progeranna/signalguard-rs`
- Phase branch: `refactor/dashboard-modules`
- Immutable Phase 3.5 base: `c06082a97254bfa2f6ebd7e29a1ad753c4acc798`
- Phase branch comparison at authorization: identical to base; ahead `0`, behind `0`
- Checkpoint 2 CI: `30548108769` — success
- Frontend baseline: 42 test files, 607 tests, 761856 raw JS bytes, 220163 gzip JS bytes, 761856-byte largest/total budget, 0-byte headroom

Phase 4 remains blocked until Checkpoint 3.5.

## Phase plan and consolidated inventory

- Plan: `signalguard-rs/phase-3.5/PLAN.md`
- Consolidated MP00 inventory: `signalguard-rs/phase-3.5/inventory/P3.5-MP00/c06082a97254bfa2f6ebd7e29a1ad753c4acc798.md`
- Consolidation commit: `ab703e4a0ed3062360f0550c5a68efaa0e9929e7`
- MP00 disposition: `P3_5_MP00_COMPLETE_WAVE_1_AUTHORIZED`

## Wave 0 audit status

### P3.5-MP00A-WEB — Bundle composition and dependency graph

Status: `ACCEPTED_STATIC_GRAPH`

- Report: `signalguard-rs/phase-3.5/inventory/P3.5-MP00A-WEB/c06082a97254bfa2f6ebd7e29a1ad753c4acc798.md`
- Commit: `3ba9dc726de4f9e46048ef2b0236ffc74bd2a77e`
- 51 production files inspected
- 14 accepted findings

Accepted:

- every current route is eager in the initial static graph;
- no route/chart dynamic import exists;
- Recharts is statically reachable through DashboardPage and TimelinePanel;
- conditional JSX is not code splitting;
- route splitting alone cannot defer Recharts inside `/dashboard`;
- local emitted-byte experiments are deferred to Wave 3 preflight.

### P3.5-MP00B — Duplicate implementation audit

Status: `ACCEPTED`

- Report: `signalguard-rs/phase-3.5/inventory/P3.5-MP00B/c06082a97254bfa2f6ebd7e29a1ad753c4acc798.md`
- Commit: `c115742575c2f47808473fe2f2c8a378e5d2f26d`
- Accepted findings: 13
- Priority A / B / C: 2 / 6 / 5
- Rejected similarities: 8

Accepted Wave 1 candidates:

1. desktop/mobile HealthScore consolidation;
2. Timeline reuse of market-health presentation helpers;
3. Dashboard anomaly modal reuse of canonical anomaly presentation helpers.

### P3.5-MP00C-WEB — Dead code, exports, dependencies, and cycles

Status: `ACCEPTED_WEB_INVENTORY`

- Report: `signalguard-rs/phase-3.5/inventory/P3.5-MP00C-WEB/c06082a97254bfa2f6ebd7e29a1ad753c4acc798.md`
- Commit: `5ffc52ca5ee5d3f25b27fb5ea96a4d23900145c1`
- 51 production files inspected
- 245 export bindings inventoried
- 3 confirmed findings, including 2 cleanup candidates
- 4 probable candidates
- 2 verification-required groups
- dependency deletion candidates: 0
- credible cycles: 0

Accepted sequencing decision:

- MP05 remains after MP04;
- MP00C must be refreshed against the integrated tree before any deletion;
- no dependency or lockfile change is currently justified.

### P3.5-MP00D — Test-guard maintainability audit

Status: `ACCEPTED`

- Report: `signalguard-rs/phase-3.5/inventory/P3.5-MP00D/c06082a97254bfa2f6ebd7e29a1ad753c4acc798.md`
- Commit: `73408022752cc63dc77aeff7c897ad1c6a1dd889`
- 42 test files inspected
- 47 guard findings
- KEEP_EXACT: 17
- KEEP_BUT_NARROW: 18
- REPLACE_WITH_BEHAVIOR: 8
- REPLACE_WITH_TYPE_OR_API_CONTRACT: 1
- REMOVE_REDUNDANT: 3
- INVESTIGATE: 0

MP06A/MP06B remain blocked until Wave 2.

## Authorized Wave 1 workers

All three workers start from exact SHA:

`c06082a97254bfa2f6ebd7e29a1ad753c4acc798`

They may implement concurrently because their leases do not overlap. Integration remains sequential.

### P3.5-MP01 — Health-score presentation

Status: `EXECUTION_AUTHORIZED`

- Worker class: GitHub web implementation worker
- Branch: `p35/mp01-health-score-presentation`
- Required commit: `refactor(ui): consolidate health score presentation`
- Writable: new `HealthScore.tsx` and focused test; MarketHealth desktop/mobile source and focused tests
- Forbidden: DashboardPage, Timeline, marketHealthPresentation, anomaly/symbol-detail modules, shared status, router/config/package/budget/backend
- Expected reduction: qualitative `medium`
- Production total JS may not increase

### P3.5-MP02 — Timeline presentation reuse

Status: `EXECUTION_AUTHORIZED`

- Worker class: GitHub web implementation worker
- Branch: `p35/mp02-timeline-presentation-reuse`
- Required commit: `refactor(ui): reuse market health presentation in timeline`
- Writable: TimelinePanel source/test; marketHealthPresentation source/test only for a proven minimal status-label contract
- Forbidden: DashboardPage, MarketHealth callers, anomaly/symbol-detail modules, adapters/view models/shared formatters, router/config/package/budget/backend
- No Recharts or lazy-boundary work
- Expected reduction: qualitative `medium`
- Production total JS may not increase

### P3.5-MP03 — Dashboard anomaly presentation

Status: `EXECUTION_AUTHORIZED_HIGH_CONFLICT`

- Worker class: GitHub web implementation worker
- Branch: `p35/mp03-dashboard-anomaly-presentation`
- Required commit: `refactor(ui): consolidate dashboard anomaly presentation`
- Exclusive writable paths: `DashboardPage.tsx`, `DashboardPage.test.tsx`, `recentAnomaliesPresentation.ts`, `recentAnomaliesPresentation.test.ts`
- No other worker may edit the Dashboard paths while MP03 is active
- Forbidden: MarketHealth callers, Timeline, marketHealthPresentation, adapters/view models, symbol-detail/shared/router/config/package/budget/backend
- Expected reduction: qualitative `medium`
- Production total JS may not increase

## Integration policy

Recommended order:

1. MP01;
2. MP02;
3. MP03.

For each candidate:

1. verify exact branch head and one logical commit;
2. inspect complete diff and path lease;
3. require focused tests;
4. require full frontend tests, typecheck, lint, build, and bundle check;
5. compare production JS against the candidate base;
6. create draft PR only after acceptance;
7. require merge-ref CI against the current phase branch;
8. merge with a normal merge commit only after independent review;
9. verify post-merge CI before integrating the next candidate.

Workers do not merge. Same-base branches are not rebased.

## Current authorization

Authorized:

- MP01, MP02, and MP03 implementation on their exact assigned branches and leases;
- independent worker reports;
- Orchestrator exact-head review and later PR creation.

Not authorized:

- worker merges;
- bundle-budget increase;
- MP04–MP09 implementation;
- MP06A/MP06B implementation;
- Phase 4;
- visual redesign, copy change, backend/API change, or ownership change outside exact leases.

## Next action

Launch MP01, MP02, and MP03 as three separate GitHub web workers from the exact immutable base. Do not share writable branches or leases.
