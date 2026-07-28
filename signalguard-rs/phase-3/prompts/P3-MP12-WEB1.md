# P3-MP12-WEB1 — Market Health Mobile Cards

Status: `IMMUTABLE_WEB_WORKER_EXECUTION_CONTRACT`

## Identity

- Product repository: `progeranna/signalguard-rs`
- Connector repository: `progeranna/connector`
- Product branch: `p3/mp12-market-health-mobile`
- PR base: `refactor/dashboard-modules`
- Exact assigned base SHA: `01bf6edae2795a5e118148ad7b291a285a70a8d8`
- Required commit message: `feat(ui): add market health mobile cards`
- Required draft PR title: `feat(ui): add market health mobile cards`

## Goal

Create the mobile-only Market Health cards component and focused tests. This is presentation extraction only. Do not modify dashboard composition, desktop table, section title, loading/empty shells, view-all action, modal list, data logic, or visible vocabulary.

## Authorized paths

Add only:

1. `web/src/features/dashboard/MarketHealthMobileCards.tsx`
2. `web/src/features/dashboard/MarketHealthMobileCards.test.tsx`

No existing product file may change.

## Required API

Export:

- a readonly props type;
- `MarketHealthMobileCards`.

Accept:

- readonly `MarketHealthPreviewRow[]` from accepted P3-MP07;
- `onOpenSymbolDetail(symbol: string)` callback.

Do not accept raw dashboard summaries or own sorting, limits, source isolation, availability coercion, or preview metadata.

## Binding presentation

Use the current mobile Market Health preview cards in `DashboardPage.tsx` at exact assigned base as the source of truth.

Preserve exactly:

- mobile-only wrapper visible below `lg` and hidden at `lg`;
- divide-y and border structure;
- one full-width button per row;
- exact accessible label `Open <SYMBOL> market detail`;
- callback with the row symbol;
- current symbol typography;
- exact `View market detail` copy;
- current StatusBadge position, wording, and tone;
- observed HealthScore number/bar presentation and tone rules;
- observed two-column metric grid with Price, Spread, Trades/min, Age;
- exact price/spread/trades/age formatting, including zero;
- configured/awaiting/unavailable cards omit score and metric grid and show the exact current availability message in the current empty-block styling;
- current hover/focus classes and spacing.

Use accepted row `key` as React identity, never array index.

## Current wording

Do not implement Wave 4 semantic changes.

Status labels remain:

- observed current health status capitalized or `Unknown`;
- `Configured`;
- `Awaiting data`;
- `Unavailable`.

Availability messages remain exactly:

- configured: `Configured for Live; Live ingestion is not active.`
- awaiting: `Awaiting first Live market data.`
- unavailable: `Live market data is unavailable.`
- observed fallback: `No current market state available for this market.`

Do not rename `Age`, add Data Age semantics, source badges, tooltips, new copy, icons, or fields.

## Accepted model ownership

Consume `MarketHealthPreviewRow` from `marketHealthPreviewModel.ts`.

Do not reorder, slice, deduplicate, mutate, reconstruct identity, fabricate metrics, or introduce Demo/Live fallback.

## Required tests

Cover at least:

1. mobile-only wrapper classes;
2. cards preserve supplied order;
3. stable identity from row key, never index;
4. exact accessible button label;
5. click callback symbol;
6. exact symbol and `View market detail` copy;
7. observed status, score, and all four metrics including numeric zero;
8. health-score tone and bar-width rules;
9. configured exact status/message and no metrics;
10. awaiting exact status/message and no metrics;
11. unavailable exact status/message and no metrics;
12. no sorting, limiting, mutation, synthesis, or source fallback;
13. no desktop table, section header, loading/empty shell, view-all action, or modal markup;
14. no Wave 4 vocabulary/tooltips;
15. no query/API/router/popup/time/random/network dependency.

Use explicit DOM assertions rather than snapshots alone.

## Forbidden scope

Do not modify or wire:

- `DashboardPage.tsx`;
- MP11 desktop component lease;
- accepted P3-MP07 model/tests or ordering owner;
- all-markets modal;
- any CSS/global style;
- other components/pages/routes;
- API/query/resource/adapter/identity files;
- status descriptors, fixtures, shared Tooltip, smoke matrix;
- package/lock/config files;
- backend, OpenAPI, CI, Docker, deployment, scripts;
- upper ticker or ticker CSS/behavior.

Do not start P3-MP15.

## Verification and publication

Run focused tests and all available frontend/global gates. Prove exact two-path scope, diff hygiene, forbidden paths, and unchanged ticker blob.

Create exactly one normal commit, push without history rewriting, open one draft PR to `refactor/dashboard-modules`, and publish:

`signalguard-rs/phase-3/reports/P3-MP12/<FINAL_PRODUCT_HEAD_SHA>.md`

The report must include component API, visual/state parity, accepted-model usage, interaction evidence, tests/CI, changed paths, ticker proof, unavailable checks, and final divergence.

Do not merge, amend, rebase, reset, squash, or force-push.
