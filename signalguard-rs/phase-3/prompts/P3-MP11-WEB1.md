# P3-MP11-WEB1 — Market Health Desktop Table

Status: `IMMUTABLE_WEB_WORKER_EXECUTION_CONTRACT`

## Identity

- Product repository: `progeranna/signalguard-rs`
- Connector repository: `progeranna/connector`
- Product branch: `p3/mp11-market-health-desktop`
- PR base: `refactor/dashboard-modules`
- Exact assigned base SHA: `01bf6edae2795a5e118148ad7b291a285a70a8d8`
- Required commit message: `feat(ui): add market health desktop table`
- Required draft PR title: `feat(ui): add market health desktop table`

## Goal

Create the desktop-only Market Health table component and focused tests. This task extracts presentation only and does not modify dashboard composition, loading/empty shells, section titles, view-all actions, modal tables, mobile cards, data logic, or visible vocabulary.

## Authorized paths

Add only:

1. `web/src/features/dashboard/MarketHealthDesktopTable.tsx`
2. `web/src/features/dashboard/MarketHealthDesktopTable.test.tsx`

No existing product file may change.

## Required API

Export:

- a readonly props type;
- `MarketHealthDesktopTable`.

The component must accept:

- readonly `MarketHealthPreviewRow[]` from the accepted P3-MP07 model;
- `onOpenSymbolDetail(symbol: string)` callback.

Exact prop names may be chosen consistently and documented.

Do not accept raw dashboard summaries and do not own preview ordering, limits, hidden counts, availability coercion, or source identity policy.

## Binding presentation

Use the current desktop Market Health preview table in `DashboardPage.tsx` at the exact assigned base as the source of truth.

Preserve exactly:

- desktop-only root breakpoint behavior: hidden below `lg`, shown at `lg`;
- horizontal overflow/overscroll and border structure;
- `aria-label="Market health"`;
- fixed table layout and current six-column widths;
- column labels and order: Market, Health Score, Last Price, Spread, Trades/min, Status;
- row keyboard semantics: focusable button-role row, Enter and Space activation, preventDefault for activation;
- row click callback with the row symbol;
- exact accessible row label `Open <SYMBOL> market detail`;
- current symbol typography and conditional `View` copy;
- current HealthScore number/bar presentation and tone rules;
- current formatting for price, spread, trades/min, and numeric zero;
- current StatusBadge wording and tones;
- current hover/focus classes and row separators.

Use stable React keys derived from the accepted row identity `key`, not array index.

## Current vocabulary rules

Do not implement Wave 4 terminology. Preserve existing labels:

- observed status is capitalized from current health status or `Unknown`;
- configured -> `Configured`;
- awaiting -> `Awaiting data`;
- unavailable -> `Unavailable`.

For non-observed rows, Health Score, Last Price, Spread, and Trades/min cells remain visually empty, while Status remains visible.

Do not add source badges, tooltips, freshness, icons, colors beyond existing classes, explanatory copy, or new columns.

## Accepted model ownership

Consume `MarketHealthPreviewRow` from `marketHealthPreviewModel.ts`.

Do not:

- reorder rows;
- limit/slice rows;
- recalculate identity;
- inspect hiddenCount/hasMore;
- fabricate metrics;
- synthesize Demo fallback;
- change source or availability.

## Required tests

Cover at least:

1. exact table aria label and column order;
2. current colgroup widths/classes;
3. desktop-only root classes;
4. rows render in supplied order;
5. stable row callback symbol on click;
6. Enter activation;
7. Space activation and preventDefault;
8. exact accessible row label;
9. observed score/status/price/spread/trades including zero;
10. current score tone/bar-width rules;
11. configured/awaiting/unavailable metrics remain empty and exact status wording remains visible;
12. no row reordering, limiting, mutation, or fallback;
13. no array-index identity;
14. no section title, loading shell, empty shell, view-all button, modal or mobile markup;
15. no Wave 4 vocabulary/tooltips;
16. no query/API/router/popup/time/random/network dependency.

Use explicit assertions rather than snapshots alone.

## Forbidden scope

Do not modify or wire:

- `DashboardPage.tsx`;
- Market Health mobile component lease;
- accepted P3-MP07 model/tests or market ordering owner;
- all-markets modal markup;
- page/app/router/component/CSS paths outside the two authorized files;
- API/query/resource/adapter/identity/selected-symbol files;
- status descriptors, fixtures, shared Tooltip, smoke matrix;
- package/lock/config files;
- backend, OpenAPI, CI, Docker, deployment, scripts;
- upper ticker or ticker CSS/behavior.

Do not start P3-MP15.

## Verification and publication

Run focused tests and all frontend/global gates when available. Prove exact two-path scope, `git diff --check`, forbidden paths, and unchanged ticker blob.

Create exactly one normal commit, push without rewriting history, open one draft PR to `refactor/dashboard-modules`, and publish:

`signalguard-rs/phase-3/reports/P3-MP11/<FINAL_PRODUCT_HEAD_SHA>.md`

The report must include component API, exact visual/interaction parity, row-state matrix, model ownership, tests/CI, changed paths, ticker proof, unavailable checks, and final divergence.

Do not merge, amend, rebase, reset, squash, or force-push.
