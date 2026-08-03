# SignalGuard RS — Authoritative Control Status

Current state: `P3_ROADMAP_RESUMED_WAVE3_CLOSURE_AUDIT_AUTHORIZED_PHASE4_BLOCKED`

Updated: 2026-08-03

## Read this first

This file is the current entrypoint for every future orchestrator, worker, reviewer, and continuation chat.

Authority order:

1. this file;
2. `signalguard-rs/phase-3/control/RESUMPTION_PLAN.md`;
3. `signalguard-rs/phase-3/control/MICRO_PHASE_LEDGER.md`;
4. `signalguard-rs/phase-3/control/EXECUTION_PLAN.md`, except where the resumption plan records an explicit product-owner override;
5. immutable implementation, integration, review, and checkpoint reports.

When an older Phase 3, Phase 3.5, Phase 3.6, Phase 4, project-rule, architecture, testing, or handoff document conflicts with the authority order above, the newer authority wins only for the exact conflicting requirement. Unrelated invariants remain binding.

## Exact product identity

- Product repository: `progeranna/signalguard-rs`
- Active product branch: `refactor/dashboard-modules`
- Current integrated product SHA: `ba31a348dc5055935c45f6be81073688caedd925`
- Current integrated product tree: `f629b6ea4339c92d03223c3bd8024cd4cb4571da`
- Integration source: Phase 3.6 modal-only correction, PR `#68`

Identity drift is a blocker. No worker may silently use a newer base.

## Restored roadmap

The active roadmap is the original 47-micro-phase Phase 3 plan:

`P3-MP00` through `P3-MP46` in `signalguard-rs/phase-3/control/EXECUTION_PLAN.md`.

The project does not proceed to a new product Phase 4 until the remaining Phase 3 work is completed, explicitly superseded by a reviewed replan, and closed by `P3-MP46` with final user-visible localhost review.

Required order:

1. close remaining modal-only Wave 3 gaps;
2. establish the semantic data bridge required for truthful UI status and tooltip facts;
3. implement the agreed late Phase 3 Wave 4 semantics, indicators, and tooltips (`P3-MP21` through `P3-MP30`);
4. complete dialogs and accessibility (`P3-MP31` through `P3-MP35`);
5. complete re-planned routing, loading, error isolation, and performance work (`P3-MP36` through `P3-MP41`);
6. complete responsive and accessibility hardening and final smoke (`P3-MP42` through `P3-MP46`);
7. only then plan the next product Phase 4.

## Binding modal-only product-owner override

The following rules supersede every historical requirement for standalone visual symbol or anomaly pages:

- `/` and `/dashboard` are the only user-facing visual console pages.
- `/symbols/:symbol` and `/anomalies` are compatibility-only replacement redirects to `/dashboard`.
- Market activation opens Dashboard-owned Symbol Detail.
- Anomaly activation opens Dashboard-owned Anomaly Detail by exact anomaly UUID.
- `View all anomalies` opens Dashboard-owned All Anomalies.
- All Anomalies rows open exact Anomaly Detail; Back restores All Anomalies and exact row focus.
- Modal state remains ephemeral local UI state; do not restore standalone detail pages or route-synchronized modal state.

This override changes route-specific portions of the old roadmap. It does not cancel the agreed Wave 4 visual semantics, dialog accessibility, error handling, bundle, responsive, or user-review work.

## Agreed Wave 4 is priority scope

The following visible vocabulary remains binding:

- `System Healthy`, `System Degraded`, `System Critical`, `System Offline`, `System Unknown`;
- `Market Healthy`, `Market Degraded`, `Market Critical`, `Market Stale`, `Market No Data`;
- `Warning · Spread Spike`, `Critical · Price Move`, `Info · Stale Data`, `No Active Anomalies`;
- `Data Age`, with `Fresh`, `Delayed`, `Stale`, and `No Data`;
- public modes remain `Demo Mode` and `Live Mode` only.

The upper ticker remains forbidden scope unless the product owner separately authorizes a change.

## Current authorization

Authorized now:

- parallel read-only GitHub web inventories for the remaining Wave 3, Wave 4, and Wave 5–7 ownership and conflict boundaries;
- connector-only synthesis and exact implementation-contract preparation;
- no product mutation during those inventories.

Not authorized now:

- Phase 4 anomaly-explorer planning or implementation;
- any implementation based on `signalguard-rs/phase-4/prompts/P4-PLANNING-INVENTORY.md`;
- restoring standalone visual symbol or anomaly pages;
- beginning `P3-MP21` before the Wave 3 closure and semantic-bridge contracts are reviewed;
- product changes without a separate immutable implementation contract.

## Superseded transition

The earlier transition from Phase 3.6 directly to Phase 4 planning was an authority-drift error.

`signalguard-rs/phase-4/prompts/P4-PLANNING-INVENTORY.md` is retained as immutable historical evidence but is `SUPERSEDED_UNEXECUTED`. It must not be run.

## Next action

Run the three authorized parallel read-only inventories described in the resumption plan. After their reports are independently reviewed, publish exact implementation contracts for:

1. `P3-MP18R` — exact Anomaly Detail activation from Symbol Detail;
2. `P3-MP20R` — removal of obsolete route/anomaly-to-symbol presentation residue;
3. semantic bridge contracts required before `P3-MP21` through `P3-MP30`.
