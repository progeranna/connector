# P3-MP15 — Binding Scope

## Identity

- Product: `progeranna/signalguard-rs`
- Branch: `p3/mp15-dashboard-compositor`
- PR base: `refactor/dashboard-modules`
- Exact base: `455a0bf15fbf7df2ecac9dbeb95e2a6dba7f8b73`
- Required commit: `refactor(ui): wire dashboard feature components`

## Exact path lease

Modify only:

1. `web/src/pages/DashboardPage.tsx`
2. `web/src/pages/DashboardPage.test.tsx`

No other product path may change. No new product file may be added.

Base blobs:

- `DashboardPage.tsx`: `deb2eee919938d3b1807e353d309c046b08ba6f5`
- `DashboardPage.test.tsx`: `a5db497f99fc2ebfdf08b46cb070176a95f22067`
- upper ticker: `727f591706a60327b3b219f3287b153a06d1160d`

## Accepted components to wire

Use the already integrated components without modifying them:

- `TimelinePanel` from `@/features/dashboard/TimelinePanel`
- `MarketHealthDesktopTable` from `@/features/dashboard/MarketHealthDesktopTable`
- `MarketHealthMobileCards` from `@/features/dashboard/MarketHealthMobileCards`
- `RecentAnomaliesDesktopTable` from `@/features/dashboard/RecentAnomaliesDesktopTable`
- `RecentAnomaliesMobileCards` from `@/features/dashboard/RecentAnomaliesMobileCards`

Accepted production blobs:

- Timeline: `ba89c4f707a76b1abe531011c293bc61dee3a606`
- Market Health desktop: `e57f8562f3b23a2a1f364f7709c49bf3f140b589`
- Market Health mobile: `767715b55cd5be4da438763a82c71755fb1a6bb5`
- Recent Anomalies desktop: `8a634c6493842e26688ebf99921cca97eac0800a`
- Recent Anomalies mobile: `92be317139a738a24e0694f50893ed6756f34bc9`

## Accepted model owners

Use the already integrated model owners:

- `buildMarketHealthPreview` from `@/features/dashboard/marketHealthPreviewModel`
- `buildRecentAnomaliesPreview` from `@/features/dashboard/recentAnomaliesPreviewModel`
- timeline normalization and domain calculation remain owned inside the accepted `TimelinePanel` through its accepted helpers

Do not recreate sorting, limiting, row adaptation, timestamp normalization, chart domains, anomaly labels, severity descriptors or stable identity in `DashboardPage.tsx`.

## Required compositor structure

### Timeline

Keep `MarketTimelineShell` as the query/controller boundary. It continues to:

- resolve the selected market from the current summary and selected symbol;
- preserve the current `useMarketTimelineQuery(symbol, selectedUiMode, observed)` identity and enablement;
- preserve error-message construction and retry behavior;
- preserve Demo/Live and symbol isolation.

Replace its inline timeline/chart/snapshot presentation with one `TimelinePanel` call using:

- `selectedMarket` — the exact resolved summary entry or `null`;
- `timelinePoints` — raw `timelineQuery.data?.points ?? []`;
- `timelineAnomalies` — raw `timelineQuery.data?.anomalies ?? []`;
- `isSummaryLoading` — the existing summary-loading input;
- `isTimelineLoading` — the timeline query loading state;
- `timelineErrorMessage` — existing `buildErrorMessage` output on timeline error, otherwise `null`;
- `onRetryTimeline` — existing refetch callback;
- `emptyAnchorMs` — an explicit finite current-time anchor owned by the shell/compositor, not by `TimelinePanel`.

Preserve the existing effective empty-domain behavior. Do not add timers, effects or local state solely for the anchor. Do not move current-time ownership into `TimelinePanel`.

After wiring, remove only dead timeline presentation imports/types/helpers from `DashboardPage.tsx`, including direct Recharts ownership and duplicate timeline normalization/domain/tooltip/marker helpers, when they are no longer referenced. Do not remove similarly named helpers still used by popup, modal or full-detail presentation.

### Market Health preview

Keep `SymbolHealthShell` as the section/loading/empty/view-all controller.

- Build one preview with `buildMarketHealthPreview(summary?.symbols ?? [])`.
- Use `preview.hasMore` for the existing `View all` action visibility.
- Use `preview.isEmpty` for the existing empty state.
- Pass the same `preview.rows` in the same order to both desktop and mobile components.
- Preserve the exact section title, subtitle, loading skeleton, empty copy and callback.
- Preserve full raw `symbols` for the all-markets modal and popup workflows outside the preview shell.

Remove only the now-dead inline desktop row, mobile card and preview-only Health Score/metric helpers when no remaining modal/detail code uses them.

### Recent Anomalies preview

Keep `RecentAnomaliesShell` as the section/loading/empty/view-all controller.

- Build one preview with `buildRecentAnomaliesPreview(summary?.recent_anomalies ?? [])`.
- Use `preview.hasMore` for the existing `View all` action visibility.
- Use `preview.isEmpty` for the existing empty state.
- Pass the same `preview.rows` in the same order to both desktop and mobile components.
- Preserve the exact section title, subtitle, loading skeleton, empty copy and callback.
- Preserve full raw anomalies for the all-anomalies modal and popup/detail workflows outside the preview shell.

Remove only dead inline anomaly preview table/card/formatting helpers. Preserve any helpers still used by all-anomalies, symbol-detail or popup presentation.

### Dashboard composition and dialogs

Preserve exactly:

- `DashboardPage` summary query ownership;
- selected-symbol resolution and persistence;
- `DashboardTablesGrid` two-column composition;
- modal state and return contexts;
- all-markets modal;
- all-anomalies modal;
- symbol detail popup;
- popup identity and mode replacement;
- `View all` behavior;
- row/card click behavior;
- loading, error, empty, unavailable and success behavior;
- current section order and responsive composition.

## Visible-behavior freeze

This task is extraction wiring only. Do not change:

- any visible label, subtitle, message or tooltip;
- table/card columns, widths or order;
- classes or CSS semantics;
- chart structure, marker colors, domains or tooltip matching;
- score/status/severity formatting;
- preview limits or ordering;
- modal or popup behavior;
- Demo/Live semantics;
- symbol identity;
- current routes;
- upper ticker text, structure, order, animation or CSS.

## Forbidden scope

Do not modify accepted components, accepted models, APIs, queries, adapters, resources, selected-symbol modules, popup modules, shared UI, CSS, routes, packages, lockfiles, TypeScript/Vite/Vitest configuration, backend, OpenAPI, CI, Docker, deployment or scripts.

Do not start P3-MP16 or any later micro-phase.

The worker does not merge.