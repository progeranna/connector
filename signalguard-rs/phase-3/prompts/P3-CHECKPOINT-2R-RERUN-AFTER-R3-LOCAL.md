# P3-CHECKPOINT-2R-RERUN-AFTER-R3 — Full combined modal-only recovery validation

Status: `P3_CHECKPOINT_2R_RERUN_AFTER_R3_LOCAL_VALIDATION_AUTHORIZED`

## Mode

Dedicated local Codex validation worker.

Use the `$rust-development` skill.

This is the final full read-only Checkpoint 2R acceptance rerun after integration of MP18R, MP20R, R1 View-all reachability recovery, R2 All Markets Back-focus recovery, and R3 favicon/browser-console recovery.

This task requires local command execution, isolated production services, a real Chrome browser context, exact focus verification, redirect/modal-state verification, stale-resource replacement checks, zero-error browser acceptance, and deterministic screenshot evidence.

It is not executable by a GitHub-only web worker.

Product write lease: `NONE`.

## Exact accepted product identity

Product repository:

`progeranna/signalguard-rs`

Target branch:

`refactor/dashboard-modules`

Exact integrated commit:

`7dab5647d322339f5bd9d0514e5178522d5181c0`

Expected integrated tree:

`d5ca241f173f2733d6699283084bf7435c0e9259`

The accepted final merge has ordered parents:

1. `cbf5c543ada8752c273fbb2e91be029c9febc3d3`
2. `778b23b6a9dbb4e1b652e7a31349a35b707f3373`

Before any validation, fetch the authenticated remote and prove `origin/refactor/dashboard-modules` still resolves exactly to this accepted commit/tree. Any drift is a hard blocker.

## Required authority and evidence

Read completely before validation:

- `signalguard-rs/phase-3/control/CURRENT_EXECUTION.md`
- `signalguard-rs/phase-3/control/STATUS.md`
- `signalguard-rs/phase-3/control/EXECUTION_PLAN.md`
- `signalguard-rs/phase-3/control/RESUMPTION_PLAN.md`
- `signalguard-rs/phase-3/control/MICRO_PHASE_LEDGER.md`
- `signalguard-rs/phase-3/control/IMPLEMENTATION_SEQUENCE.md`
- `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-LOCAL.md`
- `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-RERUN-LOCAL.md`
- `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-RERUN-AFTER-R2-LOCAL.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-BLOCKER/8bbef01d7d9979c4996954171a0e7c3748f02538.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-BLOCKER/9cedbeb9c9e5e59ad634123a3b2d6217555a5c96.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-AFTER-R2-BLOCKER/cbf5c543ada8752c273fbb2e91be029c9febc3d3.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R1-INTEGRATION/9cedbeb9c9e5e59ad634123a3b2d6217555a5c96.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R2-INTEGRATION/cbf5c543ada8752c273fbb2e91be029c9febc3d3.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R3-FAVICON/778b23b6a9dbb4e1b652e7a31349a35b707f3373.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R3-FAVICON-REVIEW/778b23b6a9dbb4e1b652e7a31349a35b707f3373.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R3-INTEGRATION/7dab5647d322339f5bd9d0514e5178522d5181c0.md`

Accepted R3 integration evidence:

- PR: `#73`
- R3 worker commit: `778b23b6a9dbb4e1b652e7a31349a35b707f3373`
- synthetic merge: `3b949b7e94f7a7ebe3d5e2b8e2bd2c8e10e59514`
- tested/final tree: `d5ca241f173f2733d6699283084bf7435c0e9259`
- workflow run: `31309410396`, attempt 1, success
- frontend job: `93234775362`, success
- rust job: `93234775345`, success
- frontend exact-ref CI: 44 files / 614 tests
- JS bundle: 389599 bytes initial/largest/total under unchanged limits
- final merge: `7dab5647d322339f5bd9d0514e5178522d5181c0`
- integration report commit: `60ac20579fa1b51901fb0b3850e273989fdcf77f`
- integration report blob: `2ece1d96dc4b471ffe972bd4be7282a1dd753625`

