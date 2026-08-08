# P3-CHECKPOINT-2R-R2 — Integration contract

Status: `P3_CHECKPOINT_2R_R2_INTEGRATION_AUTHORIZED`

## Mode

Dedicated GitHub web integration worker.

Use only connected GitHub tools.

Do not use a local checkout, shell, Codex CLI, GitHub CLI, filesystem repository copy, or unconnected repository data.

This worker may create exactly one PR, inspect the exact synthetic merge ref and its CI, perform one normal merge commit after all gates pass, and publish connector integration evidence. It must not modify the product implementation or begin the next checkpoint.

## Required authority

Read completely before any product write:

- `signalguard-rs/phase-3/control/CURRENT_EXECUTION.md`
- `signalguard-rs/phase-3/control/STATUS.md`
- `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-R2-FOCUS.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-BLOCKER/9cedbeb9c9e5e59ad634123a3b2d6217555a5c96.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R2-FOCUS/dee3f17919b21dec1fbe701e069103c064f05dd4.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R2-FOCUS-REVIEW/dee3f17919b21dec1fbe701e069103c064f05dd4.md`

The independent review must have status:

`P3_CHECKPOINT_2R_R2_FOCUS_ACCEPTED_FOR_INTEGRATION`

Independent review identity:

- connector commit: `a35b8b1bb8955b4d9295371a2afa194d5724ab49`
- blob: `66dc5d97bf24ab3bd296382d205ac4a6fc1caa07`

## Exact product identities

Product repository:

`progeranna/signalguard-rs`

Target branch:

`refactor/dashboard-modules`

Exact immutable target base:

`9cedbeb9c9e5e59ad634123a3b2d6217555a5c96`

Expected target base tree:

`9bdfdcf331ef08cdeaf8f21a8ab66adee3092fe8`

Worker branch:

`p3/checkpoint2r-all-markets-back-focus`

Exact worker commit:

`dee3f17919b21dec1fbe701e069103c064f05dd4`

Expected worker tree:

`495d14862b0996766b5376358b99382124df9916`

Required worker commit message:

`fix(ui): restore all-markets back focus`

Before writing anything, verify:

1. target branch still resolves exactly to the immutable target base and expected tree;
2. worker branch still resolves exactly to the worker commit and expected tree;
3. worker commit is exactly one commit ahead and zero behind the target base;
4. merge base is exactly the target base;
5. no existing PR already owns this exact head/base pair;
6. the worker branch was not rewritten after independent review.

Any mismatch is a hard blocker.

## Exact accepted effective diff

Base-to-worker comparison must contain exactly two modified files:

- `web/src/pages/DashboardPage.tsx` — 15 additions / 3 deletions
- `web/src/pages/DashboardPage.popup.test.tsx` — 87 additions / 1 deletion

Aggregate:

- 2 modified files;
- 102 additions;
- 4 deletions;
- no added files;
- no deleted files;
- no renamed files.

No third product path is permitted.

The implementation must remain the accepted controller-local focus recovery only. Do not accept changes to `SymbolPopupIdentity`, `SymbolPopupReturnContext`, exact anomaly UUID state, routes, shared Dialog architecture, resources/API, CSS, ticker, Demo/Live ownership, preview limits, favicon/static assets, dependencies, lockfiles, bundle budgets, backend or migrations.

## Pull request

Create exactly one non-draft PR:

- base: `refactor/dashboard-modules`
- head: `p3/checkpoint2r-all-markets-back-focus`
- title: `fix(ui): restore all-markets back focus`

Do not modify either product branch before CI.

Do not create any second PR for this head/base pair.

## Synthetic merge verification

After PR creation, resolve the exact PR synthetic merge ref.

Its ordered parents must be exactly:

1. `9cedbeb9c9e5e59ad634123a3b2d6217555a5c96`
2. `dee3f17919b21dec1fbe701e069103c064f05dd4`

Its tree must be exactly:

`495d14862b0996766b5376358b99382124df9916`

Verify:

- target base → synthetic merge contains exactly the accepted two-file +102 / -4 diff;
- worker commit → synthetic merge has an empty file diff;
- no merge-only content drift exists;
- synthetic tree equals the accepted worker tree.

Stop before merge on any mismatch.

## Required exact-ref PR CI

Locate the GitHub Actions workflow run for the exact synthetic merge SHA.

Do not merge until the run completes successfully on its first deterministic attempt and both required jobs succeed:

