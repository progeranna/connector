# P3-CHECKPOINT-2R — Independent acceptance review after R4

Status: `P3_CHECKPOINT_2R_RERUN_AFTER_R4_REVIEW_AUTHORIZED`

## Worker mode

Dedicated independent GitHub-web checkpoint acceptance worker using connected GitHub tools only.

Do not use a local checkout, shell, Codex CLI, GitHub CLI, filesystem repository copy, browser automation, or unconnected repository data.

This is an independent **read-only acceptance review** of the completed full Checkpoint 2R rerun after R4.

Product write lease: `NONE`.

Connector write lease: only the exact review report path authorized below.

Do not update `CURRENT_EXECUTION.md` or `STATUS.md`. Do not begin Bridge01, Bridge02, semantic Wave 4, or any later product work.

## Required current authority

Before any write, fetch and read completely from `progeranna/connector`:

- `signalguard-rs/phase-3/control/CURRENT_EXECUTION.md`
- `signalguard-rs/phase-3/control/STATUS.md`
- `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-RERUN-AFTER-R4.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-AFTER-R4/23656c9b93a24bfc20ba8f417275564bb5b5d240.md`
- `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-R4-LOCALHOST-USER-VERIFICATION.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R4-LOCALHOST-USER-ACCEPTANCE/23656c9b93a24bfc20ba8f417275564bb5b5d240.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R4-INTEGRATION/23656c9b93a24bfc20ba8f417275564bb5b5d240.md`
- `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-LOCAL.md`

Required current control state:

`P3_CHECKPOINT_2R_RERUN_AFTER_R4_REVIEW_AUTHORIZED`

## Exact rerun authority

Rerun contract:

- path: `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-RERUN-AFTER-R4.md`
- publication commit: `e49bb785ff753a78c9c274689365a573d44f695b`
- blob: `cee0cac364ef38f0e52947006392227dbc38a9ec`
- required status: `P3_CHECKPOINT_2R_RERUN_AFTER_R4_AUTHORIZED`

Completed rerun report:

- path: `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-AFTER-R4/23656c9b93a24bfc20ba8f417275564bb5b5d240.md`
- publication commit: `378783556646bc414a0cd16548aa6bda6ae9c503`
- blob: `a5a171385f5c902f8128168e763293d13c071109`
- required status: `P3_CHECKPOINT_2R_RERUN_AFTER_R4_COMPLETE`

Verify that current connector `main` still resolves the rerun report path to the exact blob above. Any report rewrite or identity mismatch is a hard blocker.

## Exact product identity

Product repository:

`progeranna/signalguard-rs`

Target branch:

`refactor/dashboard-modules`

Exact integrated commit:

`23656c9b93a24bfc20ba8f417275564bb5b5d240`

Expected tree:

`d8c0289a05b3646b3abc7056bd269b927e61d5c4`

Expected ordered parents:

1. `7dab5647d322339f5bd9d0514e5178522d5181c0`
2. `79abb161e7a731df7077d49b44481eaaf25bf762`

Independently verify through connected GitHub:

- target branch still resolves exactly to the integrated commit;
- target is zero commits ahead/behind that exact commit;
- merge base is the exact integrated commit;
- changed-file compare is empty;
- exact commit tree is `d8c0289a05b3646b3abc7056bd269b927e61d5c4`;
- ordered parents are exact;
- PR #74 remains merged and its final merge identity is consistent with the integration report;
- no later product commit has been integrated into the target.

Any product target drift is a hard blocker. Do not review a newer head as equivalent.

## Review objective

Determine whether the durable Checkpoint 2R rerun report is internally complete, consistent with GitHub-verifiable product and connector state, and sufficient to accept Checkpoint 2R for continuation to Bridge01.

This reviewer must preserve the distinction between:

1. facts independently reproducible through connected GitHub; and
2. local execution/browser evidence reported by the dedicated local validator but not reproducible in GitHub-only mode.

Do not falsely claim to have rerun local commands, Docker, Chrome, Playwright, screenshots, localhost services, or `/tmp` evidence.

