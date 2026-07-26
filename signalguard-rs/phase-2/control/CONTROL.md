# SignalGuard RS Phase 2 — Control Plan

## Scope

Phase 2 establishes explicit data ownership and request isolation across the web console and Redis cache boundaries.

Product repository:

`progeranna/signalguard-rs`

Control repository:

`progeranna/connector`

Authoritative product base:

`5e15a06169445461a9003e17fa1ae5a648d5a1a1`

Phase branch:

`refactor/data-boundaries`

## Approved wave plan

### Wave 1

Run in parallel:

- `P2-MP01` — query-key factories;
- `P2-MP05` — atomic Redis latest-state registration.

Barrier:

Both tasks must be delivered, reviewed, accepted, and integrated before Wave 2 contracts are released.

Integration order:

1. P2-MP01
2. P2-MP05

### Wave 2

Run in parallel after Wave 1 barrier:

- `P2-MP02` — dedicated symbol-owned frontend queries;
- `P2-MP06` — bounded bulk Redis state reads.

### Wave 3

Candidate parallel tasks:

- `P2-MP03` — market DTO to view-model adapters;
- `P2-MP04` — validated API contract publication and drift checks.

The Orchestrator must inspect the post-Wave-2 tree before release. Run them in parallel only if their path leases are non-overlapping. Otherwise run `P2-MP04` before `P2-MP03`.

### Wave 4

- `P2-MP07` — explicit source and data-availability semantics.

Operational dependency:

P2-MP07 starts only after both P2-MP03 and P2-MP04 are integrated.

### Final audit

After P2-MP07:

- inspect the complete `main...refactor/data-boundaries` diff;
- verify commit boundaries and repository hygiene;
- run complete frontend and Rust gates;
- run real Redis, PostgreSQL, Replay, runtime, and contract-drift checks;
- verify route and popup parity;
- verify Demo/Live and BTC/ETH isolation;
- perform consolidated local and visual QA;
- open the final Phase 2 PR to `main` only after acceptance.

## Concurrency rule

At most two product workers may be active at once.

Parallel workers must have disjoint primary path ownership. No worker may edit another worker's branch, report, prompt, or review record.

## Git topology

Wave 1 branches:

- `p2/mp01-query-key-factories`
- `p2/mp05-atomic-redis-state`

Both branches must start from the exact authoritative base SHA.

Workers:

- push only to their assigned task branch;
- create one atomic Conventional Commit;
- open a PR into `refactor/data-boundaries`;
- never merge the PR;
- never write directly to `main` or the phase branch;
- never force-push.

## Delivery model

Each worker must:

1. read its immutable contract from a specific `connector` commit SHA;
2. implement code in `signalguard-rs`;
3. push the exact task commit;
4. open a PR into `refactor/data-boundaries`;
5. write a delivery report to:

   `signalguard-rs/phase-2/reports/<MP-ID>/<PRODUCT-HEAD-SHA>.md`

6. return the product commit SHA, PR URL, connector report path, and connector report commit SHA.

No ZIP handoff is part of the normal workflow.

## Validation model

The Orchestrator independently verifies:

- immutable contract commit;
- task branch and exact base SHA;
- product head SHA;
- changed-file inventory;
- complete patch;
- path and semantic scope;
- architecture and product invariants;
- test additions and reported command output;
- actual CI state for the reviewed SHA;
- PR base and mergeability;
- report accuracy;
- repository hygiene.

Possible decisions:

- `ACCEPT`
- `ACCEPT_WITH_NOTES`
- `REJECT`

`ACCEPT_WITH_NOTES` cannot be used to waive a correctness, isolation, atomicity, security, or data-integrity defect.

## Repair model

For a rejected delivery, the Orchestrator writes a repair contract under:

`signalguard-rs/phase-2/repairs/<MP-ID>-R<N>.md`

The repair must target the existing task branch unless the Orchestrator explicitly replaces it.

No later dependent mini-phase is released while the rejected task remains unresolved.

## Integration model

Only an accepted, unchanged product head SHA may be integrated.

Preferred integration is one squash merge per accepted mini-phase into `refactor/data-boundaries`.

Before integration, the Orchestrator rechecks that the PR head still equals the reviewed SHA.

After integration, the Orchestrator records:

- source task SHA;
- PR number;
- integration method;
- resulting phase-branch SHA;
- CI state;
- follow-up notes.

## Permanent product invariants

- SignalGuard RS remains a read-only market-data quality monitor.
- No order submission, cancellation, routing, account, wallet, private-key, credential, or PnL functionality.
- Demo data never fills a Live resource.
- Symbol A data never renders under symbol B.
- Query identity includes every parameter that determines the returned resource.
- Existing routes remain available.
- Symbol detail route and popup both remain supported.
- Phase 2 does not authorize a visual redesign.
- Product Git history contains no raw prompts, worker reports, handoff archives, or AI-process artifacts.

## Owner involvement

The owner is not expected to move archives, patches, or reports manually.

The owner:

- approves phase decomposition;
- launches workers with short connector pointers;
- may run one consolidated local Codex audit after integration;
- performs visual localhost QA where applicable;
- explicitly approves the final Phase 2 merge to `main`.
