# SignalGuard RS Phase 3.5 — Status

Current state: `WAVE_0_AUDITS_IN_PROGRESS`

## Authoritative product baseline

- Product repository: `progeranna/signalguard-rs`
- Phase branch: `refactor/dashboard-modules`
- Immutable Phase 3.5 base: `c06082a97254bfa2f6ebd7e29a1ad753c4acc798`
- Checkpoint 2 CI: `30548108769` — success
- Frontend baseline: 42 test files, 607 tests, 761856 raw JS bytes, 220163 gzip JS bytes, 761856-byte budget, 0-byte headroom

## Phase plan

- Plan: `signalguard-rs/phase-3.5/PLAN.md`
- Phase 4 remains blocked until Checkpoint 3.5.

## Wave 0 audit status

### P3.5-MP00A — Bundle composition and dependency-graph audit

Status: `ACCEPTED_STATIC_GRAPH`

- Worker class: GitHub web worker
- Product SHA audited: `c06082a97254bfa2f6ebd7e29a1ad753c4acc798`
- Report: `signalguard-rs/phase-3.5/inventory/P3.5-MP00A-WEB/c06082a97254bfa2f6ebd7e29a1ad753c4acc798.md`
- Report commit: `3ba9dc726de4f9e46048ef2b0236ffc74bd2a77e`
- Production files inspected: 51
- Accepted findings: 14
- Independent Orchestrator review: pass

Accepted static conclusions:

1. `/`, `/dashboard`, `/symbols/:symbol`, and `/anomalies` all enter the initial static dependency graph.
2. No route-level or chart-level dynamic import boundary exists.
3. Recharts is statically reachable through `index.html -> main.tsx -> App.tsx -> router.tsx -> DashboardPage.tsx -> TimelinePanel.tsx -> recharts`.
4. Conditional chart JSX does not provide code splitting.
5. `/anomalies` is directly eager; `/symbols/:symbol` is indirectly eager through `CanonicalSymbolRoute -> SymbolDetailPage`.
6. Route splitting alone does not defer Recharts within `/dashboard`; a separate Timeline/chart boundary is required.
7. The existing bundle checker counts all emitted JavaScript toward total JS, including lazy chunks, so splitting may reduce largest or initial JS without reducing total JS.

Accepted local experiment order for Wave 3 preflight:

1. fine-grained Timeline/Recharts renderer boundary;
2. lazy `/anomalies`;
3. lazy `/symbols/:symbol`.

MP00A-WEB does not prove emitted chunk composition, Recharts byte contribution, raw/gzip savings, tree-shaking effectiveness, or prototype correctness. Those measurements are deferred to isolated no-commit local experiments immediately before MP07/MP08 authorization. This limitation does not block Wave 1 semantic consolidation.

### P3.5-MP00B — Duplicate implementation audit

Status: `ACCEPTED`

- Product SHA audited: `c06082a97254bfa2f6ebd7e29a1ad753c4acc798`
- Report: `signalguard-rs/phase-3.5/inventory/P3.5-MP00B/c06082a97254bfa2f6ebd7e29a1ad753c4acc798.md`
- Report commit: `c115742575c2f47808473fe2f2c8a378e5d2f26d`
- Accepted findings: 13
- Priority A / B / C: 2 / 6 / 5
- Rejected similarities: 8
- Independent Orchestrator review: pass

Accepted leading candidates:

1. P3.5-MP01 — exact desktop/mobile HealthScore consolidation.
2. P3.5-MP02 — Timeline reuse of `marketHealthPresentation.ts`.
3. P3.5-MP03 — Dashboard anomaly modal reuse of `recentAnomaliesPresentation.ts` under an exclusive Dashboard lease.

MP00B recommendations are not implementation authorization. Final path leases remain blocked by the MP00 consolidation gate.

### P3.5-MP00C — Dead code, exports, dependencies, and cycles audit

Status: `NOT_STARTED`

Preferred worker: GitHub web worker.

### P3.5-MP00D — Test-guard maintainability audit

Status: `ACCEPTED`

- Product SHA audited: `c06082a97254bfa2f6ebd7e29a1ad753c4acc798`
- Report: `signalguard-rs/phase-3.5/inventory/P3.5-MP00D/c06082a97254bfa2f6ebd7e29a1ad753c4acc798.md`
- Report commit: `73408022752cc63dc77aeff7c897ad1c6a1dd889`
- Frontend test files inspected: 42
- Guard findings: 47
- KEEP_EXACT: 17
- KEEP_BUT_NARROW: 18
- REPLACE_WITH_BEHAVIOR: 8
- REPLACE_WITH_TYPE_OR_API_CONTRACT: 1
- REMOVE_REDUNDANT: 3
- INVESTIGATE: 0
- Independent Orchestrator review: pass

Accepted conclusions:

1. Exact visual-parity guards from PR #56 remain exact.
2. Resource identity, Demo/Live separation, ticker ownership, row/card identity, mutation/order, forbidden dependency ownership, accessibility, callbacks, and state-matrix guards must remain strong.
3. Exact import counts, internal function names, exact JSX composition strings, helper-location assumptions, and unqualified whole-source word/method bans are legitimate modernization targets.
4. P3.5-MP06A and P3.5-MP06B may run in parallel only after final leases are published, with `DashboardPage.test.tsx` exclusive to MP06A and `DashboardPage.popup.test.tsx` exclusive to MP06B.
5. MP06A/MP06B remain test-only; all production and configuration paths are forbidden.

MP00D recommendations are not implementation authorization. MP06A and MP06B remain blocked until Wave 2 reaches their dependency gate and the Orchestrator publishes final exact path leases.

## Current authorization

Authorized:

- read-only Wave 0 audits only;
- publication of one report per assigned inventory path in `progeranna/connector`.

Not authorized:

- product branches;
- product commits;
- product pull requests;
- Wave 1 implementation;
- MP06A or MP06B implementation;
- bundle-budget changes;
- Phase 4 work;
- merges.

## Remaining Wave 0 work

1. P3.5-MP00C-WEB — dead code, exports, dependencies, and cycles audit.

## Deferred measured bundle work

The MP00A static graph is accepted. No emitted-byte or split-prototype result has been measured. Before Wave 3 implementation, the Orchestrator must require isolated no-commit local experiments for the accepted Timeline/Recharts and route boundaries, with full build, bundle, test, typecheck, lint, deep-link, loading-state, and query-identity evidence.

## Next gate

After MP00C-WEB is complete and independently reviewed, the Orchestrator must publish the consolidated MP00 inventory with:

- accepted findings from MP00A–D;
- rejected false positives;
- exact Wave 1 path leases;
- the accepted Checkpoint 2 measured bundle baseline;
- qualitative expected reduction ranges for Wave 1;
- high-conflict reservations;
- deferred Wave 3 measurement obligations;
- final authorization or rejection of MP01, MP02, and MP03.
