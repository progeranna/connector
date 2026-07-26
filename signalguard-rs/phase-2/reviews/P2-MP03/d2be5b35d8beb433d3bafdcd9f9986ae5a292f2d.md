# P2-MP03-R2 Review — d2be5b35d8beb433d3bafdcd9f9986ae5a292f2d

## Verdict

`REJECT — REPAIR_REQUIRED`

The clean replacement delivery is structurally much better than the superseded branch and passes exact-head CI, but it does not yet preserve the pre-MP03 presentation semantics required by the immutable contract.

## Reviewed product state

- repository: `progeranna/signalguard-rs`
- branch: `p2/mp03-market-view-models-r2`
- base: `1447a3ccb2fa3020738cd2dd3f8d145be6cd202a`
- reviewed head: `d2be5b35d8beb433d3bafdcd9f9986ae5a292f2d`
- PR: `https://github.com/progeranna/signalguard-rs/pull/19`
- PR base: `refactor/data-boundaries`
- commit count: exactly one
- commit message: `refactor(web): adapt market DTOs into view models`
- exact-head CI run: `30215490254` — success
- Rust job: success
- frontend job: success

## Scope validation

Exactly six authorized frontend paths changed:

- `web/src/features/dashboard/marketAdapters.test.ts`
- `web/src/features/dashboard/marketAdapters.ts`
- `web/src/features/dashboard/marketViewModel.ts`
- `web/src/pages/DashboardPage.tsx`
- `web/src/pages/SymbolDetailPage.test.tsx`
- `web/src/pages/SymbolDetailPage.tsx`

No backend, query-key, wire-schema, dependency, lockfile, tooling, or CI path changed.

## What is directionally correct

- explicit readonly market-detail view-model types exist;
- route and popup both call one adapter;
- canonical resource and anomaly symbol checks exist;
- Live/Demo resource ownership remains in the P2-MP02 resource boundary;
- full local frontend gates were reported green;
- exact-head product CI is green;
- `DashboardPage.tsx` changes are confined to imports and the existing symbol-detail popup path.

## Blocking findings

### 1. Route anomaly formatting changed instead of being preserved

Before MP03, the dedicated route rendered anomaly `observed_value` and `threshold_value` with the route-specific generic numeric formatter. For example, a spread value `2.5` rendered as `2.5`.

The new adapter creates only one popup-oriented anomaly representation:

- `spread_spike` and `price_move` become fixed three-decimal percentages;
- duration, burst, and depth-gap values receive popup-specific units.

`SymbolDetailPage` now renders those same popup-oriented strings. Therefore route output changes, for example:

- old route: `2.5`
- new route: `2.500%`

This violates the contract requirements that the task is not a visual redesign and that existing user-visible presentation semantics remain unchanged.

The shared view model may contain route/popup display variants, but both consumers must preserve their own existing rendered values.

### 2. Partial-state success shell is no longer preserved

Before MP03, the `Latest normalized state` section rendered its existing empty-state shell when `selectedSummary.state` was null.

The repaired implementation switches that condition to `marketViewModel`, which exists for any successful resource. A successful Demo resource may contain health data while state is null. In that case the route now renders a metric list instead of the previous empty-state message.

The adapter also computes:

`depthGaps: formatCount(state?.depth_sequence_gap_count ?? 0)`

This fabricates numeric zero when the whole state object is missing. The immutable contract explicitly requires missing values to remain unavailable and never become zero.

The view model must preserve explicit state availability so presentation can retain the existing shell. `depthGaps` must be unavailable when state is absent.

### 3. Consumer calls do not enforce requested identity

`adaptMarketResourceToViewModel` accepts an optional expected identity and tests that code path, but both production consumers call it without the expected route/popup identity.

The route must adapt against its current canonical `{mode, symbol}` request, and the popup must adapt against its current popup identity. This keeps the requested-identity guard active at the presentation boundary rather than only in a direct unit test.

### 4. Required connector delivery report is absent

The required report path does not exist in `progeranna/connector`:

`signalguard-rs/phase-2/reports/P2-MP03/d2be5b35d8beb433d3bafdcd9f9986ae5a292f2d.md`

The reported connector commit SHA was identical to the product commit SHA, but that SHA does not exist in the connector repository.

A new report must be created only after the repaired product head and repaired exact-head CI are final.

## Required repair outcome

- preserve one shared view-model contract;
- represent route/popup anomaly display variants where their existing formatting differs;
- restore the existing route partial-state empty shell;
- represent absent state metrics as unavailable, not zero;
- pass expected canonical identity from both production consumers;
- add executable regression tests for these behaviors;
- keep all user-visible strings, CSS classes, routes, queries, persistence, and backend contracts unchanged;
- create exactly one additional repair commit;
- keep PR #19 draft and unmerged;
- create a real connector delivery report after green repaired exact-head CI.