## Local execution isolation

Local repository:

`/Users/anion/Desktop/work/git-signalguard-rs/signalguard-rs`

Create a NEW clean detached validation worktree at the exact integrated commit. Suggested path:

`/Users/anion/Desktop/work/git-signalguard-rs/worktrees/p3-checkpoint-2r-rerun-after-r3-7dab564`

Do not reuse:

- any MP18R or MP20R worktree;
- the R1 worktree;
- the R2 worktree;
- the R3 implementation worktree;
- any previous Checkpoint 2R validation worktree;
- `p35-manual-qa`.

Use isolated service names and ports. Do not disturb existing local services or the manual-QA environment.

## Strict read-only product boundary

Do not:

- modify any tracked product or test file;
- create a product branch;
- create a product commit;
- push any product change;
- open or merge a product PR;
- run formatters in write mode;
- update dependencies or lockfiles;
- regenerate committed API artifacts;
- edit tests to make a failure pass;
- modify favicon/static assets;
- fix any defect discovered during validation;
- begin Bridge 01, Bridge 02, Wave 4, or any later phase.

Transient ignored/generated build artifacts are permitted only as required to execute validation. Remove them before final cleanliness verification.

## Required command gates

From `web/` run:

```bash
node --test scripts/check-bundle-size.test.mjs
npm run test:run
npm run typecheck
npm run lint
npm run build
npm run bundle:check
```

Required expectations:

- bundle-policy tests: 25/25;
- no fewer than 44 frontend test files;
- no fewer than 614 frontend tests;
- zero frontend test failures;
- typecheck passes;
- ESLint passes with zero warnings;
- production build passes;
- bundle-budget check passes.

Bundle limits must remain exactly:

- initial max: `409600` bytes;
- largest max: `409600` bytes;
- total max: `414720` bytes.

Expected accepted JS measurements are:

- initial JS: `389599` bytes;
- largest JS: `389599` bytes;
- total JS: `389599` bytes.

Any unexplained budget/config drift is a blocker.

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

All prescribed commands must pass. Declared service-dependent ignored tests may remain ignored exactly as designed; do not misrepresent them as executed service-backed success.

## Identity, cleanliness, and immutable-file audit

Before and after validation record and compare:

- `HEAD`;
- repository tree;
- `git status --porcelain=v1 --untracked-files=all`;
- ignored-artifact status after cleanup;
- `Cargo.toml`;
- `Cargo.lock`;
- `web/package.json`;
- `web/package-lock.json`;
- `web/bundle-size-budget.json`;
- `web/scripts/check-bundle-size.mjs`;
- `web/scripts/check-bundle-size.test.mjs`;
- `web/index.html`;
- `contracts/web-console.openapi.json`.

The final detached worktree must be clean with no tracked, untracked, ignored, generated, service, or dependency residue attributable to this validation.

## Full real-browser checkpoint

Run the exact accepted product using an isolated production build/preview and the real accepted backend behavior.

Do not mock, fabricate, or inject frontend market/anomaly data for acceptance.

Validate every core combination:

### Modes

- Demo
- Live

### Symbols

- BTCUSDT
- ETHUSDT

### Viewports

- desktop `1440×900`
- mobile `390×844`

This is an 8-cell mode × symbol × viewport core matrix.

For Live, validate the actual available/unavailable backend state. Never substitute Demo data into Live.

## Mandatory flow families

Across the full matrix validate all applicable behavior for:

1. Dashboard market activation → Symbol Detail.
2. Symbol Detail exact anomaly activation → exact UUID-keyed Anomaly Detail → Back.
3. All Markets → Symbol Detail → exact Anomaly Detail → Back to Symbol Detail → Back to All Markets.
4. All Anomalies → exact Anomaly Detail → Back to All Anomalies.
5. Direct compatibility routes → replacement redirect to Dashboard.

