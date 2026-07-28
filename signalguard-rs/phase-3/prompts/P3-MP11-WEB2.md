# P3-MP11-WEB2 — Market Health Desktop Table Replacement

Status: `IMMUTABLE_WEB_WORKER_REPLACEMENT_CONTRACT`

## Identity

- Product repository: `progeranna/signalguard-rs`
- Connector repository: `progeranna/connector`
- Replacement branch: `p3/mp11-market-health-desktop-r1`
- PR base: `refactor/dashboard-modules`
- Exact assigned base SHA: `93a870010730c458417ccfff392cb97aff23d6c9`
- Required commit message: `feat(ui): add market health desktop table`
- Required draft PR title: `feat(ui): add market health desktop table`

## Quarantined WEB1

- Branch: `p3/mp11-market-health-desktop`
- Head: `3b5e3e0b5efd1ca5291c08cb0d7f9e3ab36ea596`
- Closed PR: `#33`
- Status: `REJECTED_AND_QUARANTINED`
- Recovery control: `signalguard-rs/phase-3/control/P3-MP11-RECOVERY.md`

Do not modify, reset, amend, rebase, merge, reopen, force-push, or add commits to the quarantined branch. It is evidence only.

## Goal and authorized paths

Create the desktop-only Market Health table component and focused tests. Add only:

1. `web/src/features/dashboard/MarketHealthDesktopTable.tsx`
2. `web/src/features/dashboard/MarketHealthDesktopTable.test.tsx`

No existing product file may change.

Export a readonly props type and `MarketHealthDesktopTable`. Accept readonly `MarketHealthPreviewRow[]` and `onOpenSymbolDetail(symbol: string)`. Do not accept raw dashboard summaries.

## Binding presentation

Use the current desktop Market Health preview table in `DashboardPage.tsx` at the exact assigned base as source of truth. Preserve exactly:

- desktop-only `lg:block` breakpoint, overflow/overscroll and border structure;
- `aria-label="Market health"`;
- fixed six-column layout and widths;
- Market, Health Score, Last Price, Spread, Trades/min, Status order;
- focusable button-role rows, click, Enter and Space activation with `preventDefault()`;
- exact accessible label `Open <SYMBOL> market detail`;
- accepted `row.key` identity;
- current symbol/View classes, health-score number/bar and tone precedence;
- price, spread, compact trades/min and zero formatting;
- observed/configured/awaiting/unavailable status wording and classes;
- visually empty metric cells for non-observed rows.

Consume accepted `MarketHealthPreviewRow` values without reordering, limiting, slicing, mutating, identity reconstruction, metric synthesis, hidden-count inspection, source substitution, or Demo fallback.

Do not add section shells, mobile markup, modal markup, freshness, source badges, tooltips, icons, new columns, Wave 4 vocabulary, or caller wiring.

## Required tests and WEB1 regression prevention

Cover every requirement from P3-MP11-WEB1, including structure, columns, supplied order, identity, click/keyboard behavior, score/tone/width rules, metrics, all availability states, no mutation, and forbidden ownership.

The WEB1 failure must not be repeated. Do **not** use a whole-source assertion that rejects every generic `.slice()` call. Ownership tests must target row transformations specifically, for example by rejecting `rows.sort`, `rows.toSorted`, `rows.slice`, `rows.splice`, or `rows.reverse`, while permitting unrelated string capitalization such as `value.slice(1)`.

Preserve the binding score-first tone precedence exactly, including counterintuitive mixed inputs.

## Forbidden scope

Do not modify `DashboardPage.tsx`, accepted models, ordering owner, MP12/MP13/MP14 leases, modals, CSS, pages/routes, API/query/resource/adapter/identity files, fixtures, Tooltip, packages/configuration, backend, OpenAPI, CI, Docker, scripts, deployment, or the upper ticker. Do not start P3-MP15.

## Execution and hardening

1. Verify replacement branch equals exact assigned base with divergence `0 0`.
2. Work only on the replacement branch.
3. Run focused tests and all frontend/global gates before commit when available.
4. Create exactly one normal product commit and push normally.
5. Fetch both committed files back from GitHub by exact final SHA; verify complete UTF-8, valid TSX, correct remote blob identities, and full test inventory.
6. Verify exact base-to-head diff contains only the two authorized paths.
7. Require exact-head/current-merge-tree GitHub Actions success for frontend tests, typecheck, lint, build, bundle budget, and Rust/global gates.
8. If remote content or CI is not fully valid, stop without further branch mutation and do not claim completion.
9. Only after successful hardening, open one draft PR from `p3/mp11-market-health-desktop-r1` to `refactor/dashboard-modules`.
10. Publish `signalguard-rs/phase-3/reports/P3-MP11/<FINAL_PRODUCT_HEAD_SHA>.md`.

The report must include quarantine evidence, exact API/presentation parity, regression-test correction, remote blob read-back, exact paths, complete gates, ticker proof, unavailable checks, and divergence.

Do not merge, amend, reset, rebase, squash, or force-push.
