# P3-MP11-WEB5 — Binding Scope

Product: `progeranna/signalguard-rs`

Branch: `p3/mp11-market-health-desktop-r4`

Exact base: `025921919fa923abff1366bea01e9a502c088d22`

Required commit: `feat(ui): add market health desktop table`

Add only:

- `web/src/features/dashboard/MarketHealthDesktopTable.tsx`
- `web/src/features/dashboard/MarketHealthDesktopTable.test.tsx`

Export `MarketHealthDesktopTableProps` and `MarketHealthDesktopTable`.

Preserve the accepted desktop-only six-column Market Health table, widths, supplied order, `row.key`, click and keyboard activation, accessible labels, score-first Health Score tones, numeric formatting, zero and missing values, availability states, and current classes.

Typed `healthStatus` fixtures are limited to `healthy`, `degraded`, `unhealthy`, and `null`. Neutral/Unknown uses `null`.

The component owns no sorting, limiting, mutation, deduplication, synthesis, query, route, network, modal, source coercion, or Demo/Live fallback.

DashboardPage, ticker, integrated MP12/MP13/MP14 files, packages, configuration, routes, APIs, backend, CI, Docker, scripts, and other worker leases remain unchanged. P3-MP15 does not start.
