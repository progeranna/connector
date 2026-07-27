# SignalGuard RS Phase 3 — Status

Current state: `READY_FOR_P3_MP00`

## Authoritative inputs

Authoritative execution plan:

`signalguard-rs/phase-3/control/EXECUTION_PLAN.md`

Plan creation commit:

`8787f58d0d7b9fc64e8678af83ac2933bcf44b5b`

Final Phase 2 / authoritative starting `main` SHA:

`6b57938d87e05d3b4fa4858f9c34c27739877821`

Phase 2 final merge record:

`signalguard-rs/phase-2/integration/PHASE-2/6b57938d87e05d3b4fa4858f9c34c27739877821.md`

Phase 2-to-main PR:

`https://github.com/progeranna/signalguard-rs/pull/23`

Exact-head CI run:

`30286016632` — success.

## Product branch

Phase 3 branch:

`refactor/dashboard-modules`

Initial branch SHA:

`6b57938d87e05d3b4fa4858f9c34c27739877821`

The branch was created directly from the final merged Phase 2 main SHA and currently contains no Phase 3 product commits.

## Phase structure

Phase 3 consists of 47 small micro-phases arranged into seven execution waves, with parallel workers permitted only when path ownership and dependencies do not overlap.

Required preview model:

- stable accepted preview: `worktrees/p3-preview`, branch `refactor/dashboard-modules`, port `5173`;
- candidate comparison preview: `worktrees/p3-candidate-preview`, temporary candidate checkout, port `5174`.

Visible changes require:

`CODE_ACCEPTED → INTEGRATED_TO_PREVIEW → USER_UI_ACCEPTED`

## Binding invariants

- the upper ticker is not modified;
- dashboard composition is not redesigned;
- existing public routes remain;
- Demo and Live remain the only public modes;
- strict Phase 2 Demo/Live and symbol identity isolation remains;
- popup and symbol route both remain;
- desktop tables and mobile cards remain;
- extraction, wiring, semantic copy, tooltip content, accessibility migration, route splitting, and styling are separate tasks;
- workers do not merge their own PRs;
- no Phase 3 task may repeat Phase 2 data-boundary work.

## Wave 0

### P3-MP00 — Post-Phase-2 route, component and visual inventory

Purpose:

- verify the exact starting SHA;
- inventory current routes, page/component boundaries, dialogs, source files, tests, visual surfaces, responsive variants, and high-conflict paths;
- finalize exact path leases for the first worker wave;
- make no product presentation change.

### P3-MP01 — Reusable local UI smoke matrix

Codify Demo/Live, BTC/ETH, route/popup, responsive, loading/error/empty/unavailable/success, and rapid-switch test coverage without changing production presentation.

### P3-MP02 — Tooltip primitive foundation

Create one accessible tooltip primitive with no caller migrations.

### P3-MP03 — Pure status vocabulary and descriptor model

Create typed pure descriptors for system status, market status, anomaly severity/detector display, data-age classification, tooltip facts, and time semantics. No JSX wiring.

### P3-MP04 — Deterministic semantic fixtures

Follow P3-MP03 with stable fixtures for all descriptor states.

Parallelism:

- P3-MP01, P3-MP02, and P3-MP03 may run together after P3-MP00 publishes non-overlapping exact path leases;
- P3-MP04 follows P3-MP03.

Checkpoint 0 requires the stable localhost preview to remain visually identical to the final Phase 2 UI.

## Next action

Execute P3-MP00 as a read-only inventory/control task from exact SHA `6b57938d87e05d3b4fa4858f9c34c27739877821`, publish the exact starting inventory and Wave 0 path leases, then create the dedicated worker branches and contracts for P3-MP01 through P3-MP03.

No user-visible Phase 3 code change is authorized before P3-MP00 is accepted.

Only the Orchestrator updates this file.
