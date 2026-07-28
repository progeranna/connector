# P3-MP10-WEB1 — Timeline Panel Component

Status: `IMMUTABLE_WEB_WORKER_EXECUTION_CONTRACT`

## Identity

- Product repository: `progeranna/signalguard-rs`
- Connector repository: `progeranna/connector`
- Product branch: `p3/mp10-timeline-panel`
- PR base: `refactor/dashboard-modules`
- Exact assigned base SHA: `01bf6edae2795a5e118148ad7b291a285a70a8d8`
- Required commit message: `feat(ui): add timeline panel component`
- Required draft PR title: `feat(ui): add timeline panel component`

## Goal

Create one independently testable Timeline panel component that reproduces the current inline timeline/chart and selected-market snapshot presentation without modifying or wiring `DashboardPage.tsx`.

This is component extraction only. It must not change visible vocabulary, layout, chart styling, data ownership, source isolation, or query behavior.

## Authorized paths

Add only:

1. `web/src/features/dashboard/TimelinePanel.tsx`
2. `web/src/features/dashboard/TimelinePanel.test.tsx`

No existing product file may change.

## Required component boundary

Export:

- a readonly props type;
- `TimelinePanel`.

The props must be sufficient for the later P3-MP15 compositor to pass, without this component owning query hooks or selected-symbol resolution:

- selected `DashboardSymbolSummary | null`;
- raw readonly `MarketTimelinePoint[]`;
- readonly `DashboardAnomaly[]`;
- summary-loading state;
- timeline-loading state;
- timeline-error message or null;
- timeline retry callback;
- explicit `emptyAnchorMs`.

Exact prop names may be chosen consistently and documented. Do not accept or derive a public Replay mode.

## Required accepted dependencies

Use the accepted ownership modules rather than duplicating their policy:

- `normalizeTimelinePoints` from `timelineNormalization.ts`;
- `buildTimelineDomains` from `timelineDomains.ts`.

These modules and tests are read-only.

The component may use existing Recharts and shared components already present in the repository. Do not add dependencies or modify package files.

## Binding render behavior

Use `DashboardPage.tsx` at exact assigned base as the visual and interaction reference for the existing inline `MarketTimelineShell` and tooltip.

Preserve:

- whole-panel summary loading skeleton;
- selected symbol heading;
- exact `Live` / `Demo` badge behavior;
- highest-severity anomaly badge and existing visible wording;
- configured/awaiting/unavailable messages;
- timeline error panel title `Market timeline unavailable`, supplied error message, and retry action;
- timeline loading skeleton;
- empty observed timeline text `Waiting for market data`;
- selected-symbol-null empty state;
- Recharts AreaChart structure, dimensions, margins, grid, axes, labels, tick formatting, gradient, colors, animation-disabled area, and reference-line styling;
- tooltip timestamp, price, optional spread/trades/freshness facts, and ±15-second anomaly matching;
- anomaly reference lines only when their parsed event/created time falls inside the computed time domain;
- selected-market aside, existing StatusBadge behavior, and exact Price / Spread / Trades/min / Freshness metrics;
- existing current status and availability wording;
- current responsive grid and class semantics.

Do not implement Wave 4 semantic vocabulary. In particular, do not rename `Freshness`, alter anomaly badge wording, add new tooltip copy, or use the future entity-qualified descriptor labels in visible output.

## State precedence

- Summary loading owns the whole panel skeleton.
- With a selected non-observed market, render its availability message; do not expose passed timeline data or error state.
- With an observed selected market: error precedes timeline loading, timeline loading precedes empty points, and valid points render the chart.
- With no selected market, render the existing no-data empty state.
- The snapshot aside must show metrics only for observed availability.

## Determinism and time

- Never call `Date.now()`.
- Never construct an internal empty-domain current-time fallback.
- Pass the explicit `emptyAnchorMs` to accepted domain calculation.
- No timer, sleep, random value, network, cache, store, or environment access.

## Data and source boundaries

- No query hook, API call, selected-symbol hook, popup state, routing, or local storage.
- Preserve selected symbol source exactly.
- No Demo fallback into Live or Live fallback into Demo.
- No market synthesis, normalization beyond accepted timeline normalization, sorting, or mutation.

## Required tests

Use deterministic tests and cover at least:

1. summary loading;
2. no selected market;
3. each non-observed availability state and exact message;
4. observed timeline error and retry;
5. observed timeline loading;
6. observed empty timeline;
7. valid chart rendering from accepted normalization/domain modules;
8. invalid raw points are excluded through accepted normalization;
9. source badge remains Demo or Live exactly;
10. highest anomaly severity badge behavior;
11. visible anomaly reference-line in-domain filtering;
12. tooltip facts and ±15-second anomaly matching;
13. snapshot metric formatting including numeric zero;
14. status badge/current status wording;
15. explicit-anchor use and no current-time access;
16. no query/API/router/popup/storage dependency;
17. no input mutation;
18. current visible copy and key CSS/ARIA structure remain unchanged.

Mock Recharts responsively where necessary, but do not replace component behavior with snapshots only.

## Forbidden scope

Do not modify or wire:

- `web/src/pages/DashboardPage.tsx`;
- any page, router, app shell, popup, dialog, or symbol-detail file;
- any CSS/global style;
- accepted timeline normalization/domain modules or tests;
- Market Health or Recent Anomalies models/components;
- status descriptor, fixture, tooltip, smoke-matrix, API/query/resource/adapter/identity files;
- package/lock/config files;
- backend, OpenAPI, CI, Docker, deployment, scripts, or docs in the product repository;
- `web/src/app/GlobalMarketTicker.tsx` or ticker CSS/behavior.

Do not start P3-MP15 or any later task.

## Verification

Run when available:

- focused TimelinePanel tests;
- `npm run test:run`;
- `npm run typecheck`;
- `npm run lint`;
- `npm run build`;
- `npm run bundle:check`;
- repository/global CI gates;
- `git diff --check`;
- exact two-path and forbidden-path proof;
- upper ticker blob proof.

## Publication workflow

1. Verify assigned branch and phase branch both initially equal exact assigned base.
2. Work only on the assigned branch.
3. Create exactly one normal product commit.
4. Push normally without history rewriting.
5. Open one draft PR from assigned branch to `refactor/dashboard-modules`.
6. Publish one immutable connector report at:

`signalguard-rs/phase-3/reports/P3-MP10/<FINAL_PRODUCT_HEAD_SHA>.md`

The report must include exact base/head, API, render-state matrix, accepted-model usage, copy/style parity evidence, tests/CI, changed paths, forbidden paths, ticker proof, unavailable checks, and final divergence.

## Prohibitions

Do not merge, amend, rebase, reset, squash, force-push, update the phase branch, modify another worker branch, or claim unavailable checks as passed.