Do not substitute unit/component evidence for real-browser acceptance.

## Mandatory R1 regression gate

Using real deterministic Demo data, explicitly prove:

- backend Demo collection has exactly the actually returned market/anomaly cardinalities; if they differ from the previously observed 7 markets / 3 anomalies, record the actual values and do not fabricate data;
- Market Health `View all` is visible, enabled, and keyboard focusable whenever the market collection is non-empty;
- Recent Anomalies `View all` is visible, enabled, and keyboard focusable whenever the anomaly collection is non-empty;
- with the accepted deterministic Demo fixture, the expected 7-market / 3-anomaly cardinality remains reachable if unchanged;
- All Markets actually opens;
- All Anomalies actually opens;
- no artificial records are injected to force these actions to appear.

## Mandatory R2 regression gate

Explicitly prove the previously failing complete nested flow on both required viewports using real Demo data:

```text
All Markets
→ BTCUSDT Symbol Detail
→ exact BTCUSDT Anomaly Detail
→ Back to Symbol Detail
→ Back to All Markets
```

Desktop `1440×900` and mobile `390×844` must each prove:

- direct All Markets initial focus behavior is correct;
- the first Back restores the exact visible anomaly UUID trigger;
- the hidden responsive anomaly duplicate does not receive focus;
- the second Back restores the exact visible originating `Open BTCUSDT market detail` row/card;
- the hidden responsive market duplicate does not receive focus;
- another market row/card does not receive focus;
- the restored parent is exactly All Markets;
- Symbol Detail identity retains `returnContext === "symbols"` semantics;
- pathname remains `/` or `/dashboard` throughout.

A unit-test pass is not sufficient if real-browser focus disagrees.

## Mandatory R3 regression gate

Use fresh browser contexts and the real production preview to prove the integrated document-level favicon recovery remains effective.

At minimum validate initial navigation to both:

- `/dashboard`
- `/`

Require:

- embedded favicon declaration is present in the served production document;
- `/favicon.ico` request count is exactly `0`;
- no browser request interception, service-worker trick, proxy suppression, route mocking, or favicon-specific response rewriting is used;
- browser console errors from the favicon surface are `0`;
- real Dashboard resources and real API calls still load normally.

The R3 regression gate must be evaluated before claiming the global zero-console acceptance result, but successful R3 proof does not replace the rest of the full matrix.

## Input, focus, lifecycle, and accessibility matrix

Validate where applicable:

- pointer click;
- Enter activation;
- Space activation;
- mobile card activation;
- exact same-symbol different-anomaly UUID distinction;
- Tab containment;
- Shift+Tab containment;
- exact visible initial focus;
- exact visible Back focus restoration;
- hidden responsive duplicate exclusion;
- explicit Close;
- Escape;
- backdrop close;
- body scroll lock while modal is open;
- exact body scroll restoration after close;
- no accidental Back behavior from Close/Escape/backdrop;
- no focus escape behind an open modal.

## Mode/symbol replacement and stale-content matrix

With Symbol Detail and nested detail states open, validate rapid:

- Demo → Live;
- Live → Demo where practical;
- BTCUSDT → ETHUSDT;
- ETHUSDT → BTCUSDT where practical.

Require:

- stale nested UUID state clears when identity replacement requires it;
- old symbol/mode content disappears immediately;
- no stale old-resource flash;
- no cross-mode resource reuse;
- no Demo fallback presented as Live;
- selected symbol ownership remains correct.

## Route and URL invariants

Validate direct navigation to:

- `/symbols/BTCUSDT`
- `/symbols/ETHUSDT`
- `/anomalies`

Each must replacement-redirect to `/dashboard` and render no standalone detail page.

During all Dashboard modal flows:

- pathname remains `/` or `/dashboard`;
- no modal state is serialized into the URL;
- browser URL is not used as modal identity storage.

## Console and page-error acceptance

