# SignalGuard RS Phase 2 — Control Plan

## Scope

Phase 2 establishes explicit data ownership and request isolation across the web console and Redis cache boundaries.

Product repository:

`progeranna/signalguard-rs`

Control repository:

`progeranna/connector`

Phase 1 base:

`5e15a06169445461a9003e17fa1ae5a648d5a1a1`

Phase branch:

`refactor/data-boundaries`

Current verified phase SHA:

`ce2ee582a370cce8bf8198d1fbb82fcb961867c3`

## Approved dependency lanes

### Frontend lane

1. `P2-MP01` — query-key factories — `INTEGRATED`.
2. `P2-MP02` — dedicated symbol-owned frontend queries — released from the integrated MP01 phase SHA.
3. Post-MP02 inspection determines the exact release shape for:
   - `P2-MP03` — market DTO to view-model adapters;
   - `P2-MP04` — validated API contract publication and drift checks.

P2-MP03 and P2-MP04 may run in parallel only if the Orchestrator proves non-overlapping path leases after MP02. Otherwise run P2-MP04 before P2-MP03.

### Backend cache lane

1. `P2-MP05` — atomic Redis latest-state registration — rejected head under repair as `P2-MP05-R1`.
2. `P2-MP06` — bounded bulk Redis state reads — remains blocked until MP05 is accepted and integrated.

### Cross-lane task

`P2-MP07` — explicit source and data-availability semantics — starts only after P2-MP03 and P2-MP04 are integrated and the relevant backend boundaries are stable.

## Current parallel execution

At most two product workers may be active:

- frontend worker: `P2-MP02` on `p2/mp02-symbol-data-queries`;
- backend worker: `P2-MP05-R1` on `p2/mp05-atomic-redis-state`.

Their primary path ownership is disjoint:

- P2-MP02: frontend under `web/src/**`;
- P2-MP05-R1: formatting-only repair of `src/storage/redis.rs` plus connector proof/report artifacts authorized by its repair contract.

Neither worker may read from, merge, rebase onto, cherry-pick from, or modify the other task branch.

## Git topology

Integrated branch state:

- `refactor/data-boundaries` at `ce2ee582a370cce8bf8198d1fbb82fcb961867c3`.

Active task branches:

- `p2/mp02-symbol-data-queries`, created exactly from `ce2ee582a370cce8bf8198d1fbb82fcb961867c3`;
- `p2/mp05-atomic-redis-state`, continuing only under the immutable P2-MP05-R1 repair contract.

Workers:

- push only to their assigned task branch;
- create only the commits authorized by their immutable contract;
- open or continue a PR into `refactor/data-boundaries`;
- never merge the PR;
- never write directly to `main` or the phase branch;
- never force-push, amend, or rewrite history without an explicit repair contract.

## Delivery model

Each implementation worker must:

1. read its immutable contract from a specific `connector` commit SHA;
2. implement code in `signalguard-rs`;
3. push the exact task commit;
4. open or continue a PR into `refactor/data-boundaries`;
5. write a delivery report to:

   `signalguard-rs/phase-2/reports/<MP-ID>/<PRODUCT-HEAD-SHA>.md`

6. return the product commit SHA, PR URL, connector report path, connector report commit SHA, and gate summary.

No ZIP handoff is part of the normal workflow.

## Validation model

The Orchestrator independently verifies:

- immutable contract commit;
- task branch and exact base SHA;
- product head SHA;
- changed-file inventory and complete patch;
- path and semantic scope;
- architecture and product invariants;
- tests and reported command output;
- actual CI state for the reviewed SHA;
- PR base and mergeability;
- connector report accuracy;
- repository hygiene.

Possible decisions:

- `ACCEPT`
- `ACCEPT_WITH_NOTES`
- `REJECT`

`ACCEPT_WITH_NOTES` cannot waive a correctness, isolation, atomicity, security, or data-integrity defect.

## Repair model

For a rejected delivery, the Orchestrator writes an immutable repair contract under:

`signalguard-rs/phase-2/repairs/<MP-ID>-R<N>.md`

The repair targets the existing task branch unless explicitly replaced.

A later task in the same dependency lane is not released while its prerequisite remains unresolved. Independent tasks in another lane may run when their own prerequisites are satisfied and path leases are disjoint.

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

## Final audit

After P2-MP07:

- inspect the complete `main...refactor/data-boundaries` diff;
- verify commit boundaries and repository hygiene;
- run complete frontend and Rust gates;
- run real Redis, PostgreSQL, Replay, runtime, and contract-drift checks;
- verify route and popup parity;
- verify Demo/Live and BTC/ETH isolation;
- perform consolidated local and visual QA;
- open the final Phase 2 PR to `main` only after acceptance.

## Owner involvement

The owner is not expected to move archives, patches, or reports manually.

The owner:

- approves phase decomposition;
- launches workers with short connector pointers;
- may run one consolidated local Codex audit after integration;
- performs visual localhost QA where applicable;
- explicitly approves the final Phase 2 merge to `main`.
