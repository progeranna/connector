# P3-MP20R — Integration contract

Status: `P3_MP20R_INTEGRATION_AUTHORIZED`

## 1. Worker mode

Dedicated GitHub web integration worker.

Use only connected GitHub tools.

Do not use a local checkout, shell, Codex CLI, GitHub CLI, filesystem repository copy, or unconnected repository data.

## 2. Authority

Read completely before any product write:

- `signalguard-rs/phase-3/control/EXECUTION_PLAN.md`
- `signalguard-rs/phase-3/control/RESUMPTION_PLAN.md`
- `signalguard-rs/phase-3/control/MICRO_PHASE_LEDGER.md`
- `signalguard-rs/phase-3/control/IMPLEMENTATION_SEQUENCE.md`
- `signalguard-rs/phase-3/control/STATUS.md`
- `signalguard-rs/phase-3/prompts/P3-MP20R-WEB.md`
- `signalguard-rs/phase-3/reports/P3-MP20R/1b09f69d79333872eeed47b00407b6ae09727822.md`
- `signalguard-rs/phase-3/reports/P3-MP20R-REVIEW/1b09f69d79333872eeed47b00407b6ae09727822.md`

Required review status:

`P3_MP20R_IMPLEMENTATION_ACCEPTED_FOR_INTEGRATION`

Review commit:

`79bfb5b37ea9ca3459e1fa5c9292cfd0d8a6d365`

Review blob:

`db93101c31a7737a9962b6d8be98548e4de52ab7`

## 3. Exact product identities

Product repository:

`progeranna/signalguard-rs`

Target branch:

`refactor/dashboard-modules`

Exact target base:

`6142ec7004b75cda077a49ab37bcfdca01f7f8e8`

Expected target base tree:

`65c816c76a5f9e31858cdcb29acd523e8a92c122`

Worker branch:

`p3/mp20r-route-presentation-residue`

Exact worker commit:

`1b09f69d79333872eeed47b00407b6ae09727822`

Expected worker tree:

`d8f9e71e7aec5fcf7b472011a68247a6df42bbac`

Exact worker commit message:

`refactor(ui): remove obsolete route presentation residue`

Before writing, verify:

- target branch resolves exactly to the target base and tree;
- worker branch resolves exactly to the worker commit and tree;
- worker commit has exactly one parent, the target base;
- worker branch is one commit ahead and zero behind;
- merge base is the exact target base;
- no PR already exists for this exact head/base combination.

Stop on any identity drift.

## 4. Exact accepted diff

The target-base-to-worker comparison must contain exactly these five modified files:

1. `web/src/features/dashboard/marketViewModel.ts`
2. `web/src/features/dashboard/marketAdapters.ts`
3. `web/src/features/dashboard/SymbolDetailAnomalies.tsx`
4. `web/src/features/dashboard/marketAdapters.test.ts`
5. `web/src/features/dashboard/SymbolDetailAnomalies.test.tsx`

Expected statistics:

- additions: 25
- deletions: 46
- changed files: 5

No added, deleted or renamed path is allowed.

Stop on scope drift.

## 5. Pull request

Create exactly one non-draft PR:

- base: `refactor/dashboard-modules`
- head: `p3/mp20r-route-presentation-residue`
- title: `refactor(ui): remove obsolete route presentation residue`

The PR body must state:

- exact immutable base and worker commit;
- exact five-file lease;
- this is a presentation-neutral data-shape refactor;
- local gates were not run by the web implementation worker;
- PR synthetic-merge CI is mandatory before merge;
- Checkpoint 2R and later phases remain blocked.

Do not edit the worker or target branches.

## 6. Synthetic merge-ref verification

After PR creation, resolve the GitHub synthetic merge commit and verify:

- ordered parent 1 is `6142ec7004b75cda077a49ab37bcfdca01f7f8e8`;
- ordered parent 2 is `1b09f69d79333872eeed47b00407b6ae09727822`;
- synthetic merge tree is exactly `d8f9e71e7aec5fcf7b472011a68247a6df42bbac`;
- target-base-to-synthetic effective diff is the exact five-file lease;
- worker-to-synthetic file diff is empty;
- no merge-only content drift exists.