- `frontend`;
- `rust`.

Verify from job metadata, steps and decoded logs that both jobs actually checked out the exact synthetic merge SHA / `refs/pull/<PR>/merge`.

### Frontend requirements

The exact synthetic merge ref must successfully run the repository's complete frontend CI, including:

- full Vitest suite;
- TypeScript typecheck;
- ESLint with zero warnings;
- production build;
- bundle-policy tests;
- bundle-budget check.

The accepted worker evidence had 44 frontend test files / 614 tests. CI must not silently lose test files or tests.

Bundle budgets must remain unchanged:

- initial max: `409600` bytes;
- largest max: `409600` bytes;
- total max: `414720` bytes.

Do not merge if CI weakens or changes budgets.

### Rust/global requirements

The exact synthetic merge ref must successfully run all configured Rust/global CI gates, including repository formatting, API-contract/OpenAPI validation where configured, `cargo check`, Clippy with warnings denied, Cargo tests, replay E2E where configured, Docker Compose config gates and shell syntax gates.

Do not use a CI rerun to conceal a deterministic first failure. If the first run exposes a product/test defect, stop and report a blocker instead of merging.

## Merge

Only after exact identity, scope, synthetic-merge and CI verification all pass, merge the PR using normal merge commit only.

Expected PR head SHA:

`dee3f17919b21dec1fbe701e069103c064f05dd4`

Do not squash, rebase, amend, force-push, or rewrite the worker commit.

## Required post-merge verification

After merge verify all of the following:

1. PR is closed and merged;
2. final target branch resolves to the normal merge commit;
3. final merge commit has exactly two ordered parents;
4. parent 1 is `9cedbeb9c9e5e59ad634123a3b2d6217555a5c96`;
5. parent 2 is `dee3f17919b21dec1fbe701e069103c064f05dd4`;
6. final tree is exactly `495d14862b0996766b5376358b99382124df9916`;
7. tested synthetic merge tree equals final merge tree;
8. old target base → final target effective diff remains exactly the accepted two files and +102 / -4;
9. worker commit → final merge has no file-content difference;
10. worker branch remains unchanged at `dee3f17919b21dec1fbe701e069103c064f05dd4`;
11. no unrelated product change was introduced.

## Connector integration publication

Publish exactly:

`signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R2-INTEGRATION/<FINAL_MERGE_SHA>.md`

Update exactly:

- `signalguard-rs/phase-3/control/CURRENT_EXECUTION.md`
- `signalguard-rs/phase-3/control/STATUS.md`

Final control state after successful integration must be:

`P3_CHECKPOINT_2R_R2_INTEGRATED_CHECKPOINT_RERUN_NOT_AUTHORIZED`

The integration report must record:

- contract identity;
- independent review identity;
- PR number/title/base/head;
- target and worker identities before PR creation;
- exact accepted two-file diff and statistics;
- synthetic merge SHA/tree/ordered parents;
- workflow run ID and attempt;
- Frontend and Rust job IDs/conclusions;
- exact checkout SHA observed in both job logs;
- frontend test file/test counts;
- bundle measurements and unchanged budgets;
- final merge SHA/tree/ordered parents;
- final target and worker branch read-back;
- proof that tested synthetic and final merge trees are identical;
- confirmation that no Checkpoint rerun occurred in this worker;
- confirmation that Bridge 01/02, Wave 4, favicon/static-asset work and later phases did not begin.

Read back and verify the integration report, `CURRENT_EXECUTION.md`, and `STATUS.md` after publication.

## Continuation boundary

This integration worker does not authorize or execute a Checkpoint 2R rerun.

After successful integration, a separate orchestrator step must publish a new local Checkpoint 2R rerun contract pinned to the final merge SHA/tree.

Until that later rerun is independently accepted:

- do not begin `P3-W4-BRIDGE01`;
- do not begin `P3-W4-BRIDGE02`;
- do not begin P3-MP21…P3-MP30 or later phase work;
- do not opportunistically fix the recorded `/favicon.ico` observation.

## Terminal status

Return exactly:

`P3_CHECKPOINT_2R_R2_INTEGRATION_COMPLETE`

only after exact PR CI, normal merge, final identity verification and connector publication all succeed.

On any identity, scope, synthetic-merge, CI, merge, or publication mismatch, do not continue and return:

`P3_CHECKPOINT_2R_R2_INTEGRATION_BLOCKED_BY_IDENTITY_SCOPE_OR_CI`
