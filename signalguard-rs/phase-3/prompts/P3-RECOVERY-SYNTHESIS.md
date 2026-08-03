# P3-RECOVERY-SYNTHESIS — Authoritative roadmap recovery synthesis

Status: `P3_RECOVERY_SYNTHESIS_AUTHORIZED`

## Mode

Dedicated synthesis worker. Use connected GitHub tools only.

The product repository is read-only. Connector writes are permitted only for the exact synthesis outputs below.

Do not use a local checkout, shell, Codex CLI or an unconnected repository copy.

## Exact product base

- repository: `progeranna/signalguard-rs`
- ref/SHA: `ba31a348dc5055935c45f6be81073688caedd925`
- expected tree: `f629b6ea4339c92d03223c3bd8024cd4cb4571da`
- phase branch: `refactor/dashboard-modules`

Verify that the phase branch still resolves to the exact SHA and tree before synthesis. Stop on drift.

## Accepted inventory evidence

All four inventories have been supplied, reviewed and reconciled by the orchestrator.

Read completely:

`signalguard-rs/phase-3/reports/P3-RECOVERY-INVENTORIES/ba31a348dc5055935c45f6be81073688caedd925.md`

This report is the authoritative synthesis input and records:

- acceptance of A after independent tree-evidence completion;
- complete B, C and D results;
- resolved lease collisions;
- required continuation order;
- exact proposed leases and reinterpretations.

Do not require the user to paste the four worker outputs again.

## Authority

Read completely:

- `signalguard-rs/phase-3/control/EXECUTION_PLAN.md`
- `signalguard-rs/phase-3/control/RESUMPTION_PLAN.md`
- `signalguard-rs/phase-3/control/STATUS.md`
- all four inventory contracts;
- the consolidated inventory evidence report.

The original 47-mini-phase roadmap remains authoritative except for the explicit modal-only product-owner overrides in `RESUMPTION_PLAN.md`.

## Required synthesis

Publish an evidence-backed ledger for every `P3-MP00…P3-MP46` using only:

- `COMPLETE`;
- `PARTIALLY_COMPLETE`;
- `SUPERSEDED_BY_PRODUCT_OWNER`;
- `SUPERSEDED_BY_ACCEPTED_IMPLEMENTATION`;
- `NOT_STARTED`;
- `REQUIRES_REVALIDATION`.

The ledger may define recovery/bridge subphases such as `P3-MP18R`, `P3-MP20R`, `P3-W4-BRIDGE01`, `P3-W4-BRIDGE02`, `P3-MP31A`, `P3-MP37A` and `P3-MP37B`, but it must retain traceability to the original `P3-MP00…P3-MP46` roadmap.

For every non-complete item include:

- current evidence;
- exact remaining result;
- exact proposed writable lease;
- forbidden adjacent paths;
- dependencies;
- safe parallelisation group;
- required branch name;
- required Conventional Commit message;
- focused tests;
- full validation gates;
- browser/screenshot evidence;
- success and blocker terminal statuses.

## Required sequencing decisions

Preserve this order:

1. `P3-MP18R`;
2. `P3-MP20R` on the accepted MP18R head;
3. Checkpoint 2R;
4. `P3-W4-BRIDGE01`;
5. `P3-W4-BRIDGE02`;
6. semantic Wave 4 `P3-MP21…P3-MP30` and Checkpoint 3;
7. Dialog primitive `P3-MP31`;
8. structural decomposition `P3-MP31A`;
9. modal migrations `P3-MP32…P3-MP34` and integrated `P3-MP35`;
10. routing/loading/performance `P3-MP36…P3-MP41`;
11. responsive/final `P3-MP42…P3-MP46`;
12. only then a new product Phase 4.

Resolve ownership using the consolidated evidence:

- MP18R owns controller/UI interaction cleanup.
- MP20R owns pure route-presentation residue cleanup.
- Bridge 02 may sequentially reopen the resulting model/adapter paths.
- Wave 4 uses the accepted G2–G7 grouped schedule.
- MP31A is mandatory before parallel MP32–MP34.
- modal-boundary and lazy-loading leases must be expressed against the post-decomposition tree.
- MP39 is superseded by the accepted native-SVG implementation and receives no implementation contract.
- MP43 must not alter ticker behavior.

## Authorization boundary

This synthesis may authorize only the first implementation step:

`P3-MP18R — exact anomaly detail from Symbol Detail`

It may also record the already-planned subsequent MP20R lease, but MP20R implementation remains blocked until MP18R is accepted and integrated.

Do not authorize semantic bridge, Wave 4, dialogs, routing/performance or responsive implementation yet.

## Connector publication

Publish exactly:

- `signalguard-rs/phase-3/control/MICRO_PHASE_LEDGER.md`
- `signalguard-rs/phase-3/control/IMPLEMENTATION_SEQUENCE.md`
- updated `signalguard-rs/phase-3/control/STATUS.md`

Use one connector commit if the tool supports an atomic multi-file write. Otherwise use the minimum sequential commits and record every commit identity.

The resulting status must be either:

- `P3_MP18R_IMPLEMENTATION_AUTHORIZED`, when the first lease is exact and non-conflicting;
- `P3_RECOVERY_BLOCKED_BY_UNRESOLVED_CONFLICT`, when it is not.

Do not create product branches, product commits or PRs.

## Terminal result

Return exactly one:

- `P3_RECOVERY_SYNTHESIS_COMPLETE`
- `P3_RECOVERY_SYNTHESIS_BLOCKED_BY_INPUT`
- `P3_RECOVERY_SYNTHESIS_BLOCKED_BY_IDENTITY_DRIFT`
- `P3_RECOVERY_SYNTHESIS_BLOCKED_BY_UNRESOLVED_CONFLICT`
