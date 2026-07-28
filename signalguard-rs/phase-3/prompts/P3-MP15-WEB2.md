# P3-MP15-WEB2 — Dashboard compositor recovery

This is the immutable replacement execution contract for SignalGuard RS Phase 3 microphase P3-MP15.

## Contract identity

- Connector repository: `progeranna/connector`
- Contract path: `signalguard-rs/phase-3/prompts/P3-MP15-WEB2.md`
- Binding original scope: `signalguard-rs/phase-3/prompts/P3-MP15-SCOPE.md`
- Binding original verification: `signalguard-rs/phase-3/prompts/P3-MP15-VERIFICATION.md`
- Binding recovery: `signalguard-rs/phase-3/control/P3-MP15-WEB1-RECOVERY.md`
- Binding WEB1 review: `signalguard-rs/phase-3/reviews/P3-MP15/WEB1-BLOCKED-REQUIRED-GATES-UNAVAILABLE.md`
- Binding Wave 2 closure: `signalguard-rs/phase-3/control/WAVE_2_CLOSURE.md`

Read every binding file completely before any product write. This replacement contract overrides only the unavailable-local-gate execution order. Product scope, behavior, path ownership, integrity, CI, review, integration and visual-acceptance requirements remain unchanged.

## Product identity

- Product repository: `progeranna/signalguard-rs`
- Worker branch: `p3/mp15-dashboard-compositor-r1`
- PR base: `refactor/dashboard-modules`
- Exact assigned base: `455a0bf15fbf7df2ecac9dbeb95e2a6dba7f8b73`
- Required product commit: `refactor(ui): wire dashboard feature components`

Before any product write verify the replacement branch is exactly:

```text
ahead 0
behind 0
```

## Superseded WEB1

- Branch: `p3/mp15-dashboard-compositor`
- State: stopped before mutation
- Final divergence: `0 0`
- Product commits: `0`
- PR: none

Do not modify, continue, publish from, reset, rebase, force-push, merge or open a PR from the WEB1 branch.

## Exact product lease

Modify only:

- `web/src/pages/DashboardPage.tsx`
- `web/src/pages/DashboardPage.test.tsx`

Do not add another product path. Do not modify accepted components, accepted models, ticker, routes, APIs, resources, packages, configuration, backend, OpenAPI, CI, Docker, deployment or scripts.

## Mission

Replace duplicated inline dashboard presentation with the five accepted integrated components:

- `TimelinePanel`
- `MarketHealthDesktopTable`
- `MarketHealthMobileCards`
- `RecentAnomaliesDesktopTable`
- `RecentAnomaliesMobileCards`

Use the accepted model owners:

- `buildMarketHealthPreview`
- `buildRecentAnomaliesPreview`

This is compositor wiring only. Preserve query/data ownership, selected-symbol behavior, Demo/Live and symbol isolation, routes, dialogs, popup return contexts, View-all actions, labels, messages, tooltips, classes, responsive layout and all user-visible behavior.

## Timeline wiring

Keep `MarketTimelineShell` as the controller boundary. It must continue to:

- resolve the selected market using the existing selected-symbol policy;
- compute `observed` from the exact selected market availability;
- call `useMarketTimelineQuery(selectedMarket?.symbol ?? null, selectedUiMode, observed)`;
- preserve exact mode/symbol query identity;
- preserve the current retry callback and error formatting.

Render `TimelinePanel` with exactly:

- `selectedMarket={selectedMarket}`;
- `timelinePoints={timelineQuery.data?.points ?? []}`;
- `timelineAnomalies={timelineQuery.data?.anomalies ?? []}`;
- `isSummaryLoading={isLoading}`;
- `isTimelineLoading={timelineQuery.isLoading}`;
- `timelineErrorMessage={timelineQuery.isError ? buildErrorMessage(timelineQuery.error) : null}`;
- `onRetryTimeline={() => void timelineQuery.refetch()}`;
- a finite explicit `emptyAnchorMs` derived from existing query metadata.

Use the existing TanStack Query metadata as the deterministic anchor:

```ts
const emptyAnchorMs = Number.isFinite(timelineQuery.dataUpdatedAt)
  ? timelineQuery.dataUpdatedAt
  : 0;
```

Passing `timelineQuery.dataUpdatedAt` directly is acceptable if its repository type is a guaranteed finite number. Do not call `Date.now`, create zero-argument `new Date`, add state/effects/timers for the anchor, or move time ownership into `TimelinePanel`.

Remove the now-dead direct Recharts imports and duplicate inline timeline normalization/domain/tooltip/marker presentation only after the accepted component is wired. Do not remove helpers still used by full dialogs, popup/detail presentation or other page sections.

## Market Health wiring

Inside the existing Market Health shell/controller:

```ts
const preview = buildMarketHealthPreview(symbols);
```

Use:

- `preview.rows` for both `MarketHealthDesktopTable` and `MarketHealthMobileCards`;
- `preview.hasMore` for the existing View-all action visibility;
- `preview.isEmpty` for the existing empty state;
- the existing exact symbol callback for both components.

Preserve full raw `symbols` for the all-markets dialog, symbol-detail popup, selected-symbol validation and every existing full-collection workflow.

Do not separately sort, slice or remap the preview rows in the page.

## Recent Anomalies wiring

Inside the existing Recent Anomalies shell/controller:

```ts
const preview = buildRecentAnomaliesPreview(anomalies);
```

Use:

