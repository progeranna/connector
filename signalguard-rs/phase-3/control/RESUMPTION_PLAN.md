# SignalGuard RS Phase 3 — Authoritative Resumption Plan

Status: `P3_RESUMPTION_BASELINE_ACTIVE`

## 1. Authority

This file is the mandatory entry point for every future SignalGuard RS orchestrator and worker after 2026-08-03.

The authoritative product base is:

- repository: `progeranna/signalguard-rs`
- phase branch: `refactor/dashboard-modules`
- product SHA: `ba31a348dc5055935c45f6be81073688caedd925`
- product tree: `f629b6ea4339c92d03223c3bd8024cd4cb4571da`

The original 47-mini-phase roadmap remains authoritative:

`signalguard-rs/phase-3/control/EXECUTION_PLAN.md`

This resumption plan does not replace that roadmap. It records the current execution point, product-owner overrides and the safe continuation sequence.

## 2. Binding product-owner overrides

The following decisions supersede every older requirement for standalone symbol or anomaly visual pages:

1. `/` and `/dashboard` are the only visual console pages.
2. `/symbols/:symbol` and `/anomalies` are compatibility replacement redirects to `/dashboard`.
3. Activating a market opens Symbol Detail as a Dashboard-owned modal.
4. Activating an anomaly opens Anomaly Detail by exact anomaly UUID.
5. `View all anomalies` opens All Anomalies modal.
6. All Anomalies rows open Anomaly Detail, not Symbol Detail.
7. Modal state is ephemeral local UI state; URL-synchronised modal state and modal deep links are forbidden.
8. The backend `/anomalies` endpoint remains valid and is not affected by visual-route removal.

These overrides alter only route/popup ownership. They do not cancel semantic Wave 4, dialogs/accessibility, performance or responsive work.

## 3. Rejected direction

The connector contract:

`signalguard-rs/phase-4/prompts/P4-PLANNING-INVENTORY.md`

is superseded by this resumption baseline and MUST NOT be executed. A new product Phase 4 remains blocked until `P3-MP46` is accepted.

## 4. Reconstructed execution state

### Complete or accepted foundation

- `P3-MP00` through `P3-MP17`: complete.
- `P3-MP19`: standalone-route objective superseded by modal-only decision.
- `P3-MP20`: shared Symbol Detail sections integrated for popup use, but requires closure work listed below.
- Phase 3.5 native SVG/bundle work: complete and integrated.
- Phase 3.6 modal-only correction: complete and integrated at the authoritative product base.

### Wave 3 closure still required

#### `P3-MP18R — Exact anomaly detail from Symbol Detail`

Current defect: Symbol Detail anomaly presentation still contains inactive desktop rows and mobile activation that opens Symbol Detail instead of Anomaly Detail.

Required result:

- desktop and mobile anomaly rows activate exact UUID;
- Anomaly Detail resolves from the correct active mode/symbol resource;
- Back restores Symbol Detail and exact row/card focus;
- mode/symbol changes cannot retain stale anomaly detail;
- no anomaly activation opens Symbol Detail.

#### `P3-MP20R — Remove obsolete route presentation residue`

Required cleanup:

- remove `MarketDisplayVariants.route` and route-only anomaly formatters;
- remove dead route/popup-parity concepts;
- remove obsolete SymbolPopup anomaly return context where no longer reachable;
- retain Dashboard → Symbol Detail, All Markets → Symbol Detail and Symbol Detail → Anomaly Detail.

#### Checkpoint 2R

Required manual matrix:

- Demo and Live;
- BTCUSDT and ETHUSDT;
- Dashboard → Symbol Detail;
- Symbol Detail anomaly → Anomaly Detail → Back;
- All Anomalies → Anomaly Detail → Back;
- desktop and approximately 390px mobile;
- keyboard, Escape, focus containment and focus return;
- no red console errors.

## 5. Semantic bridge before Wave 4 presentation

Wave 4 semantic descriptors and fixtures already exist, but several presentation decisions lack authoritative runtime facts.

### `P3-W4-BRIDGE01 — Expose semantic health facts`

