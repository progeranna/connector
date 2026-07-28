# P3-MP06-WEB1 Contract — Pure Timeline Chart-Domain Calculation

## Execution role

You are an isolated GitHub web implementation worker for SignalGuard RS Phase 3 microphase `P3-MP06`.

Read this immutable contract from `progeranna/connector`, implement the product change in `progeranna/signalguard-rs`, publish one normal product commit to the assigned remote branch, open one draft product PR, and publish one immutable delivery report back to the connector repository.

This is a remote GitHub workflow. Do not assume a user-local path, worktree, Docker service, or local Codex session.

## Immutable identity

- Product repository: `progeranna/signalguard-rs`
- Connector repository: `progeranna/connector`
- Assigned product branch: `p3/mp06-timeline-domains`
- Required PR base: `refactor/dashboard-modules`
- Exact assigned base SHA: `773b110816d10d31e65a36ce2ed76a1b37beca01`
- Required product commit message: `feat(ui): extract timeline chart domains`
- Dependency integration: P3-MP05 resulting SHA `773b110816d10d31e65a36ce2ed76a1b37beca01`
- Accepted normalized-point source: `web/src/features/dashboard/timelineNormalization.ts`

The product branch must contain exactly one normal product commit above the assigned base.

## Ownership boundary

The worker owns implementation, focused tests, one product commit, normal push, one draft PR, and one connector delivery report.

The worker must not merge, edit the phase branch directly, rewrite history, force-push, modify another worker branch, update Phase 3 control files, modify P3-MP05 files, wire the model into a page/component, or start P3-MP10/compositor work.

## Remote preflight

Before editing:

1. Fetch product refs.
2. Verify `origin/refactor/dashboard-modules` equals `773b110816d10d31e65a36ce2ed76a1b37beca01` at initial preflight. If it later advances because another accepted Wave 1 task integrates, preserve this immutable assigned base and follow the moving-base rule below.
3. Verify `origin/p3/mp06-timeline-domains` equals the same exact SHA.
4. Check out only the assigned branch without history rewriting.
5. Verify clean state and comparison `0 0` against the exact assigned base.
6. Read exact-base versions of:
   - `web/src/features/dashboard/timelineNormalization.ts` and its tests;
   - `web/src/pages/DashboardPage.tsx` read-only, especially current price/time domain helpers;
   - `web/src/features/dashboard/types.ts` read-only;
   - Phase 3 Wave 1 requirements and P3-MP05 integration record.
7. Confirm `NormalizedTimelinePoint` still exposes finite `timestampMs` and `price` plus the accepted normalized fields.

Stop and report a blocker if branch identity, exact base, cleanliness, or the accepted normalized-point API differs.

## Goal

Create one pure deterministic chart-domain model for normalized timeline points.

This microphase owns:

- price/Y-domain calculation;
- time/X-domain calculation;
- deterministic empty-time-domain behavior through an explicit supplied anchor;
- finite ascending bounds and duplicate/single-point behavior.

It must not normalize DTO points, calculate visible anomaly markers, format ticks/tooltips, render Recharts, read current time, call queries, or migrate any production caller.

## Required production API

Create a small module exporting consistently documented readonly types and pure functions for:

1. a numeric domain tuple representing `[lower, upper]`;
2. price-domain calculation from `readonly NormalizedTimelinePoint[]`;
3. time-domain calculation from `readonly NormalizedTimelinePoint[]` plus an explicit empty-domain anchor;
4. optionally one combined domain result/function delegating to the same rules without duplicating policy.

The module must import `NormalizedTimelinePoint` as a type only from `./timelineNormalization`.

Recommended names are:

- `TimelineNumericDomain`;
- `buildTimelinePriceDomain`;
- `buildTimelineTimeDomain`;
- `buildTimelineDomains`.

Exact names may vary only if consistent, focused, and documented in the delivery report.

## Binding price-domain semantics

Given normalized points:

1. Empty input returns exactly `[0, 1]`.
2. For non-empty input, calculate `low` and `high` from the minimum and maximum `price` across all points. Do not assume input chronological order and do not use only the first/last point.
3. Calculate:
   - `range = Math.max(high - low, 0.0001)`;
   - `magnitude = Math.max(Math.abs(low), Math.abs(high))`;
   - `padding = Math.max(range * 0.08, magnitude * 0.002, 0.01)`.
4. Return `[low - padding, high + padding]`.
5. The returned bounds must be finite and strictly ascending.
6. If finite normalized inputs nevertheless produce a non-finite or non-ascending bound because of numeric overflow, throw a deterministic `RangeError` with exact message:

   `timeline price domain exceeds finite numeric bounds`

7. Preserve support for zero and negative prices at this pure domain layer.
8. Do not round, clamp to zero, locale-format, or mutate points.

## Binding time-domain semantics

Use one explicit `emptyAnchorMs` argument; never call `Date.now()` or read current time.

1. Empty input:
   - require finite `emptyAnchorMs`;
   - return exactly `[emptyAnchorMs - 60_000, emptyAnchorMs]`;
   - if the anchor or resulting bounds are non-finite/non-ascending, throw `RangeError` with exact message:

     `timeline empty time-domain anchor must produce finite bounds`

2. Non-empty input:
   - derive minimum and maximum `timestampMs` across all points;
   - do not assume input order;
   - ignore `emptyAnchorMs` for domain selection.
