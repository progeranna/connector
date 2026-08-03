# P3-RECOVERY-SYNTHESIS — Authoritative roadmap recovery synthesis

Status: `P3_RECOVERY_SYNTHESIS_BLOCKED_PENDING_INVENTORIES`

## Mode

Dedicated synthesis worker. Use connected GitHub tools. Product repository is read-only. Connector writes are permitted only after all four inventory outputs are provided in the conversation and independently checked against the exact product base.

## Exact product base

- repository: `progeranna/signalguard-rs`
- ref/SHA: `ba31a348dc5055935c45f6be81073688caedd925`
- expected tree: `f629b6ea4339c92d03223c3bd8024cd4cb4571da`

## Required inputs

Complete terminal outputs from:

- `P3-RECOVERY-INV-A-WAVE3.md`
- `P3-RECOVERY-INV-B-WAVE4.md`
- `P3-RECOVERY-INV-C-DIALOGS.md`
- `P3-RECOVERY-INV-D-PERF-RESPONSIVE.md`

Do not synthesize from missing, blocked or identity-drifted inventories.

## Authority

Read completely:

- `signalguard-rs/phase-3/control/EXECUTION_PLAN.md`
- `signalguard-rs/phase-3/control/RESUMPTION_PLAN.md`
- `signalguard-rs/phase-3/control/STATUS.md`
- all four inventory contracts;
- all four worker outputs.

## Required synthesis

Publish an evidence-backed ledger for every `P3-MP00…P3-MP46` using only:

- `COMPLETE`;
- `PARTIALLY_COMPLETE`;
- `SUPERSEDED_BY_PRODUCT_OWNER`;
- `SUPERSEDED_BY_ACCEPTED_IMPLEMENTATION`;
- `NOT_STARTED`;
- `REQUIRES_REVALIDATION`.

For every non-complete item include:

- current evidence;
- exact remaining result;
- exact proposed writable lease;
- forbidden adjacent paths;
- dependencies;
- safe parallelisation group;
- required commit message;
- focused tests;
- full validation gates;
- browser/screenshot evidence;
- terminal status.

The synthesis must preserve this order:

1. `P3-MP18R` / `P3-MP20R`;
2. Checkpoint 2R;
3. semantic bridge;
4. `P3-MP21…P3-MP30` and Checkpoint 3;
5. `P3-MP31…P3-MP35`;
6. `P3-MP36…P3-MP41`;
7. `P3-MP42…P3-MP46`;
8. only then a new product Phase 4.

## Connector publication

Publish exactly:

- `signalguard-rs/phase-3/control/MICRO_PHASE_LEDGER.md`
- `signalguard-rs/phase-3/control/IMPLEMENTATION_SEQUENCE.md`
- updated `signalguard-rs/phase-3/control/STATUS.md`

Use one connector commit if the available connector tooling supports an atomic multi-file write; otherwise use the minimum sequential commits and record every commit identity in the final response.

The resulting status must be either:

- `P3_WAVE3_CLOSURE_IMPLEMENTATION_AUTHORIZED`, when leases are complete and non-conflicting;
- `P3_RECOVERY_BLOCKED_BY_UNRESOLVED_CONFLICT`, when they are not.

Do not create product branches, product commits or PRs. Do not authorise Wave 4 implementation before Wave 3 closure and Checkpoint 2R.

Return exactly one terminal marker:

- `P3_RECOVERY_SYNTHESIS_COMPLETE`
- `P3_RECOVERY_SYNTHESIS_BLOCKED_BY_INPUT`
- `P3_RECOVERY_SYNTHESIS_BLOCKED_BY_IDENTITY_DRIFT`
- `P3_RECOVERY_SYNTHESIS_BLOCKED_BY_UNRESOLVED_CONFLICT`
