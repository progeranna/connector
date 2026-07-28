# P3-MP10-WEB3 — Timeline Panel Diagnostic Replacement

Status: `IMMUTABLE_WEB_WORKER_EXECUTION_CONTRACT`

## Identity

- Product repository: `progeranna/signalguard-rs`
- Connector repository: `progeranna/connector`
- Replacement branch: `p3/mp10-timeline-panel-r2`
- PR base: `refactor/dashboard-modules`
- Exact assigned base SHA: `144ca95ae0338cfcf5ae00bd1cccd8317dbbc0b0`
- Required product commit message: `feat(ui): add timeline panel component`
- Required draft PR title: `feat(ui): add timeline panel component`

## Immutable rejected executions

### WEB1

- Branch: `p3/mp10-timeline-panel`
- Head: `9bddc301d32c51bbb54dc5058d8d33320c144ff7`
- PR: `#36`, closed and unmerged
- CI: `30367741374`, frontend tests failed
- Known defect: incorrect expected price domain `[99.84, 102.16]`

### WEB2

- Branch: `p3/mp10-timeline-panel-r1`
- Head: `0ad34843578670d8b313af4f7f53853195c305a9`
- Assigned base: `93a870010730c458417ccfff392cb97aff23d6c9`
- Orchestrator-opened PR: `#41`, closed and unmerged
- Current-tree merge ref: `cc19e0cf6c5179e25e2d35970694808c43331c1f`
- CI: `30372209086`
- Frontend job: `90318715688`, tests failed; typecheck/lint/build/bundle were skipped
- Rust job: `90318715655`, complete success
- Review: `signalguard-rs/phase-3/reviews/P3-MP10/0ad34843578670d8b313af4f7f53853195c305a9.md`
- Recovery: `signalguard-rs/phase-3/control/P3-MP10-WEB2-RECOVERY.md`

Do not modify, reopen, amend, reset, rebase, merge, force-push, or add commits to either rejected branch. Do not blindly copy either rejected test file.

## Stage 0 — mandatory exact diagnosis before product write

Before modifying the product repository, identify the exact failing test and assertion from WEB2 current-tree CI.

Required evidence targets:

- PR `#41`
- workflow run `30372209086` (`CI` run `#208`)
- frontend job `90318715688`
- merge ref `cc19e0cf6c5179e25e2d35970694808c43331c1f`

Use one or more of:

1. complete GitHub Actions frontend job log;
2. GitHub check annotations or UI failure details;
3. faithful local checkout/reproduction of the exact merge ref;
4. a faithful reconstruction of the exact merge tree from parents `144ca95ae0338cfcf5ae00bd1cccd8317dbbc0b0` and `0ad34843578670d8b313af4f7f53853195c305a9`, followed by the repository-native focused/full test command.

Record:

- exact test file;
- exact test name;
- exact assertion or runtime error;
- expected value/behavior;
- actual value/behavior;
- whether the defect is in production code, test code, test infrastructure, or integration with the current phase tree;
- the evidence source used.

Do not infer the failure merely from source inspection or from the fact that a test looks suspicious.

### Diagnostic hard stop

If the exact failure cannot be identified or faithfully reproduced, stop before any product write. Publish only:

`signalguard-rs/phase-3/reports/P3-MP10/WEB3-DIAGNOSTIC-30372209086.md`

The diagnostic report must list every evidence path attempted and state why it was insufficient. Do not create a product commit, do not move the replacement branch, and do not open a PR.

## Stage 1 — product goal after successful diagnosis

Only after Stage 0 succeeds, recreate the current inline dashboard timeline/chart and selected-market snapshot as a standalone presentation component with focused tests, without wiring `DashboardPage.tsx`.

## Authorized product paths

Add only:

1. `web/src/features/dashboard/TimelinePanel.tsx`
2. `web/src/features/dashboard/TimelinePanel.test.tsx`

No existing product file may change.

## Required API and ownership

Export:

- `TimelinePanel`
- readonly `TimelinePanelProps`

The component must receive through props:

- selected market;
- timeline points;
- timeline anomalies;
- summary loading state;
- timeline loading state;
- timeline error message;
- retry callback;
- explicit empty-domain anchor.

Reuse accepted owners:

- `normalizeTimelinePoints` from `timelineNormalization.ts`;
- `buildTimelineDomains` from `timelineDomains.ts`.

Do not duplicate normalization or domain policy. Never call `Date.now()` or derive current time internally. Do not own API/query hooks, selected-symbol resolution, routing, popup state, storage, source fallback, or resource fetching.

