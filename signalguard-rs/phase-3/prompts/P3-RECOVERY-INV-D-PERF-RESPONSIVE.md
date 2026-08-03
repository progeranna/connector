# P3-RECOVERY-INV-D — Routing, performance and responsive inventory

Status: `P3_RECOVERY_INV_D_AUTHORIZED`

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

Inventory `P3-MP36…P3-MP46` only.

Trace:

- current router and compatibility redirects;
- missing 404 and error-boundary ownership;
- viable feature/modal lazy-loading boundaries in a single-page visual architecture;
- current native SVG timeline and superseded Recharts split work;
- bundle budgets and emitted asset topology;
- selector keyboard semantics;
- reduced-motion support and protected ticker ownership;
- Timeline and health/anomaly responsive tests;
- UI smoke matrix and final manual checkpoint requirements.

## Required findings

Report:

1. exact reinterpretation of `P3-MP36…41` under modal-only routing;
2. whether feature-level lazy loading is justified by measured bundle evidence;
3. exact proposed leases for 404, error boundaries, lazy/Suspense and bundle measurement;
4. explicit closure status for superseded Recharts work;
5. exact remaining keyboard defects in selectors;
6. exact reduced-motion gaps without modifying protected ticker ownership unless separately authorised;
7. responsive regression gaps for 1440px and approximately 390px;
8. final `P3-MP46` browser/smoke matrix;
9. safe order and parallelisation boundaries;
10. all CI, bundle and screenshot gates.

Do not implement anything.

Return exactly one terminal marker:

- `P3_RECOVERY_INV_D_COMPLETE`
- `P3_RECOVERY_INV_D_BLOCKED_BY_IDENTITY_DRIFT`
- `P3_RECOVERY_INV_D_BLOCKED_BY_MISSING_EVIDENCE`
