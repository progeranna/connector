# P3-CHECKPOINT-2R-R1 — Integration contract

Status: `P3_CHECKPOINT_2R_R1_INTEGRATION_AUTHORIZED`

## Mode

Dedicated GitHub web integration worker.

Use only connected GitHub tools. No local checkout, shell, Codex CLI, GitHub CLI or unconnected repository copy.

## Required authority

Read completely:

- `signalguard-rs/phase-3/control/CURRENT_EXECUTION.md`
- `signalguard-rs/phase-3/control/STATUS.md`
- `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-R1-WEB.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R1/f793b8447076a9feb8227447c2b851622475ef7c.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R1-REVIEW/f793b8447076a9feb8227447c2b851622475ef7c.md`

The independent review must have status:

`P3_CHECKPOINT_2R_R1_ACCEPTED_FOR_INTEGRATION`

## Exact product identities

Repository: `progeranna/signalguard-rs`

Target branch: `refactor/dashboard-modules`

Exact target base:

`8bbef01d7d9979c4996954171a0e7c3748f02538`

Expected target tree:

`d8f9e71e7aec5fcf7b472011a68247a6df42bbac`

Worker branch:

`p3/checkpoint2r-view-all-reachability`

Exact worker commit:

`f793b8447076a9feb8227447c2b851622475ef7c`

Expected worker tree:

`9bdfdcf331ef08cdeaf8f21a8ab66adee3092fe8`

Expected worker message:

`fix(ui): keep dashboard modal entry points reachable`

Before any write verify:

- target branch remains exact base/tree;
- worker branch remains exact worker commit/tree;
- worker commit has exactly one parent, the exact target base;
- worker is one commit ahead and zero behind;
- merge base is exact target base;
- no existing PR owns this exact head/base pair.

Stop on any drift.

## Exact accepted diff

The base-to-worker comparison must contain exactly these three modified paths:

1. `web/src/pages/DashboardPage.tsx`
2. `web/src/pages/DashboardPage.test.tsx`
3. `web/src/pages/DashboardPage.popup.test.tsx`

Expected aggregate statistics:

- 3 modified files;
- 98 additions;
- 13 deletions;
- no added, deleted or renamed files.

Do not integrate any different diff.

## PR

Create exactly one non-draft PR:

- base: `refactor/dashboard-modules`
- head: `p3/checkpoint2r-view-all-reachability`
- title: `fix(ui): keep dashboard modal entry points reachable`

Do not modify either product branch before CI.

## Synthetic merge verification

Read the PR synthetic merge ref and verify:

- ordered parent 1 is exact target base;
- ordered parent 2 is exact worker commit;
- synthetic tree equals expected worker tree `9bdfdcf331ef08cdeaf8f21a8ab66adee3092fe8`;
- base-to-synthetic effective diff is exactly the accepted three-file lease;
- worker-to-synthetic file diff is empty;
- no merge-only content drift exists.

## Required PR CI

Locate the CI workflow run for the exact PR synthetic merge ref.

Do not merge until both jobs complete successfully:

- `frontend`
- `rust`

Verify from job metadata/steps/logs that the exact synthetic merge SHA was checked out.

Frontend must pass the repository workflow including:

- full Vitest suite;
- TypeScript typecheck;
- lint with zero warnings;
- production build;
- bundle policy and budget checks.

Rust/global job must pass the repository workflow including:

- formatting;
- generated API contract check;
- OpenAPI validation;
- cargo check;
- Clippy with warnings denied;
- Cargo tests;
- replay E2E target;
- Docker Compose config checks;
- demo/smoke shell syntax checks.

Do not use a rerun to hide a deterministic first failure. If CI fails, do not merge and return the blocker marker.

## Merge

After exact successful CI, merge by normal merge commit only.

Expected head SHA:

`f793b8447076a9feb8227447c2b851622475ef7c`

Do not squash, rebase, amend, force-push or rewrite the worker commit.

After merge verify:

- PR is closed and merged;
- final target branch resolves to the merge commit;
- final merge has exactly two ordered parents;
- parent 1 is `8bbef01d7d9979c4996954171a0e7c3748f02538`;
- parent 2 is `f793b8447076a9feb8227447c2b851622475ef7c`;
- final tree is `9bdfdcf331ef08cdeaf8f21a8ab66adee3092fe8`;
- old base to final target effective diff remains exactly the accepted three files;
- tested synthetic tree and final merge tree are identical;
- worker branch remains unchanged.

## Connector publication

Publish:

`signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R1-INTEGRATION/<FINAL_MERGE_SHA>.md`

Update:

- `signalguard-rs/phase-3/control/CURRENT_EXECUTION.md`
- `signalguard-rs/phase-3/control/STATUS.md`

Final state after successful integration:

`P3_CHECKPOINT_2R_R1_INTEGRATED_CHECKPOINT_RERUN_NOT_AUTHORIZED`

Record:

- PR number and metadata;
- synthetic merge SHA/tree/parents;
- workflow run ID;
- Frontend and Rust job IDs and conclusions;
- exact tested checkout SHA;
- final merge SHA/tree/parents;
- exact three-file effective diff;
- target and worker branch read-back;
- connector report/status publication commits/blobs;
- confirmation that Checkpoint 2R rerun, Bridge 01/02 and Wave 4 did not begin.

Do not authorize or execute the Checkpoint 2R rerun inside this worker. A separate orchestrator step must publish a new local validation contract based on the final merge SHA/tree.

## Terminal markers

Success:

`P3_CHECKPOINT_2R_R1_INTEGRATION_COMPLETE`

Blocker:

`P3_CHECKPOINT_2R_R1_INTEGRATION_BLOCKED_BY_IDENTITY_SCOPE_OR_CI`
