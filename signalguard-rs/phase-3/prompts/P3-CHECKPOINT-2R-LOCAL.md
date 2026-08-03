# P3-CHECKPOINT-2R — Combined modal-only recovery validation

Status: `P3_CHECKPOINT_2R_LOCAL_VALIDATION_AUTHORIZED`

## Mode

Dedicated local Codex validation worker.

This is a read-only product verification checkpoint. It requires a real local checkout, command execution, production preview, browser automation and screenshot evidence.

It is not executable by a GitHub-only web worker.

Use the `$rust-development` skill.

## Exact accepted product identity

Product repository:

`progeranna/signalguard-rs`

Local repository:

`/Users/anion/Desktop/work/git-signalguard-rs/signalguard-rs`

Target branch:

`refactor/dashboard-modules`

Exact integrated commit:

`8bbef01d7d9979c4996954171a0e7c3748f02538`

Expected tree:

`d8f9e71e7aec5fcf7b472011a68247a6df42bbac`

Before validation, fetch the remote and verify that `origin/refactor/dashboard-modules` still resolves exactly to this commit and tree. Stop on drift.

## Required connector authority

Read completely:

- `signalguard-rs/phase-3/control/EXECUTION_PLAN.md`
- `signalguard-rs/phase-3/control/RESUMPTION_PLAN.md`
- `signalguard-rs/phase-3/control/MICRO_PHASE_LEDGER.md`
- `signalguard-rs/phase-3/control/IMPLEMENTATION_SEQUENCE.md`
- `signalguard-rs/phase-3/control/STATUS.md`
- `signalguard-rs/phase-3/reports/P3-MP18R-INTEGRATION/6142ec7004b75cda077a49ab37bcfdca01f7f8e8.md`
- `signalguard-rs/phase-3/reports/P3-MP20R-INTEGRATION/8bbef01d7d9979c4996954171a0e7c3748f02538.md`
- `signalguard-rs/phase-3/reports/P3-MP20R-INTEGRATION-TERMINAL-CORRECTION/8bbef01d7d9979c4996954171a0e7c3748f02538.md`

The contradictory chat marker from the MP20R integration worker is superseded by durable remote evidence. Do not recreate or reintegrate MP20R.

## Product write boundary

Product repository is strictly read-only.

Do not:

- create a product branch;
- create a product commit;
- modify, format, restore or regenerate any product file;
- update dependencies or lockfiles;
- open or merge a product PR;
- fix defects discovered during validation;
- alter routes, modal state, ticker, CSS, bundle budgets, API contracts or tests.

If a defect is found, preserve evidence and return a blocker report with the smallest proposed recovery lease. Do not implement the fix.

## Exact checkpoint objective

Validate the combined accepted MP18R + MP20R tree as one modal-only product state.

Required invariants:

- `/` and `/dashboard` are the only visual console pages.
- `/symbols/:symbol` and `/anomalies` replacement-redirect to `/dashboard`.
- Market activation opens Dashboard-owned Symbol Detail.
- Symbol Detail anomaly activation opens exact UUID-keyed Anomaly Detail.
- All Anomalies activation opens exact UUID-keyed Anomaly Detail.
- All Anomalies rows never open Symbol Detail.
- Back from nested Anomaly Detail restores the exact parent modal identity.
- Back restores focus to the exact visible originating row or card.
- Hidden responsive duplicates never receive focus.
- Close, Escape and backdrop close the complete active modal workflow.
- Mode or symbol replacement clears incompatible nested state.
- Late old-resource results cannot flash stale content into the new identity.
- Modal state remains local and ephemeral; URLs do not encode modal state.
- Demo and Live remain isolated.
- BTCUSDT and ETHUSDT identities remain exact.
- MP20R direct observed/threshold strings preserve the accepted visible formatting.
- No route/popup presentation wrapper has reappeared.

## Static and command validation

Use a clean detached worktree or clean checkout at the exact integrated commit. Do not reuse a dirty implementation worktree.

From `web/` run:

```bash
node --test scripts/check-bundle-size.test.mjs
npm run test:run
npm run typecheck
npm run lint
npm run build
npm run bundle:check
```

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

