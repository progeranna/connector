# P3-CHECKPOINT-2R-RERUN — Combined modal-only recovery validation after R1

Status: `P3_CHECKPOINT_2R_RERUN_LOCAL_VALIDATION_AUTHORIZED`

## Mode

Dedicated local Codex validation worker.

Use the `$rust-development` skill.

This is a read-only product acceptance checkpoint. It requires local command execution, an isolated production preview, real-browser automation, focus verification, and deterministic screenshot evidence.

It is not executable by a GitHub-only web worker.

## Exact accepted product identity

Product repository:

`progeranna/signalguard-rs`

Local repository:

`/Users/anion/Desktop/work/git-signalguard-rs/signalguard-rs`

Target branch:

`refactor/dashboard-modules`

Exact integrated commit:

`9cedbeb9c9e5e59ad634123a3b2d6217555a5c96`

Expected tree:

`9bdfdcf331ef08cdeaf8f21a8ab66adee3092fe8`

Before validation, fetch the remote over authenticated HTTPS and verify that `origin/refactor/dashboard-modules` still resolves exactly to this commit and tree. Stop on identity drift.

Use a new clean detached validation worktree at the exact commit. Do not reuse dirty MP18R, MP20R, R1, or previous Checkpoint 2R worktrees.

## Required connector authority

Read completely before product validation:

- `signalguard-rs/phase-3/control/CURRENT_EXECUTION.md`
- `signalguard-rs/phase-3/control/STATUS.md`
- `signalguard-rs/phase-3/control/EXECUTION_PLAN.md`
- `signalguard-rs/phase-3/control/RESUMPTION_PLAN.md`
- `signalguard-rs/phase-3/control/MICRO_PHASE_LEDGER.md`
- `signalguard-rs/phase-3/control/IMPLEMENTATION_SEQUENCE.md`
- `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-LOCAL.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-BLOCKER/8bbef01d7d9979c4996954171a0e7c3748f02538.md`
- `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-R1-WEB.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R1/f793b8447076a9feb8227447c2b851622475ef7c.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R1-REVIEW/f793b8447076a9feb8227447c2b851622475ef7c.md`
- `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-R1-INTEGRATION.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R1-INTEGRATION/9cedbeb9c9e5e59ad634123a3b2d6217555a5c96.md`

The previous Checkpoint 2R blocker was the missing real-Demo `View all` reachability at 7 markets and 3 recent anomalies. R1 is now integrated through PR #71. This rerun must validate the complete checkpoint from the beginning; do not assume only the former blocker needs testing.

## Accepted R1 integration evidence

- PR: `#71`, closed and merged by normal merge commit.
- worker commit: `f793b8447076a9feb8227447c2b851622475ef7c`.
- final merge: `9cedbeb9c9e5e59ad634123a3b2d6217555a5c96`.
- final tree: `9bdfdcf331ef08cdeaf8f21a8ab66adee3092fe8`.
- synthetic merge: `3b7f85eb12f78a729206d61a6a4e86b29f6d0961`.
- synthetic tree: `9bdfdcf331ef08cdeaf8f21a8ab66adee3092fe8`.
- CI workflow run: `31252099540`, attempt 1, conclusion success.
- frontend job: `93089901530`, success.
- rust job: `93089901697`, success.
- both CI jobs checked out the exact synthetic merge SHA.
- PR CI frontend suite: 44 files, 612 tests passed; typecheck, lint, build, and bundle policy passed.
- PR CI bundle: 389,453 bytes initial/largest/total JS within unchanged budgets.
- Rust/global CI passed all required workflow steps.

Independently verify this durable evidence where practical. The synthetic and final trees must be identical.

## Product write boundary

Product write lease: `NONE`.

Do not:

- modify any repository-controlled product or test file;
- create a product branch or product commit;
- push product changes;
- open or merge a product PR;
- run a formatter in write mode;
- update dependencies, manifests, lockfiles, generated API artifacts, routes, CSS, modal state, ticker behavior, or bundle budgets;
- fix defects discovered during this checkpoint;
- begin Bridge 01, Bridge 02, Wave 4, or any later phase.

Normal transient ignored artifacts produced by build/test commands are permitted only for validation. Remove them afterward and prove the checkout is clean. Do not delete or overwrite user work outside the isolated validation worktree.

Do not disturb existing services, implementation worktrees, or the `p35-manual-qa` environment. Use isolated ports and isolated service/project names.

## Exact checkpoint objective

Validate the accepted combined MP18R + MP20R + Checkpoint-2R-R1 tree as one modal-only product state.