- `preview.rows` for both `RecentAnomaliesDesktopTable` and `RecentAnomaliesMobileCards`;
- `preview.hasMore` for the existing View-all action visibility;
- `preview.isEmpty` for the existing empty state;
- the existing exact symbol callback for both components.

Preserve full raw `anomalies` for the all-anomalies dialog, symbol popup/detail workflows and every existing full-collection use.

Do not separately sort, slice, deduplicate or remap preview rows in the page.

## Dead inline presentation

Remove only code made genuinely dead by the five accepted components and two accepted preview builders, including where applicable:

- direct dashboard Recharts imports and inline chart JSX;
- duplicate timeline chart-point/domain/visible-marker/tooltip helpers;
- inline Market Health desktop row and mobile card presentation;
- inline Recent Anomalies desktop row and mobile card presentation;
- duplicate preview constants and preview-only formatters no longer referenced.

Do not remove or change code used by:

- all-markets or all-anomalies dialogs;
- symbol-detail popup or route-compatible view models;
- modal state and return contexts;
- `SectionTitle`, `EmptyBlock` or formatters still used elsewhere;
- full-dialog rows/cards;
- selected-symbol persistence;
- error formatting;
- mode/symbol isolation.

## Focused compositor tests

Update only `DashboardPage.test.tsx`. Replace obsolete assertions that require inline tables/cards with architecture-aware assertions.

The focused test must prove at least:

1. all five accepted components are imported from their accepted modules;
2. both accepted preview builders are imported and called;
3. `MarketTimelineShell` retains the symbol/mode-scoped query call;
4. `TimelinePanel` receives selected market, raw points, raw anomalies, both loading states, formatted error/null, retry callback and finite query-metadata anchor;
5. no `Date.now`, zero-argument `new Date`, timer or new anchor state/effect is added for compositor wiring;
6. Market Health desktop/mobile receive the same `preview.rows`;
7. Recent Anomalies desktop/mobile receive the same `preview.rows`;
8. View-all visibility uses `preview.hasMore`;
9. empty rendering uses `preview.isEmpty`;
10. the equal shrink-safe two-column grid remains;
11. existing section titles/subtitles/messages remain;
12. all-markets, all-anomalies and symbol-detail modal/popup entry points remain;
13. full raw collections still feed modal/detail workflows;
14. direct Recharts imports and inline dashboard chart implementation are removed;
15. old inline preview table/card component declarations are removed;
16. accepted component/model implementation is not copied into the page;
17. upper ticker, routes, Demo/Live and popup behavior are outside the diff.

Use narrow source assertions. Do not reject legitimate full-dialog or symbol-detail table/card code that intentionally remains in `DashboardPage.tsx`.

## Corrected gate order

### Before product commit

Run every check available in the execution environment. At minimum perform and record:

- exact branch/base/divergence verification;
- exact two-path lease audit;
- complete UTF-8 read/parse of both intended files;
- TypeScript/TSX syntax or transpilation checks available without a checkout;
- deterministic source-contract checks for all wiring requirements;
- import/export and prop-shape checks against exact accepted remote component/model sources;
- no forbidden path or accepted-blob mutation;
- no conflict markers or trailing whitespace;
- pre-publication Git blob identities for both leased files;
- exact intended line counts;
- no `any`, `@ts-ignore`, `@ts-expect-error` or type-bypass introduced;
- no direct Recharts ownership remaining in the page;
- no duplicate inline accepted presentation remaining;
- `DashboardPage.tsx` still contains all modal/popup/controller entry points.

Dependency-backed local commands may be recorded as unavailable when the environment genuinely lacks a checkout/dependencies/network. They must not be claimed as passed. Their unavailability alone does not block the one allowed candidate commit in WEB2, provided no available check failed.

Any actual failed available check is a hard stop before commit.

### Publication

1. Create exactly one normal product commit with the required message.
2. Push normally to `p3/mp15-dashboard-compositor-r1` without amend, reset, rebase, squash or force-push.
3. Fetch both committed files back by exact final product SHA.
4. Require exact equality with pre-publication Git blob identities.
5. Verify complete UTF-8/TSX content and repeat source/integrity checks against remote bytes.
6. Verify exact one-commit/two-path scope.
7. Verify all accepted component/model/ticker blobs are unchanged.
8. Only after remote integrity succeeds, open one draft PR to `refactor/dashboard-modules`.

### Authoritative completion gate

Require the exact current-phase PR merge ref to pass every repository GitHub Actions gate:

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
- demo and smoke script syntax.

No required gate may be red, cancelled, unavailable or skipped.

If CI fails or any remote-integrity/scope check fails, stop without another product mutation and do not claim completion.

Only after complete green CI publish:

`signalguard-rs/phase-3/reports/P3-MP15/<FINAL_PRODUCT_HEAD_SHA>.md`

## Final response

Return:

- final product SHA and parent;
- draft PR number and URL;
- exact changed paths;
- pre-publication and remote blob SHAs/equality;
- before/after page and test line counts;
- complete wiring matrix;
- timeline query and anchor proof;
- preview builder and same-row wiring proof;
- View-all/empty/modal/popup preservation;
- dead inline presentation removed;
- available pre-commit checks and precisely unavailable local commands;
- complete PR merge-ref CI run, jobs and exact tested SHA;
- accepted component/model/ticker blob preservation;
- final divergence;
- connector report path and commit;
- blockers or unavailable checks;
- exact status `CODE_COMPLETE_AWAITING_INTEGRATION_AND_USER_UI_CHECK`.

Do not merge. Do not start P3-MP16. Do not claim `USER_UI_ACCEPTED`.
