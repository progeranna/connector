# P3-CHECKPOINT-2R — Full rerun after R4

Status: `P3_CHECKPOINT_2R_RERUN_AFTER_R4_AUTHORIZED`

## Mode

Dedicated local Codex validation worker.

Use `$rust-development`.

This is a strict **read-only full Checkpoint 2R rerun** against the exact integrated R4 product. Product write lease: `NONE`.

Use the authenticated local checkout, shell, Docker, real production build/preview and real browser automation. This contract is not executable by a GitHub-only worker.

Do not modify product code, tests, generated contracts, package manifests, lockfiles, bundle budgets, routes, CSS, backend, ticker or configuration files. Do not create a product branch, commit, push, PR or merge. If a defect is found, stop product work and publish blocker evidence only.

## Exact integrated product identity

Product repository: `progeranna/signalguard-rs`

Local repository:

`/Users/anion/Desktop/work/git-signalguard-rs/signalguard-rs`

Target branch:

`refactor/dashboard-modules`

Exact integrated commit:

`23656c9b93a24bfc20ba8f417275564bb5b5d240`

Expected tree:

`d8c0289a05b3646b3abc7056bd269b927e61d5c4`

Expected ordered parents:

1. `7dab5647d322339f5bd9d0514e5178522d5181c0`
2. `79abb161e7a731df7077d49b44481eaaf25bf762`

Before validation, fetch the authenticated product remote and prove `origin/refactor/dashboard-modules` still resolves exactly to this commit/tree and exact ordered parents. Any drift is a hard blocker; do not adapt to a newer head.

## Required connector authority

Read completely before validation:

- `signalguard-rs/phase-3/control/CURRENT_EXECUTION.md`
- `signalguard-rs/phase-3/control/STATUS.md`
- `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-LOCAL.md`
- `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-R4-LOCALHOST-USER-VERIFICATION.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R4-LOCALHOST-USER-ACCEPTANCE/23656c9b93a24bfc20ba8f417275564bb5b5d240.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R4-INTEGRATION/23656c9b93a24bfc20ba8f417275564bb5b5d240.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-AFTER-R3-BLOCKER/7dab5647d322339f5bd9d0514e5178522d5181c0.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-AFTER-R3-BLOCKER-REVIEW/7dab5647d322339f5bd9d0514e5178522d5181c0.md`

Original Checkpoint contract baseline:

- path: `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-LOCAL.md`
- current blob: `72467c9adae47853586fc4665cbffe93dabfbebd`

R4 integration authority:

- report publication commit: `f2189063dba447bd0dca4a83ee16120e4f31959e`
- report blob: `6a2a94ed57e01635d8fdaa4809170400bb572c65`
- status: `P3_CHECKPOINT_2R_R4_INTEGRATION_COMPLETE`

Product-owner acceptance authority:

- report publication commit: `74e3fc339036c3fd2c8676adc3f508005c723e0d`
- report blob: `0b817619bb820f82b7482bc9b62eb386e6807d4c`
- status: `P3_CHECKPOINT_2R_R4_LOCALHOST_USER_ACCEPTED`

Required current control state:

`P3_CHECKPOINT_2R_RERUN_AFTER_R4_AUTHORIZED`

## Clean execution boundary

Create a new clean detached worktree at exact integrated commit `23656c9b93a24bfc20ba8f417275564bb5b5d240`.

Do not reuse:

- the R4 implementation worktree;
- the product-owner localhost worktree;
- any prior Checkpoint worktree;
- `p35-manual-qa` or any other existing QA environment.

Keep screenshots, logs, browser traces, helper scripts and all other evidence outside both repositories under a deterministic `/tmp/p3-checkpoint2r-rerun-after-r4-...` directory.

Before and after the rerun record and require:

- exact HEAD SHA;
- exact tree SHA;
- detached HEAD;
- `git status --porcelain` empty;
- `git diff --check` pass;
- no generated/untracked residue in the product worktree.

Use isolated PostgreSQL/Redis/backend/preview/proxy ports and do not disturb the already accepted product-owner localhost environment if it is still running.

## Static and command gates

From `web/` run exactly:

```bash
node --test scripts/check-bundle-size.test.mjs
npm run test:run
npm run typecheck
npm run lint
npm run build
npm run bundle:check
```

Required frontend disposition:

- bundle-policy: `25/25`;
- frontend test files: at least `44`, with no file-count regression;
- frontend tests: at least `615`, zero failures;
- `DashboardPage.popup.test.tsx`: all tests pass, including the R4 composed regression;
- typecheck pass;
- lint pass with zero warnings;
- production build pass;
- bundle budget pass;
- configured limits remain exactly `409600 / 409600 / 414720` bytes;
- record actual initial/largest/total JS bytes; exact integrated CI measured `389559 / 389559 / 389559`, so any drift must be explained and must not come from a tracked modification.

From repository root run exactly:

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
git diff --check
```

All must pass. Record test counts and ignored tests. Declared service-dependent ignored cases may remain ignored only as designed; do not silently convert failures to ignores.

## Real browser environment

Build and serve the exact production frontend from the detached integrated commit with a real backend and isolated PostgreSQL/Redis.

Demo must use the real deterministic Demo behavior. Live must remain source `live`; never substitute or present Demo as Live.

Do not mock or intercept API responses, selected-symbol storage, mode state, modal state, popup resources, market/anomaly data, route behavior, favicon behavior or runtime errors.

If real Live data for a required validation transition cannot be obtained, do not fabricate it. Record the environmental condition and return blocked if it prevents a mandatory replacement sequence from being proved.

## Core browser matrix

Validate all 8 cells:

- mode: Demo, Live;
- symbol: BTCUSDT, ETHUSDT;
- viewport: desktop `1440×900`, mobile `390×844`.

For every applicable cell validate the original Checkpoint flow families:

1. Dashboard market activation → Symbol Detail.
2. Symbol Detail anomaly → exact UUID Anomaly Detail → Back.
3. All Markets → Symbol Detail → exact UUID Anomaly Detail → Back.
4. All Anomalies → exact UUID Anomaly Detail → Back.

Validate across the matrix:

- desktop pointer activation;
- Enter and Space activation where specified by the UI contract;
- mobile card activation;
- Tab and Shift+Tab focus containment;
- Escape close;
- explicit Close;
- backdrop close;
- body scroll lock while a modal is open;
- exact Back parent restoration;
- exact visible focus restoration after Back and Close;
- hidden responsive duplicates never receive restored focus;
- modal state remains local/ephemeral and does not enter the URL;
- `/` and `/dashboard` remain the only visual console pages;
- direct `/symbols/BTCUSDT`, `/symbols/ETHUSDT` and `/anomalies` visits replacement-redirect to `/dashboard` without standalone visual pages;
- All Anomalies activation never incorrectly opens Symbol Detail;
- MP20R direct observed/threshold presentation remains accepted;
- Demo/Live isolation and exact BTCUSDT/ETHUSDT identity remain intact.

## Mandatory recovery regressions R1–R4

The full rerun must explicitly prove all recovery dimensions together, not merely rely on unit tests.

### R1 — All Markets / View-all flow

Prove All Markets opens from the intended dashboard trigger and market activation opens the exact Dashboard-owned Symbol Detail without route-backed modal state or duplicate presentation ownership.

### R2 — Back focus

On both desktop and mobile, prove Back from nested Symbol Detail anomaly restores the correct parent and focus to the exact visible originating All Markets row/card. Hidden desktop/mobile duplicates must never receive focus.

### R3 — favicon console cleanliness

In every fresh browser context, count requests whose pathname is exactly `/favicon.ico`.

Required count: `0`.

Any favicon 404, console error or favicon request is a blocker.

### R4 — composed mode/symbol ownership

Run this exact composed sequence on **desktop and mobile** from fresh contexts:

`Demo/BTCUSDT → Live/BTCUSDT → Live/ETHUSDT → Demo/BTCUSDT`

Use the All Markets/Symbol Detail return context and nested symbol-owned anomaly state.

Required proof:

1. Demo stores `BTCUSDT` and Live initially resolves `BTCUSDT`.
2. Open Demo BTC Symbol Detail from All Markets and open an exact Demo BTC nested anomaly when real data/UI permits.
3. Switch to Live while nested state is open; stale Demo UUID must clear and parent must be `live:BTCUSDT:symbols`.
4. Open a Live BTC nested anomaly when available.
5. Change Live selected symbol to `ETHUSDT`; stale BTC UUID must clear and parent must be `live:ETHUSDT:symbols`.
6. Open an exact Live ETH nested anomaly.
7. Switch back to Demo while the nested Live ETH state is open.
8. Header mode must be Demo and header selected symbol must restore Demo's stored `BTCUSDT`.
9. Stale Live ETH anomaly UUID/detail must disappear.
10. Open parent must be exactly `demo:BTCUSDT:symbols`, never `demo:ETHUSDT:symbols`.
11. BTCUSDT content must be visible; stale ETHUSDT content must be absent.
12. `returnContext` must remain `symbols` / All Markets.
13. Demo and Live stored selections must remain separate: Demo `BTCUSDT`, Live `ETHUSDT` after this sequence.
14. Back must return to All Markets correctly.
15. No hard page reload may be used to accomplish any replacement.
16. Late stale old-mode/old-symbol resources must not reattach or flash into the current parent.

Also prove same-mode BTCUSDT → ETHUSDT replacement and mode-only same-symbol replacement remain correct.

## Console, page, request and navigation audit

For every fresh browser context capture:

- console errors;
- page errors;
- unhandled promise rejections;
- responses >= 400;
- `requestfailed` events with concrete URL, resource type and failure text;
- document/navigation requests;
- `/favicon.ico` requests.

Required:

- zero unexpected console errors;
- zero page errors;
- zero unhandled rejections;
- zero unexplained transport failures;
- zero `/favicon.ico` requests;
- modal transitions do not create document reload/navigation.

Do **not** blanket-ignore `net::ERR_ABORTED`.

Every `net::ERR_ABORTED` must be listed individually with concrete URL, method/resource type and the mode/symbol transition that cancelled it. It may be classified as expected only when evidence shows it is an obsolete stale-query API request cancelled because ownership changed. Any unexplained aborted document, asset, favicon, navigation or critical current-identity API request blocks the checkpoint.

## Screenshot and structured evidence

Capture at least 18 deterministic screenshots outside the repositories.

Coverage must include:

- all Demo/Live × desktop/mobile cells;
- BTCUSDT and ETHUSDT in both modes;
- Symbol Detail;
- nested Anomaly Detail;
- All Markets;
- All Anomalies;
- at least four post-Back restored-parent states;
- at least four visible focus-restoration states;
- final desktop R4 `demo:BTCUSDT:symbols` state;
- final mobile R4 `demo:BTCUSDT:symbols` state.

For every screenshot record filename, mode, symbol, viewport, flow step and SHA-256.

Also produce a structured browser log outside the repositories containing identities, exact UUIDs, storage values, navigation entries, console/page/unhandled errors, >=400 responses, request failures and favicon count.

## Defect handling

On any deterministic product failure:

1. do not modify product code;
2. record exact reproduction steps;
3. record mode, symbol, viewport and input method;
4. record expected and actual behavior;
5. capture screenshot/log evidence;
6. identify the smallest proposed product and test lease;
7. classify it against the existing recovery history or as pre-existing/environmental;
8. state deterministic/non-deterministic status;
9. stop before Bridge work.

## Connector report

On complete success publish exactly:

`signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-AFTER-R4/23656c9b93a24bfc20ba8f417275564bb5b5d240.md`

Connector commit message:

`docs(phase-3): publish Checkpoint 2R rerun after R4`

The report must include:

- contract publication commit/blob;
- product commit/tree/parents and remote identity proof;
- clean detached worktree evidence;
- complete command-gate results and counts;
- bundle counts/bytes/limits;
- complete 8-cell browser matrix;
- explicit R1/R2/R3/R4 regression evidence;
- desktop and mobile composed R4 sequence evidence;
- screenshot inventory and SHA-256 hashes;
- structured console/page/unhandled/request/navigation audit;
- concrete disposition of every `net::ERR_ABORTED` if any;
- `/favicon.ico` request count;
- confirmation of zero product writes;
- confirmation Bridge01/02 and Wave 4 did not begin.

On failure publish instead exactly:

`signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-AFTER-R4-BLOCKER/23656c9b93a24bfc20ba8f417275564bb5b5d240.md`

Connector commit message:

`docs(phase-3): publish Checkpoint 2R rerun after R4 blocker`

Do not update `CURRENT_EXECUTION.md` or `STATUS.md`. The orchestrator owns the next transition.

## Continuation boundary

A successful local report is **not** independent acceptance.

After success, the only next permitted orchestration step is a dedicated independent GitHub-web checkpoint acceptance review.

Do not begin:

- Bridge01;
- Bridge02;
- P3-MP21…P3-MP30;
- dialogs/accessibility;
- routing/loading/performance;
- responsive/final;
- Phase 4 or later work.

## Terminal markers

On complete success return exactly:

`P3_CHECKPOINT_2R_RERUN_AFTER_R4_COMPLETE`

On any required gate/browser/identity/cleanliness/evidence failure return exactly:

`P3_CHECKPOINT_2R_RERUN_AFTER_R4_BLOCKED`
