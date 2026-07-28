# P3-MP10-WEB2 — Timeline Panel Replacement

Status: `IMMUTABLE_WEB_WORKER_EXECUTION_CONTRACT`

## Identity

- Product repository: `progeranna/signalguard-rs`
- Connector repository: `progeranna/connector`
- Replacement branch: `p3/mp10-timeline-panel-r1`
- PR base: `refactor/dashboard-modules`
- Exact assigned base SHA: `93a870010730c458417ccfff392cb97aff23d6c9`
- Required commit message: `feat(ui): add timeline panel component`
- Required draft PR title: `feat(ui): add timeline panel component`

## Rejected immutable execution

The prior WEB1 execution is rejected evidence:

- branch: `p3/mp10-timeline-panel`
- head: `9bddc301d32c51bbb54dc5058d8d33320c144ff7`
- PR: `#36`, closed and unmerged
- CI: `30367741374`, frontend failure
- delivery report: absent

Do not modify, amend, reset, rebase, force-push, merge, or add a corrective commit to that branch. Do not copy its test file blindly.

## Goal

Recreate the current inline dashboard timeline/chart and selected-market snapshot as a standalone presentation component with focused tests, without wiring `DashboardPage.tsx`.

## Authorized paths

Add only:

1. `web/src/features/dashboard/TimelinePanel.tsx`
2. `web/src/features/dashboard/TimelinePanel.test.tsx`

No existing product file may change.

## Required API and ownership

Export a readonly props type and `TimelinePanel`.

The component must receive all selected-market, timeline-resource, retry, and explicit empty-anchor values through props. It must not own API/query hooks, selected-symbol resolution, routing, popup state, storage, source fallback, or current time.

Reuse the accepted owners:

- `normalizeTimelinePoints` from `timelineNormalization.ts`;
- `buildTimelineDomains` from `timelineDomains.ts`.

Do not duplicate normalization or domain policy. Never call `Date.now()` or derive current time internally.

## Binding presentation

Use the current inline timeline/chart and snapshot presentation in `DashboardPage.tsx` at the exact assigned base as source of truth. Preserve current:

- loading, no-market, non-observed, error, loading-timeline, normalized-empty, and chart states;
- copy and status wording;
- Live/Demo source badge;
- highest anomaly badge;
- Recharts structure, gradient, axes, domains, grid, tooltip, reference lines, area styling, and disabled animation;
- anomaly-marker filtering to the accepted time domain;
- inclusive ±15-second tooltip anomaly matching;
- selected-market snapshot layout and Price, Spread, Trades/min, Freshness metrics;
- zero-value behavior, formatting, responsive grid, borders, spacing, and classes.

Do not introduce Wave 4 vocabulary, new tooltips, CSS, copy, fields, icons, or behavior.

## Required regression correction

The WEB1 focused test contains an incorrect expected price domain.

For normalized prices `100` and `102`, the accepted P3-MP06 formula is:

```text
range = 2
magnitude = 102
padding = max(2 * 0.08, 102 * 0.002, 0.01)
        = 0.204
domain = [99.796, 102.204]
```

The replacement tests must expect exactly `[99.796, 102.204]`. They must not expect `[99.84, 102.16]` or reimplement a partial padding formula.

Add at least one further assertion proving the magnitude branch wins when it exceeds range padding.

## Required tests

Cover at least:

1. summary loading precedence;
2. no-market presentation;
3. configured, awaiting, and unavailable states;
4. observed error before loading/chart;
5. observed loading before empty/chart;
6. invalid normalized points produce current empty state;
7. accepted normalization and exact price/time domains;
8. explicit empty-anchor/no-current-time ownership;
9. in-domain anomaly markers and severity colors;
10. highest anomaly badge behavior;
11. tooltip facts, zero values, and inclusive ±15-second matching;
12. source badge and snapshot metrics;
13. input immutability and determinism;
14. current classes/copy and forbidden dependency absence;
15. no caller wiring or ownership leakage.

Use explicit assertions rather than snapshots alone.

## Forbidden scope

Do not modify or wire:

- `DashboardPage.tsx`;
- accepted normalization/domain files or tests;
- other Wave 2 component leases;
- pages, routes, popup/modal composition, CSS/global styles;
- API/query/resource/adapter/identity files;
- package/lock/config files;
- backend, OpenAPI, CI, Docker, deployment, or scripts;
- upper ticker or ticker CSS/behavior.

Do not start P3-MP15.

## Verification before publication

Run focused tests and all repository frontend/global gates when available. Prove:

- exact two-path scope;
- exactly one product commit;
- `git diff --check` or honest equivalent;
- accepted normalization/domain imports;
- no current-time/browser/query ownership;
- unchanged `DashboardPage.tsx`, ticker, accepted models, CSS, package/config, backend, and CI paths.

## Remote post-publication hardening

After pushing the one product commit, but before opening the PR:

1. Fetch both committed files from GitHub using the exact final product SHA.
2. Record both remote blob SHAs.
3. Verify complete UTF-8/TSX content from first to last line.
4. Verify the corrected `[99.796, 102.204]` expectation is present remotely.
5. Verify the rejected `[99.84, 102.16]` expectation is absent.
6. Verify exact base-to-head diff contains only the two authorized paths.
7. Require successful exact-head/current-base GitHub Actions CI, including frontend tests, typecheck, lint, build, bundle budget, and Rust/global job.
8. Stop without further branch mutation if content corruption or any gate failure appears.

Only after those checks pass, open one draft PR:

- head: `p3/mp10-timeline-panel-r1`
- base: `refactor/dashboard-modules`
- title: `feat(ui): add timeline panel component`

Publish one immutable connector report at:

`signalguard-rs/phase-3/reports/P3-MP10/<FINAL_PRODUCT_HEAD_SHA>.md`

The report must include replacement identity, rejected-head quarantine, exact paths, component API, render-state matrix, accepted-owner usage, corrected domain evidence, remote blobs, full CI, unavailable checks, final divergence, and forbidden-path/ticker proof.

## Prohibited operations

Do not merge, amend, rebase, reset, squash, force-push, rewrite history, modify the phase branch directly, or start another microphase.