## Binding presentation

Use the inline timeline/chart and snapshot in `web/src/pages/DashboardPage.tsx` at exact assigned base `144ca95ae0338cfcf5ae00bd1cccd8317dbbc0b0` as the binding source of truth.

Preserve exactly:

- summary-loading precedence;
- no-market presentation;
- configured, awaiting, and unavailable presentation;
- observed error, loading, normalized-empty, and chart precedence;
- all current copy and status wording;
- Live/Demo source badge;
- highest anomaly badge;
- Recharts structure, gradient, axes, accepted domains, grid, tooltip, reference lines, area styling, and disabled animation;
- anomaly-marker filtering to the accepted time domain;
- inclusive ±15-second tooltip anomaly matching;
- snapshot Price, Spread, Trades/min, and Freshness metrics;
- zero-value behavior;
- current formatting, responsive grid, borders, spacing, and classes.

Do not introduce Wave 4 vocabulary, new tooltips, CSS, copy, fields, icons, or behavior.

## Required domain regression

For normalized prices `100` and `102`, accepted P3-MP06 behavior is exactly:

```text
range = 2
magnitude = 102
padding = max(2 * 0.08, 102 * 0.002, 0.01) = 0.204
domain = [99.796, 102.204]
```

Tests must expect `[99.796, 102.204]`, must not expect `[99.84, 102.16]`, and must prove that magnitude padding wins in this case.

## Required focused tests

Cover with explicit assertions:

1. exact Stage 0 regression for the diagnosed WEB2 failure;
2. summary-loading precedence;
3. no-market presentation;
4. configured, awaiting, and unavailable states;
5. observed error before loading/chart;
6. observed loading before normalized-empty/chart;
7. invalid normalized points produce current empty state;
8. accepted normalization and exact price/time domains;
9. explicit anchor and no-current-time ownership;
10. in-domain anomaly markers and severity colors;
11. highest anomaly badge;
12. tooltip facts, zero values, and inclusive ±15-second matching;
13. source badge and snapshot metrics;
14. input immutability and deterministic rendering;
15. current classes/copy and forbidden-dependency absence;
16. no caller wiring or ownership leakage.

Do not use source-string assertions as the sole evidence for user-visible behavior when a DOM assertion is possible. Avoid brittle assertions that depend on formatting or escaped Tailwind selector syntax when an equivalent stable DOM/class-token assertion is available.

## Forbidden scope

Do not modify or wire:

- `DashboardPage.tsx`;
- accepted normalization/domain files or tests;
- integrated MP13 or MP14 files;
- other Wave 2 component leases;
- pages, routes, popup/modal composition, CSS/global styles;
- API/query/resource/adapter/identity files;
- package/lock/configuration files;
- backend, OpenAPI, CI, Docker, deployment, or scripts;
- upper ticker or ticker behavior.

Do not start P3-MP15.

## Execution and publication

1. Verify `p3/mp10-timeline-panel-r2` equals exact assigned base `144ca95ae0338cfcf5ae00bd1cccd8317dbbc0b0` with divergence `0 0`.
2. Complete Stage 0 before any product write.
3. Work only on the replacement branch.
4. Add only the two authorized paths.
5. Run the diagnosed focused regression and the complete focused TimelinePanel test file.
6. Run repository frontend tests, typecheck, lint, build, bundle budget, and Rust/global gates when available before commit.
7. Create exactly one normal product commit with the required message.
8. Push normally without rewriting history.
9. Fetch both files back from GitHub by exact final SHA; verify complete UTF-8/TSX and record remote blob SHAs.
10. Verify the exact diff contains only the two authorized additions and exactly one commit.
11. Open one draft PR from `p3/mp10-timeline-panel-r2` to `refactor/dashboard-modules`.
12. Require complete green current-phase PR CI: frontend tests, typecheck, lint, build, bundle budget, and Rust/global job.
13. If any required gate is red or skipped, stop without further product-branch mutation and do not claim completion.
14. After complete green CI, publish:

`signalguard-rs/phase-3/reports/P3-MP10/<FINAL_PRODUCT_HEAD_SHA>.md`

The delivery report must include the complete Stage 0 diagnosis and evidence, exact paths, component API, state matrix, accepted-owner use, domain regression, remote blobs, full gates, current-tree merge ref, divergence, forbidden paths, integrated MP13/MP14 preservation, ticker proof, and unavailable checks.

## Prohibited operations

Do not merge, amend, reset, rebase, squash, force-push, rewrite history, modify the phase branch directly, or start another microphase.