Across the full accepted browser checkpoint require:

- zero unexpected browser console errors;
- zero page errors;
- zero unhandled promise rejections.

Record warnings separately from errors. Do not silently suppress or pre-waive a deterministic browser error.

If a deterministic unexpected browser error appears, stop success claims at that first failure, capture exact evidence, and follow the defect-handling rules below.

## Screenshot evidence

Capture at least 16 deterministic screenshots outside both repositories.

The inventory must collectively cover:

- Demo and Live;
- desktop and mobile;
- BTCUSDT and ETHUSDT;
- Dashboard with both View-all controls where data is non-empty;
- Symbol Detail;
- exact nested Anomaly Detail;
- All Markets;
- All Anomalies;
- at least four post-Back parent states;
- at least four exact visible-focus restoration states;
- R2 post-second-Back market focus on desktop and mobile;
- at least one successful R3 fresh-context Dashboard load with zero favicon request/error.

For every screenshot record:

- filename;
- mode;
- symbol;
- viewport;
- input method where applicable;
- flow step;
- exact focus target where applicable;
- SHA-256 hash.

Do not add screenshots to either repository.

## Defect handling

On the first deterministic product/browser acceptance failure:

1. Do not modify product code or tests.
2. Capture exact reproduction steps.
3. Record mode, symbol, viewport, route, input method, exact modal state, and exact identity/UUID where applicable.
4. Record expected versus actual behavior.
5. Capture relevant screenshot/log/request evidence.
6. Classify the defect as MP18R, MP20R, R1 reachability, R2 focus recovery, R3 favicon recovery, pre-existing, environmental, or a separately observed issue.
7. State whether reproduction is deterministic and at which viewports/modes.
8. Identify the smallest proposed production/test recovery lease.
9. Stop success claims for the uncompleted matrix; do not extrapolate unexecuted cells.
10. Do not implement the fix.

An environmental blocker must be supported by concrete evidence that product acceptance could not be evaluated; do not label a deterministic product failure environmental.

## Connector report publication

On full success publish exactly:

`signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-AFTER-R3/7dab5647d322339f5bd9d0514e5178522d5181c0.md`

Connector commit message:

`docs(phase-3): publish Checkpoint 2R rerun after R3`

On any blocker publish exactly:

`signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-AFTER-R3-BLOCKER/7dab5647d322339f5bd9d0514e5178522d5181c0.md`

Connector commit message:

`docs(phase-3): publish Checkpoint 2R rerun after R3 blocker`

The report must record:

- contract identity;
- exact product commit/tree;
- clean detached worktree identity/path;
- all command gates with exact test counts;
- immutable-file and cleanup audit;
- accepted R3 PR/CI identity read-back;
- isolated service/port topology;
- real Demo/Live data observations;
- R1 regression result;
- R2 regression result;
- R3 regression result;
- full browser matrix disposition;
- exact pointer/keyboard/focus behavior;
- redirect/URL invariants;
- console/page-error/unhandled-rejection counts;
- screenshot inventory and SHA-256 hashes;
- zero product-write confirmation;
- confirmation that Bridge 01/02, Wave 4 and later work did not begin.

Do not update `signalguard-rs/phase-3/control/CURRENT_EXECUTION.md` or `signalguard-rs/phase-3/control/STATUS.md` from the validation worker.

A separate GitHub web acceptance/recovery worker must independently verify the report before any Bridge 01 authorization.

## Terminal status

Return exactly:

`P3_CHECKPOINT_2R_RERUN_AFTER_R3_COMPLETE`

only if every command gate, every mandatory browser obligation, every R1/R2/R3 regression gate, the full 8-cell matrix, zero-error acceptance, screenshot requirement, final cleanliness check, and connector report publication succeeds.

Otherwise return exactly:

`P3_CHECKPOINT_2R_RERUN_AFTER_R3_BLOCKED`

Do not begin Bridge 01, Bridge 02, Wave 4, or any later work.