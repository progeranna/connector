# P3-MP14-WEB1 — Recent Anomalies Mobile Cards

Status: `IMMUTABLE_WEB_WORKER_EXECUTION_CONTRACT`

## Identity

- Product repository: `progeranna/signalguard-rs`
- Connector repository: `progeranna/connector`
- Product branch: `p3/mp14-recent-anomalies-mobile`
- PR base: `refactor/dashboard-modules`
- Exact assigned base SHA: `01bf6edae2795a5e118148ad7b291a285a70a8d8`
- Required commit message: `feat(ui): add recent anomalies mobile cards`
- Required draft PR title: `feat(ui): add recent anomalies mobile cards`

## Goal

Create the mobile-only Recent Anomalies preview cards component and focused tests. This is presentation extraction only. Do not modify dashboard composition, desktop table, section title, loading/empty shell, view-all action, all-anomalies modal, data logic, semantic vocabulary, or CSS.

## Authorized paths

Add only:

1. `web/src/features/dashboard/RecentAnomaliesMobileCards.tsx`
2. `web/src/features/dashboard/RecentAnomaliesMobileCards.test.tsx`

No existing product file may change.

## Required API

Export:

- a readonly props type;
- `RecentAnomaliesMobileCards`.

Accept:

- readonly `RecentAnomaliesPreviewRow[]` from accepted P3-MP08;
- `onOpenSymbolDetail(symbol: string)` callback.

Do not accept raw dashboard summaries and do not own ordering, duplicate-ID rejection, preview limits, hidden counts, stable identity creation, or detector/severity policy.

## Binding presentation

Use the current mobile Recent Anomalies preview cards in `DashboardPage.tsx` at exact assigned base as the source of truth.

Preserve exactly:

- mobile-only wrapper visible below `lg` and hidden at `lg`;
- divide-y and border structure;
- one full-width button per row;
- exact accessible label `Open <SYMBOL> market detail`;
- click callback with row symbol;
- current market typography;
- current detector/type heading;
- current severity badge wording, classes, and position;
- current two-column metric grid with Observed, Threshold, Time, Severity;
- current anomaly-type value formatting;
- current timestamp formatting using event time with created-at fallback;
- current severity-colored text in the Severity metric;
- current spacing, hover, and focus classes.

Use accepted row `id` as React identity, never array index, symbol, message, or timestamp.

## Current visible formatting

Preserve current copy and output. Do not implement Wave 4 severity explanations, combined labels, or tooltips.

- detector/type heading uses accepted `detectorLabel`;
- severity badge and Severity metric use accepted capitalized severity label;
- event time uses original `eventTime` when truthy, otherwise `createdAt`;
- null/undefined/NaN values render `—`;
- `spread_spike` and `price_move`: three decimal places plus `%`;
- lag/stale/quote-stuck values use current duration formatting;
- `trade_burst`: integer plus ` /m`;
- `depth_sequence_gap`: integer plus `gap` or `limit` by role;
- unknown detectors use current generic numeric formatting.

Do not show anomaly context/message in this preview card. Do not add source, detected-at copy, active-label copy, extra fields, icons, or new colors.

## Accepted model ownership

Consume `RecentAnomaliesPreviewRow` from `recentAnomaliesPreviewModel.ts`.

Do not reorder, slice, mutate, reconstruct UUID identity, reject duplicates locally, or replace descriptor fields. Do not synthesize mode/source behavior.

## Required tests

Cover at least:

1. mobile-only wrapper classes;
2. cards preserve supplied order;
3. stable UUID identity, never index;
4. exact accessible button label;
5. click callback symbol;
6. exact market and detector/type output;
7. all severity badge/metric variants;
8. event-time display and created-at fallback;
9. percentage, duration, trade-burst, depth-gap, and generic value formatting;
10. zero and negative observed/threshold values;
11. null values render `—`;
12. exact Observed / Threshold / Time / Severity metric labels;
13. no ordering, limiting, duplicate policy, or mutation;
14. no desktop table, section header, loading/empty shell, view-all action, modal, or context-message markup;
15. no Wave 4 explanatory copy/tooltips;
16. no query/API/router/popup/time-now/random/network dependency.

Use explicit DOM assertions rather than snapshots alone.

## Forbidden scope

Do not modify or wire:

- `DashboardPage.tsx`;
- MP13 desktop component lease;
- accepted P3-MP08 model/tests or descriptor model;
- all-anomalies modal rows/cards;
- any CSS/global style;
- pages/routes/components outside authorized files;
- API/query/resource/adapter/identity files;
- Tooltip, fixtures, smoke matrix;
- package/lock/config files;
- backend, OpenAPI, CI, Docker, deployment, scripts;
- upper ticker or ticker CSS/behavior.

Do not start P3-MP15.

## Verification and publication

Run focused tests and all available frontend/global gates. Prove exact two-path scope, diff hygiene, forbidden paths, and unchanged ticker blob.

Create exactly one normal commit, push without history rewriting, open one draft PR to `refactor/dashboard-modules`, and publish:

`signalguard-rs/phase-3/reports/P3-MP14/<FINAL_PRODUCT_HEAD_SHA>.md`

The report must include component API, exact display/interaction parity, formatting matrix, accepted-model ownership, tests/CI, changed paths, ticker proof, unavailable checks, and final divergence.

Do not merge, amend, rebase, reset, squash, or force-push.
