# P3-MP08-WEB1 Contract — Pure Recent Anomalies Preview Model

## Execution role

You are an isolated GitHub web implementation worker for SignalGuard RS Phase 3 microphase `P3-MP08`.

Read this immutable contract from `progeranna/connector`, implement the product change in `progeranna/signalguard-rs`, publish one normal product commit to the assigned remote branch, open one draft PR, and publish one immutable delivery report back to the connector repository.

This is a remote GitHub workflow. Do not assume a user-local path, worktree, Docker service, or local Codex session.

## Immutable identity

- Product repository: `progeranna/signalguard-rs`
- Connector repository: `progeranna/connector`
- Assigned branch: `p3/mp08-recent-anomalies-preview`
- Required PR base: `refactor/dashboard-modules`
- Exact assigned base SHA: `3587ec9b70b677121aa796467d5bb359ffb4d174`
- Required commit message: `feat(ui): extract recent anomalies preview model`
- Checkpoint source: `signalguard-rs/phase-3/checkpoints/CHECKPOINT-0/3587ec9b70b677121aa796467d5bb359ffb4d174.md`

The product branch must contain exactly one normal commit above the assigned base.

## Ownership boundary

The worker owns implementation, tests, one commit, normal push, one draft PR, and one connector report.

The worker must not merge, edit the phase branch directly, rewrite history, force-push, modify another worker branch, update control files, wire JSX, or start a component/compositor task.

## Remote preflight

Before editing:

1. Verify `origin/refactor/dashboard-modules` and `origin/p3/mp08-recent-anomalies-preview` both equal `3587ec9b70b677121aa796467d5bb359ffb4d174`.
2. Check out only the assigned branch without history rewriting.
3. Verify clean state and comparison `0 0`.
4. Read exact-base versions of:
   - `web/src/pages/DashboardPage.tsx` read-only, especially `RecentAnomaliesShell` and current preview limit;
   - `web/src/features/dashboard/types.ts` read-only;
   - `web/src/features/dashboard/statusDescriptors.ts` read-only;
   - `web/src/test/marketFixtures.ts` read-only;
   - `web/src/test/statusDescriptorFixtures.ts` read-only.

Stop and report a blocker if identity, base, cleanliness, or accepted anomaly DTO/descriptor semantics differ.

## Goal

Create one pure deterministic Recent Anomalies preview model that owns:

- newest-first ordering;
- stable anomaly identity;
- preview limiting and metadata;
- detector and severity semantic row data.

This task does not render a table/card, format numeric values for presentation, format local time, or modify dashboard composition.

## Required API

Create a module exporting at least:

1. `RECENT_ANOMALIES_PREVIEW_LIMIT` with exact value `7`.
2. A readonly anomaly preview row type.
3. A pure function mapping one `DashboardAnomaly` to one row model.
4. A pure function building the ordered preview result from an anomaly array and optional limit.
5. A readonly result with at least:
   - ordered `allRows`;
   - limited `rows`;
   - `limit`;
   - `totalCount`;
   - `hiddenCount`;
   - `hasMore`;
   - `isEmpty`.

Exact exported names may be chosen consistently and documented.

## Stable identity

- Use the accepted anomaly UUID `id` as the row identity.
- Never use array index, timestamp, symbol, message, or a generated random value as identity.
- Duplicate anomaly IDs are invalid input and must be rejected deterministically with a stable `TypeError` naming the duplicate ID.
- Preserve the original ID exactly.

## Ordering semantics

Sort without mutating the input:

1. effective event time descending;
2. created time descending when effective event times tie;
3. anomaly ID ascending as the final deterministic tie-breaker.

Effective event time:

- use finite `Date.parse(event_time)` when valid;
- otherwise use finite `Date.parse(created_at)`;
- otherwise use negative infinity so invalid-time rows sort after valid-time rows.

Created-time tie-break value:

- finite `Date.parse(created_at)` when valid;
- otherwise negative infinity.

Do not use current time, locale formatting, or input order as the final tie-breaker.

## Row-model semantics

Each row must contain at least:

- `id`;
- `symbol`;
- original `anomalyType` identifier;
- deterministic detector label from accepted `formatDetectorLabel`;
- original severity key;
- accepted severity descriptor;
- combined active label from accepted `formatActiveAnomalyLabel`;
- message;
- observed value;
- threshold value;
- original `eventTime`;
- original `createdAt`;
- parsed effective timestamp milliseconds or `null` when neither timestamp parses.