Required invariants:

- `/` and `/dashboard` are the only visual console pages.
- `/symbols/:symbol` and `/anomalies` replacement-redirect to `/dashboard`.
- Market activation opens Dashboard-owned Symbol Detail.
- Symbol Detail anomaly activation opens exact UUID-keyed Anomaly Detail.
- All Anomalies activation opens exact UUID-keyed Anomaly Detail and never Symbol Detail.
- Market Health `View all` remains reachable whenever the market collection is non-empty, including accepted Demo cardinality 7.
- Recent Anomalies `View all` remains reachable whenever the anomaly collection is non-empty, including accepted Demo cardinality 3.
- Empty corresponding collections do not expose a misleading `View all` action.
- All Markets opens from real Demo and its rows open Symbol Detail.
- All Anomalies opens from real Demo and its rows open exact Anomaly Detail.
- Back from nested Anomaly Detail restores the exact parent modal identity.
- Back restores focus to the exact visible originating row/card.
- Hidden responsive duplicates never receive focus.
- Close, Escape, and backdrop close the complete active modal workflow rather than acting as Back.
- Body scroll lock is correct while a modal is open and restored after close.
- Mode or symbol replacement clears incompatible nested state.
- Late old-resource results cannot flash stale content into the new identity.
- Modal state remains local and ephemeral; URLs do not encode modal state.
- Demo and Live remain strictly isolated.
- BTCUSDT and ETHUSDT identities remain exact.
- MP20R direct observed/threshold strings preserve accepted visible formatting.
- No route/popup presentation wrapper has reappeared.
- No standalone Symbol Detail or Anomalies page has reappeared.

## Static and command validation

Record clean status and exact HEAD/tree before running commands.

From `web/` run:

```bash
node --test scripts/check-bundle-size.test.mjs
npm run test:run
npm run typecheck
npm run lint
npm run build
npm run bundle:check
```

Expected current frontend suite floor from PR CI: 44 files and 612 tests. Do not accept a silent loss of test coverage.

From repository root run:

```bash
cargo fmt --check
cargo run --quiet --bin export-api-contract -- --check
cargo run --quiet --bin export-api-contract -- --validate
cargo check
cargo clippy --all-targets --all-features -- -D warnings
cargo test
cargo test --test replay_e2e
docker compose config
docker compose --profile app config
bash -n scripts/demo-replay.sh
bash -n scripts/smoke.sh
```

Verify after commands:

- exact HEAD remains `9cedbeb9c9e5e59ad634123a3b2d6217555a5c96`;
- exact tree remains `9bdfdcf331ef08cdeaf8f21a8ab66adee3092fe8`;
- checkout has no tracked, untracked, or generated residue after cleanup;
- package manifests and lockfiles are byte-identical to the committed checkout;
- bundle budget files/scripts are unchanged;
- no API artifact drift was generated;
- bundle budgets remain unchanged and pass;
- accepted PR CI run `31252099540` remains success;
- PR synthetic tree and integrated tree are both `9bdfdcf331ef08cdeaf8f21a8ab66adee3092fe8`.

## Browser environment

Run the accepted product locally from the exact detached commit using isolated service/project names and ports that do not conflict with existing services on 5173, 8080, 5432, or 6379 or with `p35-manual-qa`.

Use production build/preview behavior, not a source-only mock harness, for browser acceptance.

Use the actual deterministic Demo response produced by the accepted backend. Do not inject extra markets/anomalies merely to make a flow reachable.

For Live, use the actual configured Live response/state. If Live data is unavailable for a symbol, validate the accepted unavailable/empty state and strict absence of Demo fallback or cross-mode contamination. Do not fabricate Live data.

## Browser matrix

Validate every matrix cell:

- mode: Demo and Live;
- symbol: BTCUSDT and ETHUSDT;
- viewport: desktop `1440×900` and mobile `390×844`.

This is 8 core mode/symbol/viewport cells. Where a Live cell has no observed data, record the real unavailable/empty state explicitly rather than substituting Demo state.

For every applicable cell validate the relevant pointer and keyboard behavior across these flow families:

1. Dashboard market activation → Symbol Detail.
2. Symbol Detail anomaly → exact Anomaly Detail → Back.
3. All Markets → Symbol Detail → exact Anomaly Detail → Back.
4. All Anomalies → exact Anomaly Detail → Back.

The former blocker is a mandatory early check: in real Demo, confirm both `View all` controls are visible and focusable with exactly the backend-provided collections, then actually execute both modal entry flows.

Also validate:

