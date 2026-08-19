# P3-CHECKPOINT-2R-R4 — Integration contract

Status: `P3_CHECKPOINT_2R_R4_INTEGRATION_AUTHORIZED`

## Worker mode

Dedicated GitHub web integration worker using connected GitHub tools only.

Do not use a local checkout, shell, Codex CLI, GitHub CLI, filesystem repository copy, browser automation, or unconnected repository data.

This contract authorizes only exact-ref PR CI and integration of the independently accepted R4 selected-symbol ownership recovery.

Do not perform localhost product-owner verification or the next full Checkpoint 2R rerun inside this worker.

## Required authority

Read completely before any write:

- `signalguard-rs/phase-3/control/CURRENT_EXECUTION.md`
- `signalguard-rs/phase-3/control/STATUS.md`
- `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-R4-SELECTED-SYMBOL.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R4-SELECTED-SYMBOL/79abb161e7a731df7077d49b44481eaaf25bf762.md`
- `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-R4-REVIEW.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R4-REVIEW/79abb161e7a731df7077d49b44481eaaf25bf762.md`

Implementation contract identity:

- connector commit: `9ac409bbbd5e2ac8d0cb6bfdc49935b6b7712101`
- blob: `e0553a4cf90eeb907eb50bff665174d1917add55`
- required status: `P3_CHECKPOINT_2R_R4_SELECTED_SYMBOL_IMPLEMENTATION_AUTHORIZED`

Implementation report identity:

- connector commit: `7b9159bcfebf226bac852fdcdd68407ed2fd33de`
- blob: `85d797bc99bc92608097302757403d16da1827a3`
- required status: `P3_CHECKPOINT_2R_R4_SELECTED_SYMBOL_COMPLETE`

Independent review contract identity:

- connector commit: `280a333bc944aff66a990f17fd646c4f6f61de3b`
- blob: `8eed2c95d741fc28e44a87b1b99979da1c7efb8d`
- required status: `P3_CHECKPOINT_2R_R4_REVIEW_AUTHORIZED`

Independent review report identity:

- connector commit: `a1ab9cec75892d837d7b8514181c4fed807d4093`
- blob: `6b7d5b73f1e2b38cad6a34e5e5c6cf08ca6ea607`
- required status: `P3_CHECKPOINT_2R_R4_REVIEW_ACCEPTED`

The independent review accepted the exact source repair, the composed regression, the two explicit Live-ETHUSDT test preconditions, the two-file lease, and the worker branch identity. It explicitly distinguished GitHub-verifiable evidence from local `/tmp` browser evidence and retained the known `net::ERR_ABORTED` harness-classification limitation for later clean local verification.

## Exact product identity

Product repository:

`progeranna/signalguard-rs`

Target branch:

`refactor/dashboard-modules`

Exact target base:

`7dab5647d322339f5bd9d0514e5178522d5181c0`

Expected target base tree:

`d5ca241f173f2733d6699283084bf7435c0e9259`

Worker branch:

`p3/checkpoint2r-selected-symbol-ownership`

Exact worker commit:

`79abb161e7a731df7077d49b44481eaaf25bf762`

Expected worker tree:

`d8c0289a05b3646b3abc7056bd269b927e61d5c4`

Required worker message:

`fix(ui): reconcile modal symbol on mode change`

Before creating a PR, independently prove:

- target branch still resolves exactly to the target base and expected tree;
- worker branch still resolves exactly to the worker commit and expected tree;
- worker is exactly one commit ahead and zero behind the target base;
- merge base is exactly the target base;
- the worker commit direct parent is exactly the target base;
- worker message is exact;
- no existing pull request in any state already owns this head/base pair;
- no worker rewrite, extra worker commit, target drift, or unrelated branch change occurred.

Any identity drift is a hard blocker.

## Exact accepted diff

Target base → worker must contain exactly two modified files and no additions, deletions, or renames:

1. `web/src/pages/DashboardPage.tsx`
   - 26 additions
   - 14 deletions
2. `web/src/pages/DashboardPage.popup.test.tsx`
   - 119 additions
   - 0 deletions