Rules:

- Preserve numeric zero and negative values exactly; numeric formatting belongs to presentation.
- Preserve empty message exactly; do not synthesize context copy.
- Preserve Demo/Live neutrality: this model receives anomalies only and must not invent a mode/source.
- Unknown detector identifiers use accepted deterministic descriptor formatting.
- Do not add CSS classes, colors, icons, date strings, or React nodes.

## Preview-limit semantics

- Default limit is `7`.
- Validate caller limit as finite non-negative integer.
- Stable `TypeError` for non-finite/non-integer and `RangeError` for negative.
- Limit `0` returns no preview rows while preserving ordered `allRows` and metadata.
- `hiddenCount = max(totalCount - rows.length, 0)`.
- `hasMore` exactly when hidden count is positive.
- `isEmpty` exactly when total count is zero.

## Purity rules

No JSX, React runtime, hook, DOM/browser access, current time, randomness, locale formatter, network/cache/store access, query hook, CSS class, component, icon, color, IO, or Replay public mode.

The model may import accepted anomaly types and pure descriptor functions.

## Required tests

Prove at least:

1. exact default limit `7`;
2. stable row identity equals anomaly UUID;
3. duplicate IDs reject deterministically;
4. newest event time sorts first;
5. created time breaks equal event-time ties;
6. ID ascending breaks full time ties;
7. invalid event time falls back to created time;
8. both-invalid timestamps sort after valid timestamps and expose `null` effective timestamp;
9. input array and objects are not mutated;
10. known and unknown detector labels use accepted formatting;
11. severity descriptor and combined active label match accepted P3-MP03 semantics;
12. observed/threshold zero and negative values are preserved;
13. empty message is preserved;
14. fewer/equal/more-than-limit metadata;
15. limit `0`;
16. invalid-limit rejection;
17. empty input;
18. equal inputs return equal values;
19. no time/locale/React/network/Replay dependency.

Use deterministic literal fixtures. No snapshots, sleeps, current time, backend, or network.

## Authorized paths

Only these new files may be added:

- `web/src/features/dashboard/recentAnomaliesPreviewModel.ts`
- `web/src/features/dashboard/recentAnomaliesPreviewModel.test.ts`

No existing product file may change.

## Forbidden scope

Do not modify:

- `web/src/pages/DashboardPage.tsx`;
- any page/app/router/component/CSS path;
- DTO, API, query, resource, adapter, identity, selected-symbol, or catalog files;
- market-health, timeline, or resource-state worker paths;
- descriptor model or fixtures;
- tooltip, smoke matrix, existing fixtures;
- `web/src/app/GlobalMarketTicker.tsx`;
- package/lock/config files;
- backend, OpenAPI, CI, Docker, docs, deployment, or scripts.

Do not add a dependency or wire the model into current JSX.

## Verification

Run focused tests, full frontend tests, typecheck, lint, build, bundle check, `git diff --check`, exact two-path proof, forbidden-path/ticker proof, and source-purity proof when available.

Report unavailable checks honestly. Do not commit after a failed required gate.

## Publication

After all gates pass:

- commit exactly once with `feat(ui): extract recent anomalies preview model`;
- push normally to `p3/mp08-recent-anomalies-preview`;
- confirm ahead `1`, behind `0` against assigned base;
- open one draft PR to `refactor/dashboard-modules`;
- create one connector report at `signalguard-rs/phase-3/reports/P3-MP08/<FULL_PRODUCT_HEAD_SHA>.md`;
- do not merge or start another task.

If the phase branch advances after preflight, preserve the one-commit candidate and report moving-base divergence without rewriting.

## Delivery report

Record exact identity, PR, paths, exported API, stable identity, ordering/fallback/tie-break semantics, row model, limit behavior, tests/gates, unavailable checks, purity/ticker proof, divergence, and explicit no-merge/no-next-task statement.

Commit only the new report in `progeranna/connector`.

## Definition of done

P3-MP08 is delivered only when one verified product commit, one draft PR, and one immutable connector report exist for the exact head. The Orchestrator alone reviews and integrates it.