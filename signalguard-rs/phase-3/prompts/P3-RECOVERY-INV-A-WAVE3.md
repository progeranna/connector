# P3-RECOVERY-INV-A — Wave 3 modal-only closure inventory

Status: `P3_RECOVERY_INV_A_AUTHORIZED`

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

Inventory only Wave 3 modal ownership and the proposed `P3-MP18R` / `P3-MP20R` closure.

Trace:

- Dashboard modal state/controller;
- Symbol Detail resource identity;
- Symbol Detail anomaly desktop/mobile activation;
- Anomaly Detail UUID resolution;
- return context and focus restoration;
- Demo/Live and symbol-switch stale-state handling;
- obsolete route/popup formatting variants;
- dead SymbolPopup return contexts;
- all directly relevant tests and smoke scenarios.

## Required findings

Produce a structured terminal report containing:

1. exact current behaviour and defects;
2. exact files and symbols involved;
3. whether Symbol Detail anomalies can resolve by UUID from their own resource without storing a stale full object;
4. proposed identity/controller model;
5. exact proposed writable lease for `P3-MP18R`;
6. exact proposed writable lease for `P3-MP20R`;
7. non-overlap boundary between the two tasks;
8. focused tests and browser matrix;
9. forbidden adjacent paths;
10. any blocker that requires API changes.

Do not implement anything.

Return exactly one terminal marker:

- `P3_RECOVERY_INV_A_COMPLETE`
- `P3_RECOVERY_INV_A_BLOCKED_BY_IDENTITY_DRIFT`
- `P3_RECOVERY_INV_A_BLOCKED_BY_MISSING_EVIDENCE`