Verify:

- product checkout remains clean before and after validation;
- target commit and tree remain exact;
- no generated or untracked residue remains;
- package manifests, lockfiles and bundle budgets remain unchanged;
- the accepted PR CI run `30844622613` completed successfully against synthetic merge `9dd56162af7a23cc18a21dab8fe83428d521d667`;
- the synthetic merge tree and exact integrated tree are both `d8f9e71e7aec5fcf7b472011a68247a6df42bbac`.

## Browser matrix

Use isolated local ports that do not conflict with existing services or the `p35-manual-qa` environment.

Validate every matrix cell:

- mode: Demo and Live;
- symbol: BTCUSDT and ETHUSDT;
- viewport: desktop `1440×900` and mobile `390×844`.

For each applicable configuration validate pointer and keyboard behavior across these flow families:

1. Dashboard market activation → Symbol Detail.
2. Symbol Detail anomaly → exact Anomaly Detail → Back.
3. All Markets → Symbol Detail → exact Anomaly Detail → Back.
4. All Anomalies → exact Anomaly Detail → Back.

Also validate:

- desktop click, Enter and Space activation;
- mobile card activation;
- Tab and Shift+Tab containment;
- Escape;
- explicit Close;
- backdrop close;
- body scroll lock while a modal is open;
- exact visible focus restoration after Back and Close;
- no focus restoration to a hidden responsive duplicate;
- rapid Demo ↔ Live replacement while nested detail is open;
- rapid BTCUSDT ↔ ETHUSDT replacement while nested detail is open;
- direct visits to `/symbols/BTCUSDT`, `/symbols/ETHUSDT` and `/anomalies` replacement-redirect to `/dashboard` without standalone visual pages;
- modal flows do not change the route;
- zero unexpected console errors, page errors or unhandled rejections.

When Live data is unavailable for a configured symbol, validate the accepted unavailable/empty state and ensure no Demo fallback or cross-mode contamination occurs. Do not fabricate Live data.

## Screenshot evidence

Capture at least 16 deterministic changed-state screenshots.

Coverage must include:

- every Demo/Live × desktop/mobile cell;
- BTCUSDT and ETHUSDT in both modes;
- Symbol Detail;
- nested Anomaly Detail;
- All Markets flow;
- All Anomalies flow;
- at least four post-Back states showing the restored parent modal;
- at least four focus-restoration states with the visible focused trigger identifiable.

Record for every screenshot:

- file name;
- mode;
- symbol;
- viewport;
- flow step;
- SHA-256 hash.

Do not add screenshot files to the product repository.

## Defect handling

On any failure:

1. stop before modifying product code;
2. record exact reproduction steps;
3. record mode, symbol, viewport and input method;
4. record expected and actual behavior;
5. capture screenshot/video/log evidence where possible;
6. identify the smallest proposed product and test lease;
7. classify whether the defect belongs to MP18R, MP20R, pre-existing behavior or environment;
8. state whether it reproduces deterministically.

## Connector report

On success publish:

`signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R/8bbef01d7d9979c4996954171a0e7c3748f02538.md`

Connector commit message:

`docs(phase-3): publish Checkpoint 2R validation report`

The report must include:

- exact product commit/tree and clean-checkout evidence;
- complete command results;
- accepted CI run and tested synthetic merge identity;
- complete browser matrix results;
- screenshot inventory and SHA-256 hashes;
- console/page/unhandled error audit;
- confirmation of zero product writes;
- confirmation that semantic Bridge 01/02 and Wave 4 did not begin.

On failure publish instead:

`signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-BLOCKER/8bbef01d7d9979c4996954171a0e7c3748f02538.md`

using connector commit message:

`docs(phase-3): publish Checkpoint 2R blocker report`

Do not update `STATUS.md`. A separate GitHub web acceptance worker will verify the report and update control status.

## Terminal result

Return:

`P3_CHECKPOINT_2R_COMPLETE`

only after successful validation and verified connector report publication.

Return:

`P3_CHECKPOINT_2R_BLOCKED`

when any required command, browser flow, identity, clean-checkout condition or report publication fails.
