# P3-RECOVERY-INV-C — Dialogs and accessibility inventory

Status: `P3_RECOVERY_INV_C_AUTHORIZED`

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

Inventory `P3-MP31…P3-MP35` only.

Trace:

- inline `DashboardTableModal` behaviour;
- focus containment, initial focus, focus return, Escape, backdrop and body scroll lock;
- Symbol Detail, All Markets, All Anomalies and Anomaly Detail overlays;
- nested/back navigation and exact return focus;
- ARIA labelling/descriptions;
- responsive hidden controls in focus queries;
- existing dialog tests and smoke requirements;
- current `DashboardPage.tsx` ownership/decomposition pressure.

## Required findings

Report:

1. which dialog behaviours are already functionally complete;
2. which behaviours are incomplete or fragile;
3. whether a shared primitive can be extracted without visual redesign;
4. exact proposed lease for `P3-MP31`;
5. whether `P3-MP31A` decomposition is required before parallel migrations;
6. exact non-overlapping leases for `P3-MP32`, `P3-MP33` and `P3-MP34`;
7. complete `P3-MP35` keyboard/focus matrix;
8. test and browser evidence required for each migration;
9. forbidden changes to modal-only route ownership and product semantics.

Do not implement anything.

Return exactly one terminal marker:

- `P3_RECOVERY_INV_C_COMPLETE`
- `P3_RECOVERY_INV_C_BLOCKED_BY_IDENTITY_DRIFT`
- `P3_RECOVERY_INV_C_BLOCKED_BY_MISSING_EVIDENCE`
