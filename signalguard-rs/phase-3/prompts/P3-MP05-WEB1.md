# P3-MP05-WEB1 Contract — Pure Timeline Point Normalization

## Execution role

You are an isolated GitHub web implementation worker for SignalGuard RS Phase 3 microphase `P3-MP05`.

Read this immutable contract from `progeranna/connector`, implement the product change in `progeranna/signalguard-rs`, publish one normal product commit to the assigned remote branch, open one draft product PR, and publish one immutable delivery report back to the connector repository.

This is a remote GitHub workflow. Do not assume a user-local path, worktree, Docker service, or local Codex session.

## Immutable repository identity

- Product repository: `progeranna/signalguard-rs`
- Connector repository: `progeranna/connector`
- Assigned product branch: `p3/mp05-timeline-normalization`
- Required PR base: `refactor/dashboard-modules`
- Exact assigned base SHA: `3587ec9b70b677121aa796467d5bb359ffb4d174`
- Required product commit message: `feat(ui): extract timeline normalization`
- Checkpoint source: `signalguard-rs/phase-3/checkpoints/CHECKPOINT-0/3587ec9b70b677121aa796467d5bb359ffb4d174.md`

The product branch must contain exactly one normal product commit above the assigned base.

## Ownership boundary

The worker owns implementation, focused tests, one product commit, normal push, one draft PR, and one connector delivery report.

The worker must not merge, edit the phase branch directly, rewrite history, force-push, modify another worker branch, update Phase 3 control files, modify an existing prompt, wire the model into a page/component, calculate chart domains, or start P3-MP06.

## Remote preflight

Before editing:

1. Fetch product refs.
2. Verify `origin/refactor/dashboard-modules` equals `3587ec9b70b677121aa796467d5bb359ffb4d174`.
3. Verify `origin/p3/mp05-timeline-normalization` equals the same SHA.
4. Check out only the assigned branch without history rewriting.
5. Verify clean state and comparison `0 0` against the phase branch.
6. Read exact-base versions of:
   - `web/src/pages/DashboardPage.tsx` read-only, especially `MarketTimelineChartPoint` and `buildTimelineChartPoints`;
   - `web/src/features/dashboard/types.ts` read-only;
   - `web/src/test/marketFixtures.ts` read-only;
   - P3-MP03 descriptors and P3-MP04 fixtures read-only;
   - Phase 3 Wave 1 requirements.

Stop and report a blocker if identity, base, cleanliness, or the accepted timeline DTO differs.

## Goal

Create one pure typed normalization model for converting validated `MarketTimelinePoint` DTOs into deterministic chart-point data.

This microphase extracts only timestamp, price, optional numeric-field, and invalid-point normalization. It must not calculate X/Y domains, visible anomaly markers, tooltip content, chart presentation, or query state.

No production caller is migrated in this task, so visible UI behavior remains unchanged.

## Required production API

Create a small module exporting:

1. A readonly normalized point type containing at least:
   - original `timestamp`;
   - parsed finite `timestampMs`;
   - finite numeric `price`;
   - original exact `priceLabel` string;
   - normalized `spreadPct: number | null`;
   - normalized `tradesPerMinute: number | null`;
   - normalized `lastEventAgeMs: number | null`.
2. A function that normalizes one `MarketTimelinePoint` and returns a normalized point or `null` when the point is unusable.
3. A function that normalizes an array and returns only valid normalized points in original input order.

Exact exported names may be chosen consistently and documented in the report.

## Binding normalization semantics

### Timestamp

- Parse `point.timestamp` deterministically with `Date.parse`.
- Reject the point when the result is non-finite.
- Preserve the original timestamp string in accepted output.
- Do not call current time or substitute a timestamp.

### Price

- The price input is a string.
- Reject empty or whitespace-only price strings.
- Convert the original string with `Number` only after the non-empty check.
- Reject non-finite numeric results, including `NaN`, positive infinity, and negative infinity spellings.
- Preserve the original exact string as `priceLabel`; do not locale-format, round, or rewrite it.
- Accept finite zero and finite negative values at normalization level; chart-domain policy belongs to P3-MP06.

### Optional numeric fields

Normalize each optional numeric value independently:

