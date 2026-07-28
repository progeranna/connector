# P3-MP13-WEB1 — Recent Anomalies Desktop Table

Status: `IMMUTABLE_WEB_WORKER_EXECUTION_CONTRACT`

## Identity

- Product repository: `progeranna/signalguard-rs`
- Connector repository: `progeranna/connector`
- Product branch: `p3/mp13-recent-anomalies-desktop`
- PR base: `refactor/dashboard-modules`
- Exact assigned base SHA: `01bf6edae2795a5e118148ad7b291a285a70a8d8`
- Required commit message: `feat(ui): add recent anomalies desktop table`
- Required draft PR title: `feat(ui): add recent anomalies desktop table`

## Goal

Create the desktop-only Recent Anomalies preview table component and focused tests. This task extracts current presentation only and must not modify dashboard composition, mobile cards, section title, loading/empty shell, view-all action, all-anomalies modal, data logic, semantic vocabulary, or CSS.

## Authorized paths

Add only:

1. `web/src/features/dashboard/RecentAnomaliesDesktopTable.tsx`
2. `web/src/features/dashboard/RecentAnomaliesDesktopTable.test.tsx`

No existing product file may change.

## Required API

Export:

- a readonly props type;
- `RecentAnomaliesDesktopTable`.

Accept:

- readonly `RecentAnomaliesPreviewRow[]` from accepted P3-MP08;
- `onOpenSymbolDetail(symbol: string)` callback.

Do not accept raw dashboard summaries and do not own anomaly ordering, duplicate detection, preview limits, hidden counts, stable identity creation, or detector/severity policy.

## Binding presentation

Use the current desktop Recent Anomalies preview table in `DashboardPage.tsx` at exact assigned base as the source of truth.

Preserve exactly:

- desktop-only wrapper hidden below `lg` and shown at `lg`;
- horizontal overflow/overscroll and border structure;
- `aria-label="Recent anomalies"`;
- fixed table layout and current six-column widths;
- exact columns and order: Time, Market, Type, Severity, Observed, Threshold;
- row focusability, `role="button"`, click behavior, Enter and Space activation with preventDefault;
- exact accessible label `Open <SYMBOL> market detail`;
- current timestamp formatting from event time with created-at fallback;
- current market and detector/type typography;
- current compact severity badge wording, classes, and tones;
- current observed and threshold formatting by anomaly type;
- current severity-dependent observed-value text class;
- current hover/focus classes and row separators.

Use accepted row `id` as React identity, never array index, symbol, message, or timestamp.

## Current visible formatting

Preserve current output. Do not implement Wave 4 tooltip or severity-description changes.

- detector/type label must use accepted `detectorLabel`;
- severity visible label remains accepted capitalized severity label;
- event time uses original `eventTime` when truthy, otherwise `createdAt`; invalid time preserves current fallback behavior;
- null/undefined/NaN numeric values render `—`;
- `spread_spike` and `price_move`: three decimal places plus `%`;
- `event_lag_spike`, `stale_data`, `quote_stuck`: current duration formatting;
- `trade_burst`: current integer plus ` /m`;
- `depth_sequence_gap`: current integer plus `gap` for observed and `limit` for threshold;
- unknown detectors use current numeric formatting.

Do not add Context/message, Detected at, source badge, combined active label, severity explanation, tooltip, icons, or columns; those belong to other views or later waves.

## Accepted model ownership

Consume `RecentAnomaliesPreviewRow` from `recentAnomaliesPreviewModel.ts`.

Do not reorder, slice, mutate, reparse identity, reject duplicates locally, or replace accepted descriptor fields. Do not introduce mode/source fallback.

## Required tests

Cover at least:

1. exact aria label, columns, colgroup widths, and desktop-only classes;
2. rows preserve supplied order;
3. row identity is UUID and never index;
4. click callback symbol;
5. Enter activation;
6. Space activation and preventDefault;
7. exact accessible row label;
8. event-time display and created-at fallback;
9. known and unknown detector labels from accepted model;
10. all three severity labels/classes;
11. zero and negative observed/threshold preservation through formatting;
12. formatting for percentage, duration, trade burst, depth gap, and generic values;
13. null values render `—`;
14. no reordering, limiting, duplicate policy, or mutation;
15. no mobile cards, section header, loading/empty shell, view-all action, or modal markup;
16. no Wave 4 explanatory copy/tooltips;
17. no query/API/router/popup/time-now/random/network dependency.

Use explicit assertions rather than snapshots alone.

## Forbidden scope

Do not modify or wire:

- `DashboardPage.tsx`;
- MP14 mobile component lease;
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

`signalguard-rs/phase-3/reports/P3-MP13/<FINAL_PRODUCT_HEAD_SHA>.md`

The report must include component API, exact display/interaction parity, formatting matrix, accepted-model ownership, tests/CI, changed paths, ticker proof, unavailable checks, and final divergence.

Do not merge, amend, rebase, reset, squash, or force-push.