Plan an additive API contract for the facts needed by Wave 4, including:

- current data age;
- delayed and stale thresholds sourced from backend configuration;
- evaluated time;
- primary health issue;
- existing penalty/observed/threshold facts;
- exact source/mode/symbol identity;
- deterministic Demo values and isolated Live values.

Frontend hardcoded detector thresholds are forbidden.

### `P3-W4-BRIDGE02 — Frontend semantic adapters`

Required result:

- Zod schemas preserve required semantic facts;
- pure adapters own System, Market, Data Age and tooltip semantics;
- source/mode/symbol identity is verified;
- JSX does not independently reimplement status classification.

## 6. Agreed late Phase 3 Wave 4

This is a mandatory product objective and must not be replaced by anomaly-explorer work.

### Wave 4A

- `P3-MP21`: System status indicator — `System Healthy`, `System Degraded`, `System Critical`, `System Offline`, `System Unknown`.
- `P3-MP22`: chart anomaly indicator — combined severity and detector label, plus `No Active Anomalies`.
- `P3-MP23`: Data Age — `Fresh`, `Delayed`, `Stale`, `No Data`, with age, thresholds and last event.
- `P3-MP24`: Market Health vocabulary — `Market Healthy`, `Market Degraded`, `Market Critical`, `Market Stale`, `Market No Data`.
- `P3-MP25`: Recent Anomalies severity semantics and concise explanation.

### Wave 4B

- `P3-MP26`: selected-market status and facts.
- `P3-MP27`: unified Demo/Live explanation.
- `P3-MP28`: health-score explanation and facts.
- `P3-MP29`: observed/threshold/exceeded-by explanation.
- `P3-MP30`: unified tooltip audit.

Checkpoint 3 requires product-owner visual review before later waves.

## 7. Later continuation

### Dialogs/accessibility

- `P3-MP31`: shared Dialog primitive.
- `P3-MP31A`: modal decomposition to create non-overlapping ownership.
- `P3-MP32`: Symbol Detail migration.
- `P3-MP33`: All Markets migration.
- `P3-MP34`: All Anomalies and Anomaly Detail migration.
- `P3-MP35`: complete keyboard/focus matrix.

### Routing/loading/performance

- `P3-MP36`: explicit 404 while preserving compatibility redirects.
- `P3-MP37`: Dashboard/modal error boundaries.
- `P3-MP38`: measured feature-level lazy loading; standalone page splitting is not permitted.
- `P3-MP39`: closed as superseded by accepted native SVG chart implementation.
- `P3-MP40`: Suspense/lazy failure fallback when justified by MP38.
- `P3-MP41`: final bundle measurement under unchanged budgets.

### Responsive/final

- `P3-MP42`: selector keyboard navigation.
- `P3-MP43`: reduced-motion support outside protected ticker ownership.
- `P3-MP44`: timeline responsive regression.
- `P3-MP45`: health/anomaly responsive regression.
- `P3-MP46`: final modal-only desktop/mobile smoke and Phase 3 checkpoint.

## 8. Required order

```text
current integrated product ba31a348…
→ roadmap recovery inventory and synthesis
→ P3-MP18R / P3-MP20R
→ Checkpoint 2R
→ P3-W4-BRIDGE01 / P3-W4-BRIDGE02
→ P3-MP21–P3-MP30
→ Checkpoint 3
→ P3-MP31–P3-MP35
→ P3-MP36–P3-MP41
→ P3-MP42–P3-MP46
→ only then authorize a new product Phase 4
```

## 9. Execution model

The next action is parallel read-only GitHub inventory by four non-overlapping workers, followed by one synthesis worker.

- Inventory workers may not modify product or connector repositories.
- Only the synthesis worker may publish the final ledger and implementation leases.
- No implementation branch is authorised by this file.
- Every later implementation mini-phase requires a separate immutable contract, exact base, exact writable lease, one product commit, CI and independent integration.

Terminal state:

`P3_ROADMAP_RECOVERY_INVENTORY_AUTHORIZED_IMPLEMENTATION_BLOCKED`