Expected aggregate diff:

- 2 modified files;
- 145 additions;
- 14 deletions;
- 0 added files;
- 0 deleted files;
- 0 renamed files.

No additional product change is accepted.

The accepted semantic correction must remain exactly the independently reviewed one:

- one narrow `reconcileSymbolPopupIdentity` path combines `selectedUiMode` and non-null resolved `selectedSymbol`;
- the old `!modeChanged` suppression is removed from the causal replacement logic;
- immediate rendered Symbol Detail identity and modal-state replacement use the same reconciliation semantics;
- `returnContext` remains preserved;
- nested symbol-owned anomaly detail still collapses to Symbol Detail when parent identity changes, clearing stale UUID state;
- no second selected-symbol source, routing/URL state, resource ownership change, delay/remount/reload workaround, CSS/visual redesign, backend change, dependency change, favicon change, ticker change, or adjacent-scope modification is accepted.

## Pull request

Create exactly one non-draft pull request:

- base: `refactor/dashboard-modules`
- head: `p3/checkpoint2r-selected-symbol-ownership`
- title: `fix(ui): reconcile modal symbol on mode change`

Do not modify either branch before CI.

Do not create any second PR for the same head/base pair.

## Synthetic merge identity

After PR creation, identify the exact GitHub synthetic merge ref/commit generated for that PR.

Require ordered parents:

1. `7dab5647d322339f5bd9d0514e5178522d5181c0`
2. `79abb161e7a731df7077d49b44481eaaf25bf762`

Expected synthetic merge tree:

`d8c0289a05b3646b3abc7056bd269b927e61d5c4`

Because the worker directly descends from the exact target base and no unrelated target change is allowed, the synthetic tree must equal the accepted worker tree.

Verify before accepting CI:

- target base → synthetic effective diff is exactly the accepted two-file diff and exact per-file statistics;
- worker → synthetic file diff is empty;
- synthetic ordered parents are exact;
- synthetic tree equals the accepted worker tree;
- no merge-only content drift exists.

Stop before merge if any synthetic identity differs.

## Exact-ref PR CI

Require a fresh PR-triggered CI run for the exact synthetic merge ref.

Do not merge until both required jobs complete successfully on the exact synthetic merge SHA:

- `frontend`
- `rust`

Verify workflow run metadata, attempt number, job metadata, steps, and decoded logs.

Both jobs must have checked out the exact synthetic merge SHA, not merely the worker head SHA.

Do not infer exact-ref coverage from a green status alone.

### Frontend required result

The exact synthetic merge ref must pass:

- complete Vitest suite;
- exactly/no fewer than 44 frontend test files, with no file-count regression;
- no fewer than 615 frontend tests;
- zero test failures;
- TypeScript typecheck;
- ESLint with zero warnings;
- production build;
- bundle-policy tests;
- bundle-budget check.

Required bundle-policy result:

- 25/25 tests.

Configured bundle limits must remain unchanged:

- initial JS max: 409600 bytes;
- largest JS max: 409600 bytes;
- total JS max: 414720 bytes.

The accepted worker build recorded:

- initial JS: 389559 bytes;
- largest JS: 389559 bytes;
- total JS: 389559 bytes.

Because the synthetic tree must equal the accepted worker tree, expected deterministic measurements are the same. Any unexplained bundle drift or budget modification is a blocker.

The composed R4 regression must remain part of the passing suite; no test removal or weakening is permitted.

### Rust/global required result

The exact synthetic merge ref must pass the configured workflow gates for:

- formatting;
- generated API-contract check;
- OpenAPI validation;
- cargo check;
- Clippy with warnings denied;
- Cargo tests;
- replay E2E target discovery;
- Docker Compose config;
- Docker Compose app-profile config;
- demo script syntax;
- smoke script syntax.

Declared service-dependent ignored tests may remain ignored exactly as designed.

### First-attempt rule

A deterministic first-attempt CI failure blocks integration.

Do not rerun, alter, or retry CI to conceal a deterministic product/test/configuration failure.

