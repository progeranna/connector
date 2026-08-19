# P3-CHECKPOINT-2R-R4 — Reconcile open Symbol Detail ownership on mode replacement

Status: `P3_CHECKPOINT_2R_R4_SELECTED_SYMBOL_IMPLEMENTATION_AUTHORIZED`

## Mode

Dedicated local Codex implementation worker.

Use the `$rust-development` skill.

This is a narrow recovery implementation for the independently accepted Checkpoint 2R stale mode/symbol ownership blocker.

Do not perform unrelated cleanup or continue to Bridge 01/02, semantic Wave 4, dialogs/accessibility, routing/loading/performance, responsive/final, Phase 4, or later work.

## Exact product base

Product repository:

`progeranna/signalguard-rs`

Target branch:

`refactor/dashboard-modules`

Immutable implementation base commit:

`7dab5647d322339f5bd9d0514e5178522d5181c0`

Expected base tree:

`d5ca241f173f2733d6699283084bf7435c0e9259`

Before editing, fetch the authenticated remote and prove `origin/refactor/dashboard-modules` still resolves exactly to this commit and tree. Any drift is a hard blocker.

The accepted base has ordered parents:

1. `cbf5c543ada8752c273fbb2e91be029c9febc3d3`
2. `778b23b6a9dbb4e1b652e7a31349a35b707f3373`

## Required connector authority

Read completely before implementation:

- `signalguard-rs/phase-3/control/CURRENT_EXECUTION.md`
- `signalguard-rs/phase-3/control/STATUS.md`
- `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-RERUN-AFTER-R3-LOCAL.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-AFTER-R3-BLOCKER/7dab5647d322339f5bd9d0514e5178522d5181c0.md`
- `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-RERUN-AFTER-R3-BLOCKER-REVIEW.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-AFTER-R3-BLOCKER-REVIEW/7dab5647d322339f5bd9d0514e5178522d5181c0.md`

Accepted blocker publication:

- connector commit: `e83b4cfeb5c6b334eb94b833c39e666dc27450e7`
- blocker report blob: `e4e222259996fafac7c8fc8a20b3f4630772a255`
- status: `P3_CHECKPOINT_2R_RERUN_AFTER_R3_BLOCKED`

Independent blocker review publication:

- connector commit: `e24851c157c0708c1a44641d462d924206aa1847`
- review report blob: `1a1ae7eb5829591b051e58afb8d69cd4418467fd`
- status: `P3_CHECKPOINT_2R_RERUN_AFTER_R3_BLOCKER_ACCEPTED_R4_REQUIRED`

The independent review accepted the causal classification as:

`MP18R stale mode/symbol replacement and selected-symbol ownership regression`

## Local repository and branch

Local repository:

`/Users/anion/Desktop/work/git-signalguard-rs/signalguard-rs`

Assigned worker branch:

`p3/checkpoint2r-selected-symbol-ownership`

Use a fresh dedicated worktree from the exact immutable base. Suggested path:

`/Users/anion/Desktop/work/git-signalguard-rs/worktrees/p3-checkpoint2r-r4-selected-symbol`

Required single product commit message:

`fix(ui): reconcile modal symbol on mode change`

One recovery micro-phase means one worker branch and exactly one product commit.

## Exact writable product lease

Exactly these two tracked product paths are writable:

Production:

`web/src/pages/DashboardPage.tsx`

Tests:

`web/src/pages/DashboardPage.popup.test.tsx`

No other tracked product path is writable.

The final base-to-worker diff must contain exactly these paths, unless the test file does not require a byte change because the required regression already exists at the immutable base. In normal execution both paths are expected to change.

No file may be added, deleted, or renamed.

## Accepted defect

At the immutable base, Dashboard modal replacement uses local popup identity `{ mode, symbol, returnContext }` and nested anomaly detail retains the same parent identity.

The relevant replacement effect first reconciles the popup mode and then reconciles the symbol only under a `!modeChanged` guard.

This creates the accepted deterministic failure:

`Demo/BTCUSDT → Live/BTCUSDT → Live/ETHUSDT → Demo`

with Symbol Detail / nested anomaly state open.

Expected after the final transition:

- mode ownership: `demo`;
- Demo's resolved stored selected symbol: `BTCUSDT`;
- nested Live anomaly UUID cleared;
- open Symbol Detail parent identity: `demo:BTCUSDT:<preserved returnContext>`;
- no ETHUSDT content retained in the open Demo-owned modal.

Accepted failing behavior at the base:

- header mode: Demo;
- header symbol: `BTCUSDT`;
- nested Live anomaly UUID clears;
- open Symbol Detail parent becomes `demo:ETHUSDT:<returnContext>`;
- modal still renders ETHUSDT content.

## Required implementation semantics

Make the smallest safe correction inside the existing Dashboard modal identity replacement/reconciliation logic.

Required behavior:

1. When selected UI mode changes while Symbol Detail or nested symbol-owned anomaly detail is open, derive the replacement parent identity atomically from:
   - the new `selectedUiMode`; and
   - that mode's already resolved `selectedSymbol`, when non-null.
2. Mode replacement must not suppress same-cycle selected-symbol reconciliation.
3. If both mode and symbol need replacement, the resulting parent identity must contain both new values in one state transition.
4. Preserve the existing `returnContext` exactly.
5. Any stale nested symbol-owned anomaly UUID must continue to be cleared by collapsing to Symbol Detail when parent identity changes.
6. Existing same-mode symbol replacement must remain correct.
7. Existing mode-only replacement where the selected symbol remains the same must remain correct.
8. Do not introduce a second source of selected-symbol truth or duplicate per-mode selection storage.
9. Do not move modal state into the URL or router.
10. Do not change resource-query ownership. `useSymbolPopupResource` must continue to consume the supplied exact popup identity.

The independent review established that the existing selected-symbol hook, AppShell header ownership, popup identity helpers, and popup resource layer already provide the correct primitives. Do not modify those files.

Do not solve the defect with arbitrary delays, timers, forced remount hacks, page reloads, direct DOM mutation, or by closing the modal on mode change.

## Required regression test

In `web/src/pages/DashboardPage.popup.test.tsx`, add a deterministic regression covering the composed per-mode selection sequence with Symbol Detail and nested detail open:

`Demo/BTCUSDT → Live/BTCUSDT → Live/ETHUSDT → Demo/BTCUSDT`

The regression must prove at minimum:

- Demo and Live maintain separate stored selected-symbol ownership;
- Demo/BTC → Live/BTC clears the stale Demo nested UUID as required;
- Live/BTC → Live/ETH clears the stale BTC nested UUID as required;
- after a Live ETH nested detail is open, Live/ETH → Demo returns the open Symbol Detail parent to Demo/BTCUSDT, not Demo/ETHUSDT;
- the stale Live ETH UUID is absent;
- ETHUSDT modal content is absent after Demo ownership resolves to BTCUSDT;
- active popup/resource identity is Demo/BTCUSDT;
- the original Symbol Detail `returnContext` is preserved;
- no late old-mode or old-symbol resource can reattach stale content.

Keep existing R1/R2/R3 and MP18R regression tests intact.

## Strictly forbidden adjacent scope

Do not modify:

- `web/src/features/dashboard/selectedSymbol.ts`;
- `web/src/app/AppShell.tsx`;
- `web/src/features/dashboard/symbolPopup.ts`;
- `web/src/features/dashboard/symbolPopupResource.ts`;
- any route/router/navigation file;
- URL-backed modal behavior;
- CSS, styling, responsive layout, copy, or visual redesign;
- R1 View-all reachability logic except for executing existing tests;
- R2 Back-focus/focus-return logic except for executing existing tests;
- R3 favicon/static assets or `web/index.html`;
- MP20R presentation/formatting adapters or view models;
- ticker code or ticker ownership;
- API/resource schemas, query definitions, OpenAPI or backend Rust code;
- package manifests, lockfiles, dependencies, Cargo manifests;
- bundle-size budgets or bundle scripts;
- Docker, migrations, replay/service behavior;
- Bridge01/Bridge02, semantic Wave 4, or any later work.

Do not opportunistically refactor DashboardPage outside the exact replacement logic needed for this defect.

## Focused test validation

Before the complete gates, run the exact popup test file with the new regression and prove all tests in that file pass.

Use the repository's existing test runner without changing package scripts or test configuration.

Then run the complete frontend test suite to ensure the fix does not regress R1/R2/MP18R behavior.

## Focused real-browser recovery proof

After the focused test passes, build and run a fresh isolated production frontend/backend environment from the worker commit with a real Chrome context and real Demo/Live resources.

Do not mock frontend API resources, selected-symbol storage, mode state, popup resources, or browser navigation to force acceptance.

Execute the exact accepted failure sequence on both required viewports:

- desktop `1440×900`;
- mobile `390×844`.

Sequence:

1. Fresh `/dashboard` in Demo with Demo selected/stored `BTCUSDT`.
2. Open All Markets → BTCUSDT Symbol Detail → exact available Demo BTC anomaly detail.
3. Switch to Live through the real application mode control behavior.
4. Prove nested Demo UUID clears and parent becomes `live:BTCUSDT:symbols`.
5. Open an exact available Live BTC anomaly.
6. Switch selected Live symbol to `ETHUSDT` through the real application behavior.
7. Prove nested BTC UUID clears and parent becomes `live:ETHUSDT:symbols`.
8. Open an exact available Live ETH anomaly.
9. Switch to Demo through the real application mode control behavior.
10. Prove atomically:
    - header mode = Demo;
    - header symbol = BTCUSDT;
    - stale Live ETH UUID absent;
    - open parent identity = `demo:BTCUSDT:symbols`;
    - modal heading/content = BTCUSDT;
    - ETHUSDT content absent;
    - pathname remains `/dashboard` and no modal identity enters the URL.

Also prove on both viewports:

- zero unexpected console errors;
- zero page errors;
- zero unhandled promise rejections;
- zero transport failures attributable to the recovery;
- `/favicon.ico` request count remains `0`;
- no Demo fallback is presented as Live;
- modal close/body-lock behavior remains intact in the exercised flow.

Capture deterministic focused evidence outside both repositories, including at least:

- one screenshot after the final corrected desktop transition;
- one screenshot after the final corrected mobile transition;
- a structured identity/error/request log for the sequence.

Record SHA-256 hashes in the implementation report.

This focused browser proof is not a substitute for the later full Checkpoint 2R rerun.

## Full frontend gates

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

- 25/25 bundle-policy tests;
- no fewer than 44 frontend test files;
- frontend test count must not decrease from the accepted 614-test baseline and should increase by the added regression;
- zero frontend test failures;
- typecheck pass;
- ESLint pass with zero warnings;
- production build pass;
- bundle-budget pass;
- bundle budget limits remain exactly `409600 / 409600 / 414720` bytes.

Do not raise a bundle budget.

Record actual test counts and actual initial/largest/total JS measurements rather than assuming they are unchanged.

## Full root/global gates

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
git diff --check
```

All commands must pass. Declared service-dependent ignored tests remain ignored exactly as designed.

## Exact diff and residual audit

Before commit prove:

- only the two writable lease paths differ from the immutable base;
- no added/deleted/renamed files;
- no package/lock/budget/config change;
- no route/CSS/API/backend/favicon/ticker change;
- `git diff --check` passes.

After commit prove:

- exactly one product commit ahead of `7dab5647d322339f5bd9d0514e5178522d5181c0`;
- zero commits behind;
- merge base exactly the immutable base;
- direct parent exactly the immutable base;
- commit message exactly `fix(ui): reconcile modal symbol on mode change`;
- effective diff contains only the exact writable lease paths;
- worker tree is clean apart from intentionally external validation artifacts, which must remain outside the repository.

## Delivery

Push only:

`p3/checkpoint2r-selected-symbol-ownership`

Do not open a pull request.

Do not merge anything.

Do not modify `refactor/dashboard-modules`.

Publish the implementation report to:

`signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R4-SELECTED-SYMBOL/<PRODUCT_COMMIT_SHA>.md`

Connector report commit message:

`docs(phase-3): publish Checkpoint 2R R4 implementation`

The report must include:

- exact contract identity;
- exact immutable base SHA/tree;
- worker branch/commit/tree/message/parent;
- exact two-file diff and concise behavioral explanation;
- regression-test description and actual focused/full test counts;
- focused desktop/mobile real-browser evidence for the exact accepted sequence;
- identity/error/request-log and screenshot hashes;
- confirmation of preserved returnContext, stale UUID clearing, no stale ETHUSDT content, and Demo/BTCUSDT final ownership;
- confirmation of zero `/favicon.ico` requests in focused proof;
- every frontend/root gate result;
- actual bundle measurements and unchanged limits;
- final branch relation and repository cleanliness;
- confirmation that no PR/merge was created;
- confirmation that no adjacent scope or later work began.

Do not update `CURRENT_EXECUTION.md` or `STATUS.md` from the implementation worker.

## Terminal status

Return exactly:

`P3_CHECKPOINT_2R_R4_SELECTED_SYMBOL_COMPLETE`

only if the exact two-file recovery, required regression, focused desktop/mobile browser proof, all prescribed gates, exact commit/branch identity, push, and connector report publication succeed.

Otherwise return exactly:

`P3_CHECKPOINT_2R_R4_SELECTED_SYMBOL_BLOCKED`

On any new deterministic product defect, do not expand the lease or repair it without a new orchestrator contract.