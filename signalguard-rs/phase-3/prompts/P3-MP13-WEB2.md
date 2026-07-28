# P3-MP13-WEB2 — Recent Anomalies Desktop Table Replacement

Status: `IMMUTABLE_WEB_WORKER_REPLACEMENT_CONTRACT`

## Identity

- Product repository: `progeranna/signalguard-rs`
- Connector repository: `progeranna/connector`
- Replacement branch: `p3/mp13-recent-anomalies-desktop-r1`
- PR base: `refactor/dashboard-modules`
- Exact assigned base SHA: `93a870010730c458417ccfff392cb97aff23d6c9`
- Required commit message: `feat(ui): add recent anomalies desktop table`
- Required draft PR title: `feat(ui): add recent anomalies desktop table`

## Superseded WEB1

- Original branch: `p3/mp13-recent-anomalies-desktop`
- Remote state: identical to original assigned base, no product commit, no PR, no connector report.
- Status: `STALLED_NO_REMOTE_DELIVERY_SUPERSEDED`
- Recovery control: `signalguard-rs/phase-3/control/P3-MP13-RECOVERY.md`

Do not use or modify the original branch. Use a new web-worker chat and only the replacement branch.

## Goal and authorized paths

Create the desktop-only Recent Anomalies preview table component and focused tests. Add only:

1. `web/src/features/dashboard/RecentAnomaliesDesktopTable.tsx`
2. `web/src/features/dashboard/RecentAnomaliesDesktopTable.test.tsx`

No existing product file may change.

Export a readonly props type and `RecentAnomaliesDesktopTable`. Accept readonly `RecentAnomaliesPreviewRow[]` and `onOpenSymbolDetail(symbol: string)`. Do not accept raw dashboard summaries.

## Binding presentation

Use the current desktop Recent Anomalies preview table in `DashboardPage.tsx` at the exact assigned base as source of truth. Preserve exactly:

- desktop-only wrapper hidden below `lg`, shown at `lg`;
- overflow/overscroll and border structure;
- `aria-label="Recent anomalies"`;
- fixed six-column layout and current widths;
- Time, Market, Type, Severity, Observed, Threshold order;
- focusable button-role rows, click, Enter and Space activation with `preventDefault()`;
- exact accessible label `Open <SYMBOL> market detail`;
- accepted UUID `row.id` identity and supplied order;
- event-time display with created-at fallback;
- accepted detector label and severity descriptor label/tone;
- current compact severity badge classes;
- current anomaly-type value formatting and severity-dependent observed text class;
- current hover/focus classes and separators.

Consume accepted model fields directly. Do not reorder, slice, limit, mutate, reject duplicates locally, rebuild identity, replace descriptors, synthesize mode/source behavior, or own preview metadata.

Do not add Context/message, Detected at, source badges, active labels, explanations, tooltips, icons, extra columns, mobile cards, section shells, modal markup, Wave 4 vocabulary, or caller wiring.

## Required tests

Use explicit DOM assertions covering:

1. aria label, columns, widths and desktop wrapper classes;
2. supplied order and UUID-keyed reconciliation;
3. exact accessible labels and callbacks;
4. click, Enter, Space and default prevention;
5. event-time and created-at fallback, invalid/falsy timestamp behavior;
6. known and unknown accepted detector labels;
7. info/warning/critical labels and classes;
8. zero, negative, null, undefined and NaN values;
9. percentage, duration, trade-burst, depth-gap and generic formatting;
10. no order/limit/duplicate/mutation ownership;
11. absence of mobile/shell/modal/context/Wave 4/external dependencies.

Tests must not use overbroad whole-source guards that reject unrelated string operations. Scope ownership assertions to the `rows` collection and relevant APIs.

## Forbidden scope

Do not modify `DashboardPage.tsx`, accepted P3-MP08 model/descriptors, integrated MP14 component, MP10/MP11/MP12 leases, all-anomalies modal, CSS, routes/pages, API/query/resource/adapter/identity files, Tooltip, fixtures, packages/configuration, backend, OpenAPI, CI, Docker, scripts, deployment, or the upper ticker. Do not start P3-MP15.

## Execution and hardening

1. Verify replacement branch equals exact assigned base with divergence `0 0`.
2. Work only on the replacement branch.
3. Run focused and full available gates before commit.
4. Create exactly one normal product commit and push normally.
5. Fetch both committed files back from GitHub by exact final SHA; verify complete UTF-8/TSX, remote blob identities and complete test inventory.
6. Verify exact two-path diff and unchanged integrated MP14 blobs.
7. Require full exact-head/current-merge-tree GitHub Actions success: frontend tests, typecheck, lint, build, bundle budget, and Rust/global gates.
8. On corruption or any red/skipped required gate, stop without further branch mutation and do not claim completion.
9. Only after successful hardening, open one draft PR from `p3/mp13-recent-anomalies-desktop-r1` to `refactor/dashboard-modules`.
10. Publish `signalguard-rs/phase-3/reports/P3-MP13/<FINAL_PRODUCT_HEAD_SHA>.md`.

The report must include superseded-WEB1 evidence, exact API/presentation matrix, model ownership, remote read-back, complete gates, paths, MP14/ticker proof, unavailable checks, and divergence.

Do not merge, amend, reset, rebase, squash, or force-push.
