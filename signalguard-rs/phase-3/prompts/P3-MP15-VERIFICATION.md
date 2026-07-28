# P3-MP15 — Binding Verification

## Initial identity

Before any product write:

- verify `p3/mp15-dashboard-compositor` points exactly to `455a0bf15fbf7df2ecac9dbeb95e2a6dba7f8b73`;
- verify divergence from the assigned base is `ahead 0 / behind 0`;
- verify the working tree is clean;
- verify the current blobs of both leased files equal the binding scope.

## Required focused tests

Update `web/src/pages/DashboardPage.test.tsx` to test the new compositor source contract rather than requiring inline copies of extracted presentation.

The focused test must prove at least:

1. `DashboardPage.tsx` imports and renders all five accepted components.
2. It imports and calls both accepted preview builders.
3. `MarketTimelineShell` preserves `useMarketTimelineQuery` with selected symbol, UI mode and observed enablement.
4. `TimelinePanel` receives selected market, raw timeline points, raw timeline anomalies, summary loading, timeline loading, error message, retry callback and explicit empty anchor.
5. Market Health desktop and mobile receive the same model-owned `rows` and exact symbol callback.
6. Recent Anomalies desktop and mobile receive the same model-owned `rows` and exact symbol callback.
7. `preview.hasMore` owns both existing View-all visibility decisions.
8. `preview.isEmpty` owns both existing empty decisions.
9. The equal shrink-safe two-column dashboard grid remains.
10. Existing Market Health and Recent Anomalies titles/subtitles and empty copy remain.
11. Modal and popup calls remain present: all markets, all anomalies and symbol detail.
12. Full raw symbols/anomalies remain available to their modals; preview rows are not substituted into modal/detail data.
13. Direct Recharts imports and the inline timeline chart/tooltip/domain implementation are absent from `DashboardPage.tsx` after wiring.
14. Inline preview-only desktop/mobile components are absent after wiring.
15. No accepted component/model implementation is copied into the page.
16. The upper ticker is not imported, modified or recreated in the page.

Avoid brittle global assertions that fail because full-detail modal tables legitimately retain table, metric or severity helpers. Scope source guards to the extracted preview/timeline boundaries.

Do not weaken or delete unrelated existing tests merely to make the compositor pass.

## Behavior and ownership regression

The page and full suite must continue proving:

- Demo and Live remain isolated;
- BTCUSDT and ETHUSDT paths remain valid where existing fixtures cover them;
- selected-symbol persistence remains mode-scoped;
- route and popup workflows remain available;
- row/card activation opens the exact symbol;
- all-markets and all-anomalies actions still open the existing dialogs;
- no preview component owns sorting, limiting, fallback or raw-data adaptation;
- no stale symbol or mode data is introduced;
- no page/route/section/popup is removed.

## Required local gates before commit

Run in this order:

1. focused DashboardPage/compositor tests;
2. full frontend tests;
3. repository TypeScript typecheck;
4. frontend lint;
5. production build;
6. bundle-budget check;
7. complete Rust/global repository gates;
8. `git diff --check`;
9. exact changed-path audit;
10. forbidden-file and repository-hygiene scan.

The build may change measured bundle output but this micro-phase may not modify package/configuration/budget files. Report the measured bundle result honestly.

## Commit and remote integrity

After all available pre-commit gates pass:

1. Create exactly one normal product commit:
   `refactor(ui): wire dashboard feature components`
2. Push normally without amend, rebase, reset, squash or force-push.
3. Fetch both modified files back from GitHub using the exact final product SHA.
4. Record pre-publication and remote Git blob SHAs for both files.
5. Require exact blob equality and complete UTF-8/TSX decoding.
6. Verify the remote source contains all five component imports/usages and both preview builder imports/usages.
7. Verify remote source no longer contains direct Recharts imports or duplicate timeline chart/domain/tooltip implementation.
8. Verify exact base-to-head scope is one commit and exactly the two leased modified paths.
9. Verify every accepted component/model blob and the upper ticker blob remains unchanged.

If any remote-integrity check fails, stop without another product mutation and do not open a PR.

## Draft PR and authoritative CI

Only after remote integrity succeeds, open one draft PR:

- head: `p3/mp15-dashboard-compositor`
- base: `refactor/dashboard-modules`

Require current-phase merge-ref CI to complete successfully with:

- frontend tests;
- TypeScript typecheck;
- frontend lint;
- production build;
- bundle budget;
- Rust formatting;
- generated API contract check;
- OpenAPI validation;
- `cargo check`;
- clippy with warnings denied;
- Rust tests;
- replay target discovery;
- both Docker Compose validations;
- demo and smoke script syntax checks.

No required gate may be red, cancelled, unavailable or skipped.

If the Phase base advances independently, do not rebase or rewrite the worker branch. Validate the exact immutable worker head with the new Phase base through the PR merge ref.

## Connector report

Only after complete green current-phase CI, publish:

`signalguard-rs/phase-3/reports/P3-MP15/<FINAL_PRODUCT_HEAD_SHA>.md`

The report must include:

- contract identity;
- final product SHA and parent;
- exact changed paths;
- pre-publication and remote blob equality;
- before/after `DashboardPage.tsx` line count;
- imports and component wiring matrix;
- timeline prop/data/query ownership proof;
- Market Health preview builder/component wiring proof;
- Recent Anomalies preview builder/component wiring proof;
- View-all, empty-state, modal and popup preservation;
- dead inline presentation removed;
- focused and full frontend results;
- complete Rust/global results;
- exact CI run, jobs and tested merge ref;
- final divergence;
- accepted component/model and ticker blob preservation;
- routes and popup preservation;
- unavailable checks or blockers;
- explicit status `CODE_COMPLETE_AWAITING_INTEGRATION_AND_USER_UI_CHECK`.

## Visual acceptance boundary

The worker must not claim `USER_UI_ACCEPTED`.

After orchestrator review and integration, Visual Checkpoint 1 will be performed separately on the stable preview. It must cover desktop/mobile dashboard composition, timeline, Market Health, Recent Anomalies, View all, row clicks, Demo/Live and BTC/ETH.

## Stop conditions

A red, skipped, unavailable or cancelled required CI gate; unexpected changed path; remote blob mismatch; accepted component/model blob change; ticker change; route/popup removal; or visible-copy/CSS change ends execution without another product mutation.

Do not merge. Do not start P3-MP16.