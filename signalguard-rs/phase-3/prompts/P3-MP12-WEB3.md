# P3-MP12-WEB3 — Market Health Mobile Cards Replacement

Status: `IMMUTABLE_WEB_WORKER_REPLACEMENT_CONTRACT`

## Identity

- Product repository: `progeranna/signalguard-rs`
- Connector repository: `progeranna/connector`
- Replacement branch: `p3/mp12-market-health-mobile-r2`
- PR base: `refactor/dashboard-modules`
- Exact assigned base SHA: `93a870010730c458417ccfff392cb97aff23d6c9`
- Required commit message: `feat(ui): add market health mobile cards`
- Required draft PR title: `feat(ui): add market health mobile cards`

## Quarantined prior executions

### WEB1

- Branch: `p3/mp12-market-health-mobile`
- Head: `e2b13831be4bda00c4d6a554e583abfc877b82c9`
- PR: `#35` — closed, unmerged
- Failure: incorrect score-tone expectation

### WEB2

- Branch: `p3/mp12-market-health-mobile-r1`
- Head: `ae19b372943f890c9f0ec18bc85143e366dadef1`
- PR: `#39` — closed, unmerged
- CI: `30369207184` — frontend typecheck failed; lint/build/bundle skipped
- Failure: invalid test fixture `healthStatus: "info"`
- Review: `signalguard-rs/phase-3/reviews/P3-MP12/ae19b372943f890c9f0ec18bc85143e366dadef1.md`
- Recovery: `signalguard-rs/phase-3/control/P3-MP12-WEB2-RECOVERY.md`

Do not modify, reopen, repair, amend, reset, rebase, force-push, merge, or add commits to either quarantined branch.

## Goal and authorized paths

Create the mobile-only Market Health cards component and focused tests. Add only:

1. `web/src/features/dashboard/MarketHealthMobileCards.tsx`
2. `web/src/features/dashboard/MarketHealthMobileCards.test.tsx`

No existing product file may change.

Export a readonly props type and `MarketHealthMobileCards`. Accept readonly `MarketHealthPreviewRow[]` and `onOpenSymbolDetail(symbol: string)`. Do not accept raw summaries or preview metadata.

## Binding presentation

Use the current mobile Market Health cards in `DashboardPage.tsx` at the exact assigned base as source of truth. Preserve exactly:

- mobile-only `lg:hidden` wrapper with current divide-y/border structure;
- one full-width native button per supplied row;
- exact accessible label and symbol callback;
- accepted `row.key` identity and supplied order;
- current symbol typography and `View market detail` copy;
- StatusBadge placement, wording, and tone;
- observed Health Score number/bar and current score-first tone precedence;
- observed Price, Spread, Trades/min and Age grid and formatting;
- exact configured, awaiting, unavailable and observed-fallback messages and empty-block classes;
- current spacing, hover, and focus classes.

Do not sort, slice, limit, deduplicate, mutate, synthesize metrics, inspect preview metadata, change source/availability, or provide Demo/Live fallback.

Do not add desktop, section-shell, modal, tooltip, source badge, icon, Wave 4 vocabulary, or caller wiring.

## Required tests and regression prevention

Cover every P3-MP12 presentation and ownership requirement with explicit DOM assertions.

### Binding score-tone precedence

1. `status === "healthy"` or finite/non-null score `>= 80` → healthy/green;
2. otherwise `status === "degraded"` or score `>= 50` → degraded/amber;
3. otherwise `status === "unhealthy"` or score `< 50` → unhealthy/rose;
4. otherwise neutral.

Required mixed/boundary cases include:

- `healthStatus: "degraded"`, `healthScore: 95` → healthy/green score tone while StatusBadge remains Degraded/amber;
- `healthStatus: "unhealthy"`, `healthScore: 90` → healthy/green;
- `healthStatus: "healthy"`, low score → healthy/green;
- null status with 80/50/49/0 boundaries.

### WEB2 typecheck regression prevention

All `MarketHealthPreviewRow` fixtures must be valid under the accepted type.

For `healthStatus`, use only:

```text
"healthy" | "degraded" | "unhealthy" | null
```

Never use `"info"`, `"warning"`, `"critical"`, `"unknown"`, or another out-of-domain literal as `healthStatus`.

Test the visible `Unknown` status with `healthStatus: null`.

Do not bypass the accepted type with `as any`, `as unknown as`, `@ts-ignore`, `@ts-expect-error`, an untyped fixture helper, or a widened string cast.

The focused test source itself must pass the repository TypeScript compiler.

## Forbidden scope

Do not modify `DashboardPage.tsx`, accepted models, ordering owner, MP10/MP11/MP13/MP14 files, modals, CSS, routes/pages, API/query/resource/adapter/identity files, fixtures, Tooltip, packages/configuration, backend, OpenAPI, CI, Docker, scripts, deployment, or the upper ticker. Do not start P3-MP15.

## Execution and hardening

1. Verify `p3/mp12-market-health-mobile-r2` equals exact assigned base with divergence `0 0`.
2. Work only on the replacement branch.
3. Run focused tests and all available frontend/global gates before commit.
4. Before publication, perform a strict TypeScript validation that includes both the production component and focused test source. Explicitly prove no out-of-domain `healthStatus` literal exists.
5. Create exactly one normal product commit and push normally.
6. Fetch both committed files back from GitHub by exact final SHA; verify complete UTF-8/TSX, remote blob identities, complete test inventory, corrected precedence cases, and absence of invalid health-status fixtures.
7. Verify exact two-path diff and unchanged accepted model/ticker blobs.
8. Open one draft PR from `p3/mp12-market-health-mobile-r2` to `refactor/dashboard-modules` to trigger authoritative CI.
9. Require complete exact-head/current-merge-tree GitHub Actions success:
   - frontend tests;
   - frontend typecheck;
   - frontend lint;
   - frontend build;
   - frontend bundle budget;
   - Rust/global job.
10. On corruption or any red/skipped required gate, stop without additional branch mutation and do not claim completion.
11. Only after all required gates are green, publish `signalguard-rs/phase-3/reports/P3-MP12/<FINAL_PRODUCT_HEAD_SHA>.md`.

The report must include both quarantines, exact state/presentation matrix, score-tone precedence, type-safe fixture inventory, remote read-back, complete gates, exact paths, ticker proof, unavailable checks, and divergence.

Do not merge, amend, reset, rebase, squash, or force-push.
