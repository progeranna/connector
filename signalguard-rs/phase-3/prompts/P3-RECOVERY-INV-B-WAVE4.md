# P3-RECOVERY-INV-B — Wave 4 semantic and data-contract inventory

Status: `P3_RECOVERY_INV_B_AUTHORIZED`

## Mode

GitHub web inventory worker. Use only connected GitHub tools. Read-only for both product and connector repositories. Do not create branches, commits, PRs, reports or comments.

## Exact product base

- repository: `progeranna/signalguard-rs`
- ref/SHA: `ba31a348dc5055935c45f6be81073688caedd925`
- expected tree: `f629b6ea4339c92d03223c3bd8024cd4cb4571da`

## Authority

Read completely before inventory:

- `signalguard-rs/phase-3/control/EXECUTION_PLAN.md`
- `signalguard-rs/phase-3/control/RESUMPTION_PLAN.md`
- `signalguard-rs/phase-3/control/STATUS.md`

## Scope

Inventory the semantic bridge and agreed Wave 4 `P3-MP21…P3-MP30` only.

Trace:

- backend health/detector settings and runtime thresholds;
- Dashboard and market-health DTOs/OpenAPI;
- Demo fixtures and Live resource identity;
- frontend Zod schemas;
- `statusDescriptors` and fixtures;
- System indicator/header presentation;
- Timeline anomaly indicator and Data Age;
- Market Health desktop/mobile/modal presentation;
- Recent Anomalies presentation;
- selected-market, Demo/Live, health-score and observed/threshold tooltip inputs;
- shared Tooltip behaviour and tests.

## Required decisions

Report:

1. which `P3-MP21…30` models are already complete, partial or absent;
2. every mismatch between approved vocabulary and rendered UI;
3. exact missing runtime facts for `Market Stale`, Data Age and tooltips;
4. recommended additive API shape and source of each field;
5. deterministic Demo versus isolated Live semantics;
6. whether one or two bridge mini-phases are required;
7. exact proposed writable leases for bridge work and each Wave 4 mini-phase;
8. safe parallelisation groups and conflicting ownership;
9. focused tests, browser evidence and tooltip accessibility matrix;
10. bundle-risk analysis under current strict budgets;
11. forbidden hardcoded threshold or fallback behaviour.

Do not implement anything.

Return exactly one terminal marker:

- `P3_RECOVERY_INV_B_COMPLETE`
- `P3_RECOVERY_INV_B_BLOCKED_BY_IDENTITY_DRIFT`
- `P3_RECOVERY_INV_B_BLOCKED_BY_MISSING_EVIDENCE`
