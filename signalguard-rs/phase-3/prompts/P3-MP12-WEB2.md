# P3-MP12-WEB2 — Market Health Mobile Cards Replacement

Status: `IMMUTABLE_WEB_WORKER_REPLACEMENT_CONTRACT`

## Identity

- Product repository: `progeranna/signalguard-rs`
- Connector repository: `progeranna/connector`
- Replacement branch: `p3/mp12-market-health-mobile-r1`
- PR base: `refactor/dashboard-modules`
- Exact assigned base SHA: `93a870010730c458417ccfff392cb97aff23d6c9`
- Required commit message: `feat(ui): add market health mobile cards`
- Required draft PR title: `feat(ui): add market health mobile cards`

## Quarantined WEB1

- Branch: `p3/mp12-market-health-mobile`
- Head: `e2b13831be4bda00c4d6a554e583abfc877b82c9`
- Closed PR: `#35`
- Status: `REJECTED_AND_QUARANTINED`
- Recovery control: `signalguard-rs/phase-3/control/P3-MP12-RECOVERY.md`

Do not modify, reset, amend, rebase, merge, reopen, force-push, or add commits to the quarantined branch.

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

## Required tests and WEB1 regression prevention

Cover every P3-MP12-WEB1 requirement with explicit DOM assertions.

The WEB1 failure must not be repeated. The exact binding tone precedence is:

1. `status === "healthy"` **or** finite/non-null score `>= 80` → healthy/green;
2. otherwise `status === "degraded"` **or** score `>= 50` → degraded/amber;
3. otherwise `status === "unhealthy"` **or** score `< 50` → unhealthy/rose;
4. otherwise neutral.

Therefore tests must assert, among other mixed cases:

- `healthStatus: "degraded"`, `healthScore: 95` → healthy/green;
- `healthStatus: "unhealthy"`, `healthScore: 90` → healthy/green;
- `healthStatus: "healthy"`, low score → healthy/green;
- null status with 80/50/49/0 boundaries follows the exact score rules.

Do not “improve” or reinterpret this precedence in Wave 2.

## Forbidden scope

Do not modify `DashboardPage.tsx`, accepted models, ordering owner, MP11/MP13/MP14 files, modals, CSS, routes/pages, API/query/resource/adapter/identity files, fixtures, Tooltip, packages/configuration, backend, OpenAPI, CI, Docker, scripts, deployment, or the upper ticker. Do not start P3-MP15.

## Execution and hardening

1. Verify replacement branch equals exact assigned base with divergence `0 0`.
2. Work only on the replacement branch.
3. Run focused tests and all frontend/global gates before commit when available.
4. Create exactly one normal product commit and push normally.
5. Fetch both committed files back by exact final SHA; verify complete UTF-8/TSX, remote blob identities, and complete test inventory.
6. Verify exact two-path diff.
7. Require full exact-head/current-merge-tree GitHub Actions success: tests, typecheck, lint, build, bundle budget, and Rust/global job.
8. On corruption or any red/skipped required gate, stop without additional branch mutation and do not claim completion.
9. Only after successful hardening, open one draft PR from `p3/mp12-market-health-mobile-r1` to `refactor/dashboard-modules`.
10. Publish `signalguard-rs/phase-3/reports/P3-MP12/<FINAL_PRODUCT_HEAD_SHA>.md`.

The report must include quarantine evidence, exact state/presentation matrix, corrected precedence tests, remote read-back, complete gates, paths, ticker proof, unavailable checks, and divergence.

Do not merge, amend, reset, rebase, squash, or force-push.