- `spread_pct`: preserve finite numbers including zero and negatives; otherwise `null`;
- `trades_per_minute`: preserve finite non-negative numbers; otherwise `null`;
- `last_event_age_ms`: preserve finite non-negative numbers; otherwise `null`.

Do not reject an otherwise valid point because one optional field is unusable.

### Collection behavior

- Preserve input order exactly.
- Do not sort, deduplicate, merge, interpolate, or mutate input points.
- Preserve duplicate timestamps and duplicate prices.
- Return a new readonly-compatible array.
- Equal inputs must produce equal values.

## Purity rules

The module must contain no:

- JSX or React runtime import;
- hook or DOM/browser access;
- `Date.now`, `new Date()` without supplied input, timer, random value, locale formatter, environment lookup, IO, network, cache, or store access;
- Recharts import;
- query hook or API call;
- CSS class, color, component, tooltip, or descriptor presentation;
- public Replay mode concept.

It may import `MarketTimelinePoint` as a type only.

## Required tests

Use deterministic focused tests proving at least:

1. a fully valid point maps to every required output field;
2. exact timestamp and price strings are preserved;
3. finite zero price is accepted;
4. finite negative price is accepted at this layer;
5. empty and whitespace-only prices are rejected;
6. nonnumeric, `NaN`, and infinite prices are rejected;
7. invalid timestamps are rejected;
8. finite optional values including zero are preserved;
9. non-finite optional values become `null` without dropping the point;
10. negative trades/min and age become `null`;
11. negative spread remains preserved;
12. array normalization filters invalid points while preserving valid input order;
13. duplicate timestamps are retained;
14. input objects and input array are not mutated;
15. equal inputs return equal values;
16. no current-time, locale, React, browser, Recharts, network, or Replay dependency is introduced.

Use no snapshots, sleeps, random values, current time, or network/backend service.

## Authorized product paths

Only these new files may be added:

- `web/src/features/dashboard/timelineNormalization.ts`
- `web/src/features/dashboard/timelineNormalization.test.ts`

No existing product file may change.

## Forbidden product paths

Do not modify:

- `web/src/pages/DashboardPage.tsx`;
- any page, app, router, component, CSS, or current test fixture;
- `web/src/features/dashboard/types.ts`;
- API/query/resource/adapter/identity files;
- `timelineNormalization` paths owned by another head after publication;
- P3-MP06 domain paths;
- status descriptors or semantic fixtures;
- tooltip primitive or smoke matrix;
- `web/src/app/GlobalMarketTicker.tsx`;
- `web/package.json`, lockfiles, or build/test/style configuration;
- backend, OpenAPI, CI, Docker, docs, deployment, or scripts.

Do not add a dependency. Do not wire the new functions into current JSX.

## Required verification

Run, when available:

1. focused timeline-normalization tests;
2. `cd web && npm run test:run`;
3. `cd web && npm run typecheck`;
4. `cd web && npm run lint`;
5. `cd web && npm run build`;
6. `cd web && npm run bundle:check`;
7. `git diff --check`;
8. exact two-path proof;
9. forbidden-path and ticker proof;
10. source-purity proof.

Report unavailable checks honestly. Do not commit after a failed required check.

## Product publication

After successful verification:

1. stage only the two authorized new paths;
2. create exactly one commit with message `feat(ui): extract timeline normalization`;
3. push normally to `p3/mp05-timeline-normalization`;
4. confirm ahead `1`, behind `0` relative to the exact assigned base;
5. open one draft PR to `refactor/dashboard-modules` titled `feat(ui): extract timeline normalization`;
6. include exact base/head, paths, semantics, verification, and report path in the PR body;
7. do not merge.

If the phase branch advances after successful preflight, preserve the immutable one-commit candidate and report moving-base divergence. Do not rebase or rewrite.

## Connector delivery report

Create exactly one new report:

`signalguard-rs/phase-3/reports/P3-MP05/<FULL_PRODUCT_HEAD_SHA>.md`

Include exact identity, PR, paths, exported API, every normalization rule, focused/full gates, unavailable checks, purity proof, ticker proof, final divergence, and explicit no-merge/no-P3-MP06 statement.

Commit only this new report in `progeranna/connector`.

## Definition of done

P3-MP05 is delivered only when the assigned branch contains one verified product commit, a draft PR targets the phase branch, and one immutable connector report records the exact product head. The Orchestrator alone reviews and integrates it.