If the first attempt fails for a demonstrably external GitHub infrastructure condition, record the exact evidence and stop for orchestrator disposition rather than unilaterally deciding to rerun.

## Merge

Only after exact synthetic identity and successful exact-ref PR CI, merge by normal merge commit.

Expected worker/head SHA:

`79abb161e7a731df7077d49b44481eaaf25bf762`

Do not squash, rebase, amend, force-push, rewrite, or recreate the accepted worker commit.

After merge independently verify:

- PR is closed and merged;
- target branch resolves to the final merge commit;
- final merge commit has exactly two ordered parents;
- parent 1 is `7dab5647d322339f5bd9d0514e5178522d5181c0`;
- parent 2 is `79abb161e7a731df7077d49b44481eaaf25bf762`;
- final tree is exactly `d8c0289a05b3646b3abc7056bd269b927e61d5c4`;
- old target base → final target contains the expected normal-merge history and exact accepted effective two-file diff;
- worker → final merge has empty file diff;
- tested synthetic tree equals final merge tree;
- worker branch remains unchanged at the accepted worker commit;
- no extra product path appears in final effective diff.

Do not claim integration complete before this final read-back.

## Connector publication

Publish the integration report exactly to:

`signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R4-INTEGRATION/<FINAL_MERGE_SHA>.md`

Connector report commit message:

`docs(phase-3): publish Checkpoint 2R R4 integration`

The report must record:

- integration contract identity;
- implementation contract/report identities;
- independent review contract/report identities;
- exact pre-PR target and worker identities;
- exact accepted two-file diff and statistics;
- PR number/title/base/head;
- synthetic merge SHA/tree/ordered parents;
- exact synthetic effective diff and empty worker→synthetic diff;
- workflow run ID, attempt, trigger, conclusion, and exact synthetic association;
- frontend and rust job IDs/conclusions;
- exact synthetic checkout SHA proved from decoded logs for both jobs;
- frontend test file/test counts, lint/typecheck/build/bundle-policy results, bundle measurements and unchanged limits;
- Rust/global gate disposition;
- first-attempt disposition;
- final merge SHA/tree/ordered parents;
- final target and worker branch read-back;
- final exact effective diff and synthetic/final tree equality;
- confirmation that no localhost product-owner verification, full Checkpoint 2R rerun, Bridge01/02, semantic Wave 4, or later work began.

Then update exactly these two connector control files:

- `signalguard-rs/phase-3/control/CURRENT_EXECUTION.md`
- `signalguard-rs/phase-3/control/STATUS.md`

Final control state must be exactly:

`P3_CHECKPOINT_2R_R4_INTEGRATED_LOCALHOST_USER_VERIFICATION_REQUIRED`

The control files must pin the new final product merge SHA/tree and state that the next orchestration step is a separate dedicated local localhost/product-owner verification contract against the exact integrated merge.

The control files must explicitly state that the full Checkpoint 2R rerun is not yet authorized until that localhost verification step is completed and accepted by the user/orchestrator.

## Strict continuation boundary

Do not execute, authorize, or begin within this integration worker:

- localhost/product-owner verification;
- a full Checkpoint 2R rerun;
- any defect repair discovered outside exact integration/CI blockers;
- `P3-W4-BRIDGE01`;
- `P3-W4-BRIDGE02`;
- P3-MP21…P3-MP30 / semantic Wave 4;
- dialogs/accessibility work;
- routing/loading/performance work;
- responsive/final work;
- Phase 4 or later work.

If integration is blocked by identity, scope, synthetic merge, CI, or merge-read-back failure, do not repair product code from this worker. Publish only the blocker evidence permitted by the current authority and return the blocker marker.

## Terminal status

Return exactly:

`P3_CHECKPOINT_2R_R4_INTEGRATION_COMPLETE`

only after exact-ref first-attempt CI success, normal merge, final identity verification, integration report publication, and control transition all succeed.

Otherwise return exactly:

`P3_CHECKPOINT_2R_R4_INTEGRATION_BLOCKED_BY_IDENTITY_SCOPE_OR_CI`