Do not merge if the synthetic tree differs from the worker tree.

## 7. Required PR CI

Locate the CI workflow run for the exact PR synthetic merge ref.

Do not merge until the workflow is completed successfully and both jobs pass:

- `frontend`;
- `rust`.

Verify from job metadata, steps and logs that the exact synthetic merge SHA was checked out.

Required Frontend gates:

- dependency installation;
- full frontend Vitest suite;
- TypeScript typecheck;
- ESLint;
- production build;
- bundle-policy tests and budget check.

Required Rust/global gates:

- Rust formatting;
- generated API-contract check;
- OpenAPI validation;
- cargo check;
- Clippy with warnings denied;
- Cargo tests;
- replay E2E target/test;
- Docker Compose config;
- Docker Compose app-profile config;
- demo and smoke script syntax checks.

Record exact workflow run ID, job IDs, conclusions and tested merge SHA.

No CI rerun is allowed to hide a deterministic first failure. On failure, stop and publish the applicable blocker result without merging.

## 8. Merge

After exact identity and successful CI, merge the PR using normal merge commit only.

- merge method: `merge`;
- expected head SHA: `1b09f69d79333872eeed47b00407b6ae09727822`.

Do not squash, rebase, amend, force-push, or rewrite the worker commit.

After merge verify:

- PR is closed and merged;
- final target branch resolves to the merge commit;
- final merge commit has exactly two ordered parents;
- parent 1 is `6142ec7004b75cda077a49ab37bcfdca01f7f8e8`;
- parent 2 is `1b09f69d79333872eeed47b00407b6ae09727822`;
- final tree is exactly `d8f9e71e7aec5fcf7b472011a68247a6df42bbac`;
- old base to final target is two commits ahead and zero behind;
- effective old-base-to-final diff remains exactly the five accepted paths;
- synthetic merge tree and final merge tree are identical;
- worker branch remains unchanged.

## 9. Connector publication

Publish:

`signalguard-rs/phase-3/reports/P3-MP20R-INTEGRATION/<FINAL_MERGE_SHA>.md`

Update:

`signalguard-rs/phase-3/control/STATUS.md`

The final control state must be:

`P3_MP20R_INTEGRATED_CHECKPOINT_2R_NOT_AUTHORIZED`

Record:

- PR number, title, base/head and exact SHAs;
- synthetic merge SHA, tree and parents;
- workflow run ID;
- Frontend and Rust job IDs and conclusions;
- exact tested checkout SHA;
- final merge SHA, tree and ordered parents;
- exact five-file effective diff;
- target branch read-back;
- connector report/status commits and blobs;
- retained worker branch state;
- confirmation that Checkpoint 2R and later phases did not begin.

Read back and verify the integration report and updated status.

## 10. Authorization boundary

This worker may create the PR, verify CI, merge MP20R, publish the integration report and update status only.

It may not:

- begin Checkpoint 2R;
- authorize semantic Bridge 01 or Bridge 02;
- implement Wave 4;
- change any product file outside the accepted merge;
- restore standalone routes;
- change modal behavior, API/resource identity, Demo/Live isolation, ticker ownership, dependencies, lockfiles or bundle budgets;
- begin any later Phase 3 or product Phase 4 work.

## 11. Terminal result

Return exactly one:

- `P3_MP20R_INTEGRATION_COMPLETE`
- `P3_MP20R_INTEGRATION_BLOCKED_BY_IDENTITY_OR_SCOPE`
- `P3_MP20R_INTEGRATION_BLOCKED_BY_CI`
- `P3_MP20R_INTEGRATION_BLOCKED_BY_MERGE`
- `P3_MP20R_INTEGRATION_BLOCKED_BY_CONNECTOR_PUBLICATION`

Return success only after PR CI, normal merge, final identity verification and connector publication all succeed.