Conversely, do not reject the checkpoint merely because GitHub-only mode cannot reopen local `/tmp` artifacts, provided the durable report records the required evidence completely and no GitHub-verifiable contradiction exists.

## Mandatory report completeness audit

Read the completed rerun report completely and require explicit durable disposition for all of the following.

### Static/frontend gates

The report must record:

- bundle-policy `25/25`;
- frontend test files `44/44` or greater than/equal to 44 with no regression;
- frontend tests `615/615` or greater than/equal to 615 with zero failures;
- `DashboardPage.popup.test.tsx` passing all composed tests including R4;
- typecheck pass;
- lint pass with zero warnings;
- production build pass;
- bundle check pass;
- actual JS bytes;
- unchanged limits exactly `409600 / 409600 / 414720`.

Expected integrated deterministic bytes are `389559 / 389559 / 389559`. Any different value requires a credible explanation and no tracked product drift.

### Rust/global gates

The report must record pass disposition for:

- `cargo fmt --check`;
- generated API contract check;
- OpenAPI validation;
- `cargo check`;
- Clippy with warnings denied;
- `cargo test`;
- `cargo test --test replay_e2e`;
- both Docker Compose config gates;
- `bash -n scripts/demo-replay.sh`;
- `bash -n scripts/smoke.sh`;
- `git diff --check`.

It must distinguish designed ignored service-dependent tests from failures.

### Clean execution boundary

The report must record:

- fresh detached worktree at exact integrated commit;
- exact tree;
- clean before and after;
- no tracked/untracked/generated residue;
- no product writes;
- no target drift before/after;
- isolated local services/evidence outside both repositories.

### Full browser matrix

Require durable disposition for all 8 cells:

- Demo/BTCUSDT desktop 1440×900;
- Demo/BTCUSDT mobile 390×844;
- Demo/ETHUSDT desktop;
- Demo/ETHUSDT mobile;
- Live/BTCUSDT desktop;
- Live/BTCUSDT mobile;
- Live/ETHUSDT desktop;
- Live/ETHUSDT mobile.

Require coverage of the original Checkpoint flow families and modal/focus/route invariants, including Dashboard Symbol Detail, nested exact UUID Anomaly Detail, All Markets, All Anomalies, Back, focus restoration, Escape, Close, backdrop, focus containment, scroll lock, route replacement redirects, ephemeral modal state, Demo/Live isolation, and exact symbol identity.

A legitimate real-data empty state may be accepted only if the report explicitly states that no data was fabricated and covers the applicable flow without cross-mode fallback.

### Recovery R1–R4

Require explicit durable evidence for:

- R1 All Markets/View-all ownership;
- R2 exact visible Back-focus restoration and hidden-duplicate exclusion on desktop and mobile;
- R3 `/favicon.ico` request count exactly zero and console cleanliness;
- R4 exact composed desktop and mobile sequence:
  `Demo/BTCUSDT → Live/BTCUSDT → Live/ETHUSDT → Demo/BTCUSDT`.

For R4 require the report to state:

- nested UUID clearing on ownership replacement;
- exact intermediate identities `live:BTCUSDT:symbols` and `live:ETHUSDT:symbols`;
- final identity `demo:BTCUSDT:symbols`;
- stale ETH detail/content absent;
- `returnContext=symbols` preserved;
- final per-mode selected-symbol storage Demo=`BTCUSDT`, Live=`ETHUSDT`;
- Back restoration to All Markets;
- no hard reload;
- stale late resources do not reattach.

### Runtime/transport audit

Require the report to record:

- zero unexpected console errors;
- zero page errors;
- zero unhandled rejections;
- zero unexplained HTTP >=400 responses;
- zero unexplained request failures;
- `/favicon.ico` request count zero;
- document/navigation accounting showing modal flows did not reload;
- concrete disposition of every `net::ERR_ABORTED`, if any.

Blanket acceptance of `net::ERR_ABORTED` is forbidden. If the report records none, state that explicitly in the review.

### Evidence inventory

Require at least 18 screenshots with durable inventory metadata and SHA-256 hashes recorded in the report, including final desktop/mobile R4 states and focus/post-Back coverage.

