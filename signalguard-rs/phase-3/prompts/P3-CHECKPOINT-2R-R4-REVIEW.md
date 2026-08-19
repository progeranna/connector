# P3-CHECKPOINT-2R-R4 — Independent implementation review

Status: `P3_CHECKPOINT_2R_R4_REVIEW_AUTHORIZED`

## Mode

Dedicated independent GitHub web review worker.

Use only the connected GitHub tools.

Do not use a local checkout, shell, Codex CLI, GitHub CLI, filesystem repository copy, browser automation, or unconnected repository data.

This is read-only product review. Product write lease: `NONE`.

The worker may publish only the exact review report authorized below in `progeranna/connector`. It must not modify product code, product branches, pull requests, control files, status files, prior reports, or any other connector path.

## Exact connector authority

Connector repository:

`progeranna/connector`

Implementation contract:

`signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-R4-SELECTED-SYMBOL.md`

Implementation-contract publication commit:

`9ac409bbbd5e2ac8d0cb6bfdc49935b6b7712101`

Expected implementation-contract blob:

`e0553a4cf90eeb907eb50bff665174d1917add55`

Expected implementation authorization:

`P3_CHECKPOINT_2R_R4_SELECTED_SYMBOL_IMPLEMENTATION_AUTHORIZED`

Implementation report:

`signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R4-SELECTED-SYMBOL/79abb161e7a731df7077d49b44481eaaf25bf762.md`

Implementation-report publication commit:

`7b9159bcfebf226bac852fdcdd68407ed2fd33de`

Expected implementation-report blob:

`85d797bc99bc92608097302757403d16da1827a3`

Reported terminal status:

`P3_CHECKPOINT_2R_R4_SELECTED_SYMBOL_COMPLETE`

Read the implementation contract and implementation report completely before forming a conclusion.

Also read completely:

- `signalguard-rs/phase-3/control/CURRENT_EXECUTION.md`
- `signalguard-rs/phase-3/control/STATUS.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-AFTER-R3-BLOCKER/7dab5647d322339f5bd9d0514e5178522d5181c0.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-AFTER-R3-BLOCKER-REVIEW/7dab5647d322339f5bd9d0514e5178522d5181c0.md`

## Exact product identities

Product repository:

`progeranna/signalguard-rs`

Target branch:

`refactor/dashboard-modules`

Immutable accepted base commit:

`7dab5647d322339f5bd9d0514e5178522d5181c0`

Expected base tree:

`d5ca241f173f2733d6699283084bf7435c0e9259`

Worker branch:

`p3/checkpoint2r-selected-symbol-ownership`

Exact worker commit:

`79abb161e7a731df7077d49b44481eaaf25bf762`

Expected worker tree:

`d8c0289a05b3646b3abc7056bd269b927e61d5c4`

Required worker commit message:

`fix(ui): reconcile modal symbol on mode change`

First independently prove:

- target branch is still exactly the immutable base commit/tree;
- worker branch is still exactly the worker commit/tree;
- worker is exactly one commit ahead and zero behind the immutable base;
- merge base and direct parent are exactly the immutable base;
- no worker rewrite or extra commit occurred;
- no R4 pull request exists yet.

Any identity drift is a hard review blocker.

## Exact expected diff

The base-to-worker effective diff must contain exactly these two modified paths and no additions, deletions, or renames:

- `web/src/pages/DashboardPage.tsx`
- `web/src/pages/DashboardPage.popup.test.tsx`

Expected compare statistics:

- `web/src/pages/DashboardPage.tsx`: 26 additions, 14 deletions;
- `web/src/pages/DashboardPage.popup.test.tsx`: 119 additions, 0 deletions;
- total: 145 additions, 14 deletions.

No other product path is authorized.

## Required independent source review

Do not accept the implementation merely because the implementation report says it passed.

Inspect the exact worker diff and the relevant exact base/worker source. At minimum determine independently whether:

1. the old `previousUiModeRef` / `modeChanged` / `!modeChanged` suppression is removed only from the causal replacement logic;
2. a single narrow reconciliation path derives popup identity from both `selectedUiMode` and the already resolved non-null `selectedSymbol`;
3. the same reconciliation semantics are used for immediate rendered Symbol Detail identity and modal-state replacement;
4. when mode and symbol both change, the resulting parent identity contains both new values without an intermediate retained old-symbol owner becoming the accepted state;
5. `returnContext` is preserved by the existing popup identity helpers;
6. nested symbol-owned anomaly detail still collapses to Symbol Detail when parent identity changes, clearing stale UUID state;
7. same-mode symbol replacement remains correct;
8. mode replacement where the selected symbol is unchanged remains correct;
9. no second selected-symbol source of truth, new storage, timer/delay, forced remount, reload, modal-closing workaround, DOM mutation, URL-backed modal state, or resource ownership change was introduced;
10. imports and hook usage remain coherent after removal of `previousUiModeRef`.

Inspect the new composed regression in `DashboardPage.popup.test.tsx` and verify it genuinely covers:

`Demo/BTCUSDT → Live/BTCUSDT → Live/ETHUSDT → Demo/BTCUSDT`

with nested detail state open and proves stale UUID/content absence, final `demo:BTCUSDT:symbols` ownership, preserved `symbols` return context, per-mode stored selection isolation, and late stale-resource rejection.

The implementation also modified two pre-existing tests by explicitly seeding Live `ETHUSDT`. Review these changes carefully and determine whether they preserve the original test intent rather than weakening, bypassing, or rewriting an assertion to make the implementation pass.

## Adjacent-scope audit

Confirm the worker did not modify or semantically require changes to:

- `web/src/features/dashboard/selectedSymbol.ts`;
- `web/src/app/AppShell.tsx`;
- `web/src/features/dashboard/symbolPopup.ts`;
- `web/src/features/dashboard/symbolPopupResource.ts`;
- routes/router/navigation;
- URL-backed modal state;
- CSS, layout, copy, or visual redesign;
- R1 View-all implementation;
- R2 Back-focus implementation;
- R3 favicon/static assets;
- MP20R presentation/adapters;
- ticker ownership;
- API/resource schemas or queries;
- backend Rust/OpenAPI/contracts;
- dependencies, manifests, lockfiles;
- bundle budgets/scripts;
- Docker or migrations;
- Bridge01/Bridge02, semantic Wave 4, or later work.

## Validation-evidence review

The implementation report records:

- focused popup file: 32/32 tests;
- full frontend: 44/44 files, 615/615 tests;
- bundle-policy: 25/25;
- typecheck: pass;
- lint: zero warnings;
- build: pass;
- JS bytes: 389559 / 389559 / 389559 under unchanged 409600 / 409600 / 414720 limits;
- Rust/global gates: pass, including 379 Rust tests and declared ignored service-dependent cases;
- focused real-browser desktop and mobile sequence: reported pass;
- `/favicon.ico` requests: reported zero;
- no PR/merge: reported.

Independently verify all evidence that is available through connected GitHub: exact source, commit/tree/parent identity, compare stats, branch relations, absence of an R4 PR, report immutability, and any repository-backed test/CI evidence that actually exists.

### External browser-evidence limitation

The implementation report references `/tmp` browser artifacts and SHA-256 hashes. Those bytes are not GitHub repository objects and are not available to a GitHub-only reviewer.

Do not claim to have opened, rehashed, or independently verified those external files or screenshots.

The implementation transcript also records that the local validation harness was adjusted after a run containing `net::ERR_ABORTED` request failures so that `net::ERR_ABORTED` events were classified as expected request cancellations, while non-`ERR_ABORTED` failures remained unexpected. The transcript available to the orchestrator does not expose the folded concrete cancellation URLs.

Therefore the review report must explicitly distinguish:

- repository-backed facts independently verified by GitHub;
- browser/gate facts reported by the implementation worker but not independently reproducible in GitHub-only mode;
- the `ERR_ABORTED` classification limitation above.

This limitation alone does not require rejection if the exact code/test change is independently correct and the reported focused proof is internally coherent, because a full clean local Checkpoint 2R rerun is mandatory after integration. But the reviewer must reject any attempt to represent unavailable external bytes as independently verified evidence.

## Review decision

Accept the R4 worker only if all of the following are independently supported:

- exact immutable identities and branch relation are correct;
- exact two-file lease and diff are correct;
- source change fixes the accepted causal defect without broadening ownership;
- new regression is meaningful and adjacent test edits do not weaken coverage;
- no unauthorized product change, PR, merge, or target mutation occurred;
- implementation report is immutable and internally consistent;
- no repository-backed evidence contradicts the reported gate/browser outcome.

If accepted, the next orchestration step is a separate immutable **GitHub-web R4 integration contract**. This review does not authorize creating the PR or merging.

## Report publication

Publish exactly one new connector report:

`signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R4-REVIEW/79abb161e7a731df7077d49b44481eaaf25bf762.md`

The report must include:

- exact reviewed connector contract/report commits and blobs;
- exact product base/worker SHA and tree identities;
- worker branch relation and no-rewrite proof;
- exact two-file diff and stats;
- independent source/test semantic review;
- explicit disposition of the two pre-existing test seed changes;
- adjacent-scope audit;
- GitHub-verifiable validation evidence;
- explicit external-browser-evidence limitation and `ERR_ABORTED` classification limitation;
- accepted or rejected review conclusion;
- next allowed orchestration step.

Do not update `CURRENT_EXECUTION.md` or `STATUS.md`; the orchestrator owns the next control transition.

## Terminal markers

If accepted:

`P3_CHECKPOINT_2R_R4_REVIEW_ACCEPTED`

If blocked or rejected:

`P3_CHECKPOINT_2R_R4_REVIEW_BLOCKED`

No product write, PR creation, merge, integration, localhost acceptance, Checkpoint rerun, Bridge work, or later work is authorized by this review contract.