3. One point, or multiple points with the same timestamp:
   - return exactly `[timestampMs - 60_000, timestampMs + 60_000]`.
4. Multiple distinct timestamps:
   - return exactly `[minimumTimestampMs, maximumTimestampMs]`.
5. Every returned time domain must be finite and strictly ascending.
6. If point-derived expansion/bounds overflow, throw `RangeError` with exact message:

   `timeline time domain exceeds finite numeric bounds`

7. Do not sort, deduplicate, mutate, or rewrite point timestamps.

## Collection, determinism, and composition rules

- Input order must not affect calculated min/max domains.
- Duplicate points remain permitted and do not change the policy beyond min/max/equal-timestamp behavior.
- Input arrays and point objects remain untouched.
- Equal point values and the same explicit anchor produce equal output values.
- A combined helper, if exported, must return the exact same price/time tuples as the individual helpers and must not introduce separate policy.
- No fallback market, source, symbol, query, chart, or visible-copy behavior belongs here.

## Purity rules

The production module must contain no:

- JSX or React runtime import;
- hook, DOM, or browser access;
- `Date.now`, zero-argument `new Date`, timer, random value, locale formatter, environment lookup, IO, network, cache, or store access;
- Recharts import;
- query hook, API call, or retry callback;
- CSS class, color, component, tooltip, tick formatting, anomaly-marker logic, or descriptor presentation;
- public Replay mode concept.

It may import only the accepted normalized-point type as a production dependency.

## Required tests

Use deterministic focused tests proving at least:

1. empty price input returns `[0, 1]`;
2. normal positive prices reproduce the exact formula;
3. zero-only and one-price inputs receive finite strict padding;
4. negative and mixed-sign prices use min/max and magnitude correctly;
5. input order does not affect the price domain;
6. duplicate prices are preserved semantically and do not break bounds;
7. overflow/non-finite derived price bounds throw the exact `RangeError`;
8. empty time input uses the supplied anchor exactly and never current time;
9. invalid/overflowing empty anchors throw the exact anchor `RangeError`;
10. one timestamp expands by exactly 60 seconds on each side;
11. duplicate equal timestamps use the same single-timestamp expansion;
12. multiple distinct out-of-order timestamps return global min/max;
13. point-derived time overflow throws the exact time-domain `RangeError`;
14. outputs are finite, strictly ascending readonly-compatible tuples;
15. input arrays and points are not mutated;
16. equal inputs and anchor return equal values;
17. any combined helper exactly matches individual helpers;
18. no React/browser/current-time/locale/Recharts/network/query/Replay dependency is introduced.

Use no snapshots, sleeps, random values, current time, browser, backend service, or network call.

## Authorized product paths

Only these new files may be added:

- `web/src/features/dashboard/timelineDomains.ts`
- `web/src/features/dashboard/timelineDomains.test.ts`

No existing product file may change.

## Forbidden product paths

Do not modify:

- `web/src/features/dashboard/timelineNormalization.ts` or its tests;
- `web/src/pages/DashboardPage.tsx`;
- any page, app, router, component, CSS, or current fixture;
- `web/src/features/dashboard/types.ts`;
- API/query/resource/adapter/identity files;
- market-health, anomaly-preview, or dashboard-resource-state worker files;
- status descriptors, semantic fixtures, tooltip primitive, or smoke matrix;
- `web/src/app/GlobalMarketTicker.tsx`;
- `web/package.json`, lockfiles, or build/test/style configuration;
- backend, OpenAPI, CI, Docker, docs, deployment, or scripts.

Do not add a dependency and do not wire the new functions into current JSX.

## Required verification

Run, when available:

1. focused timeline-domain tests;
2. `cd web && npm run test:run`;
3. `cd web && npm run typecheck`;
4. `cd web && npm run lint`;
5. `cd web && npm run build`;
6. `cd web && npm run bundle:check`;
7. `git diff --check`;
8. exact two-path proof;
9. forbidden-path and ticker proof;
10. source-purity proof;
11. dependency proof that P3-MP05 normalized-point files remain byte-identical.

Report unavailable checks honestly. Do not commit after a failed required check.

## Product publication

After successful verification:

1. stage only the two authorized new paths;
2. create exactly one commit with message `feat(ui): extract timeline chart domains`;
3. push normally to `p3/mp06-timeline-domains`;
4. confirm ahead `1`, behind `0` relative to exact assigned base `773b110816d10d31e65a36ce2ed76a1b37beca01`;
5. open one draft PR to `refactor/dashboard-modules` titled `feat(ui): extract timeline chart domains`;
6. include exact base/head, paths, exported API, price/time/overflow semantics, verification, and report path in the PR body;
7. do not merge.

If the phase branch advances after successful preflight, preserve the immutable one-commit candidate and report moving-base divergence. Do not rebase or rewrite.

## Connector delivery report

Create exactly one new report:

`signalguard-rs/phase-3/reports/P3-MP06/<FULL_PRODUCT_HEAD_SHA>.md`

Include exact identity, PR, paths, exported API, every price/time-domain rule, overflow behavior, focused/full gates, unavailable checks, purity proof, P3-MP05 blob-preservation proof, ticker proof, final divergence, and explicit no-merge/no-next-task statement.

Commit only this new report in `progeranna/connector`.

## Definition of done

P3-MP06 is delivered only when the assigned branch contains one verified product commit, a draft PR targets the phase branch, and one immutable connector report records the exact product head. The Orchestrator alone reviews and integrates it.