- desktop pointer click;
- desktop Enter activation;
- desktop Space activation;
- mobile card activation;
- Tab and Shift+Tab focus containment;
- Escape close;
- explicit Close;
- backdrop close;
- body scroll lock while modal is open and restoration after close;
- exact visible focus restoration after Back and after closing a parent workflow where specified;
- focus never returns to a hidden desktop/mobile responsive duplicate;
- same-symbol different anomaly UUIDs remain distinguishable;
- rapid Demo ↔ Live replacement while nested detail is open;
- rapid BTCUSDT ↔ ETHUSDT replacement while nested detail is open;
- no stale old-resource flash during replacement;
- direct visits to `/symbols/BTCUSDT`, `/symbols/ETHUSDT`, and `/anomalies` replacement-redirect to `/dashboard` without standalone visual pages;
- modal activation/back/close flows leave pathname at `/` or `/dashboard` and never synchronize modal identity to the URL;
- zero unexpected console errors;
- zero page errors;
- zero unhandled promise rejections.

## Screenshot evidence

Capture at least 16 deterministic changed-state screenshots outside the product repository.

The inventory must collectively include:

- every Demo/Live × desktop/mobile category;
- BTCUSDT and ETHUSDT in both modes where the real state permits;
- real-Demo Dashboard with both `View all` entry points reachable;
- Symbol Detail;
- nested exact Anomaly Detail;
- All Markets;
- All Anomalies;
- at least four post-Back states showing the restored parent modal;
- at least four focus-restoration states where the visible focused trigger can be identified.

For every screenshot record:

- filename;
- mode;
- symbol;
- viewport;
- input method where relevant;
- flow step;
- SHA-256 hash.

Do not add screenshots or browser artifacts to the product repository.

## Evidence quality

Do not claim a flow passed merely because a component/unit test covers it. Browser-required acceptance must come from the real running product.

Do not skip a mandatory flow because it is inconvenient. If actual product/data state makes a mandatory flow impossible, that is a checkpoint blocker unless this contract explicitly defines that state as an accepted unavailable/empty Live condition.

For focus restoration, record the exact trigger identity and the element receiving focus after Back/Close. For responsive duplicates, explicitly record that the focused element is visible in the active viewport.

For anomaly detail, record the exact UUID used and verify same-symbol alternative UUID content is not substituted.

## Defect handling

On any required failure:

1. stop before modifying product code;
2. preserve the clean accepted product identity;
3. record exact reproduction steps;
4. record mode, symbol, viewport, route, and input method;
5. record expected and actual behavior;
6. capture screenshot/log/video evidence where useful;
7. identify the smallest proposed production and test lease;
8. classify the defect as MP18R, MP20R, R1 reachability, pre-existing behavior, or environment;
9. state whether it reproduces deterministically;
10. do not implement the proposed fix.

## Connector report

On success publish:

`signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN/9cedbeb9c9e5e59ad634123a3b2d6217555a5c96.md`

Connector commit message:

`docs(phase-3): publish Checkpoint 2R rerun validation report`

The success report must include:

- exact contract commit/blob;
- exact product commit/tree and clean detached-checkout evidence;
- complete command-gate results and test counts;
- bundle byte measurements and unchanged budgets;
- accepted PR #71 synthetic-merge/CI identity;
- complete browser matrix, including explicit real Live unavailable states where applicable;
- exact UUID/focus evidence;
- former `View all` blocker regression verification at real Demo cardinalities;
- screenshot inventory and SHA-256 hashes;
- console/page/unhandled-rejection audit;
- zero product writes confirmation;
- confirmation that Bridge 01/02 and Wave 4 did not begin.

On failure publish instead:

`signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-BLOCKER/9cedbeb9c9e5e59ad634123a3b2d6217555a5c96.md`

Connector commit message:

`docs(phase-3): publish Checkpoint 2R rerun blocker report`

Do not update `STATUS.md` or `CURRENT_EXECUTION.md` from the local validation worker. A separate GitHub web acceptance/recovery worker will independently verify the report and update control state.

## Terminal result

Return:

`P3_CHECKPOINT_2R_RERUN_COMPLETE`

only after every required command gate, browser obligation, evidence obligation, clean-checkout condition, and connector success-report publication succeeds.

Return:

`P3_CHECKPOINT_2R_RERUN_BLOCKED`

when any required identity, command, browser, evidence, cleanup, or report-publication obligation fails.

Neither terminal marker authorizes Bridge 01, Bridge 02, or Wave 4. A separate GitHub web acceptance step is mandatory after this rerun.