The report may reference local `/tmp` paths, but the reviewer must describe those screenshots/hashes as reported local evidence unless the bytes are independently available through GitHub.

Require a structured browser evidence/log disposition in the durable report.

## GitHub-verifiable consistency checks

Independently inspect enough current product source/test state to establish that the accepted integrated R4 implementation and its regression still exist at the exact target commit.

At minimum inspect or verify the relevant exact files at the integrated commit:

- `web/src/pages/DashboardPage.tsx`;
- `web/src/pages/DashboardPage.popup.test.tsx`;
- `web/src/features/dashboard/selectedSymbol.ts`;
- `web/src/features/dashboard/symbolPopup.ts`;
- `web/index.html` or the current favicon-owning entry point as applicable.

Verify no repository-backed evidence contradicts the rerun report's R1–R4 conclusions.

Also read the R4 integration report and product-owner acceptance report completely and ensure their exact identities and status are consistent with the rerun report.

## Scope and mutation audit

The reviewer must perform no product write.

Do not:

- create/modify/delete product files;
- create branches;
- create/update PRs;
- merge anything;
- push or rewrite refs;
- update product configuration;
- run a repair.

The reviewer also must not update connector control files.

The only connector write permitted is the exact review report below.

## Disposition rules

Accept only if all of the following hold:

1. contract/report identities and statuses are exact;
2. product target remains exact and undrifted;
3. rerun report is complete against every required gate and browser/recovery dimension;
4. no GitHub-verifiable contradiction exists;
5. local-only evidence is clearly labeled as reported rather than independently reproduced;
6. no unauthorized product or connector-control mutation occurred;
7. Bridge01/02 and Wave 4 have not begun.

Do not introduce new product requirements during review.

If the report is incomplete, internally contradictory, or contradicted by current exact product/GitHub state, block with specific evidence. Do not repair product code.

## Connector review report

On acceptance publish exactly:

`signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-AFTER-R4-REVIEW/23656c9b93a24bfc20ba8f417275564bb5b5d240.md`

Connector commit message:

`docs(phase-3): accept Checkpoint 2R rerun after R4`

The report must include:

- review contract commit/blob/status;
- current control blobs/status observed before review;
- rerun contract/report commit/blob/status;
- exact product commit/tree/parents and target compare proof;
- R4 integration/product-owner acceptance identities;
- GitHub-verifiable source/test consistency audit;
- full report-completeness disposition for frontend, Rust/global, clean boundary, 8-cell browser matrix, R1–R4, runtime/transport, evidence inventory;
- explicit distinction between GitHub-verifiable facts and reported local-only evidence;
- `net::ERR_ABORTED` disposition;
- confirmation of zero product writes and zero control-file writes;
- confirmation Bridge01/02 and Wave 4 did not begin;
- acceptance rationale.

Terminal status in the report:

`P3_CHECKPOINT_2R_RERUN_AFTER_R4_ACCEPTED`

On blocker publish exactly:

`signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-AFTER-R4-REVIEW-BLOCKER/23656c9b93a24bfc20ba8f417275564bb5b5d240.md`

Connector commit message:

`docs(phase-3): block Checkpoint 2R rerun after R4 review`

Terminal status:

`P3_CHECKPOINT_2R_RERUN_AFTER_R4_REVIEW_BLOCKED`

Do not update `CURRENT_EXECUTION.md` or `STATUS.md` in either outcome. The orchestrator owns the next transition.

## Continuation boundary

An accepted review authorizes no work by itself until the orchestrator verifies the published review and updates control state.

Do not begin:

- `P3-W4-BRIDGE01`;
- `P3-W4-BRIDGE02`;
- P3-MP21…P3-MP30 / semantic Wave 4;
- dialogs/accessibility;
- routing/loading/performance;
- responsive/final;
- Phase 4 or later work.

## Worker terminal markers

On acceptance return exactly:

`P3_CHECKPOINT_2R_RERUN_AFTER_R4_ACCEPTED`

On blocker return exactly:

`P3_CHECKPOINT_2R_RERUN_AFTER_R4_REVIEW_BLOCKED`
