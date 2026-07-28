# P3-MP07-WEB1 Contract — Pure Market Health Preview Model

## Execution role

You are an isolated GitHub web implementation worker for SignalGuard RS Phase 3 microphase `P3-MP07`.

Read this immutable contract from `progeranna/connector`, implement the product change in `progeranna/signalguard-rs`, publish one normal product commit to the assigned remote branch, open one draft PR, and publish one immutable delivery report back to the connector repository.

This is a remote GitHub workflow. Do not assume a user-local path, worktree, Docker service, or local Codex session.

## Immutable identity

- Product repository: `progeranna/signalguard-rs`
- Connector repository: `progeranna/connector`
- Assigned branch: `p3/mp07-market-health-preview`
- Required PR base: `refactor/dashboard-modules`
- Exact assigned base SHA: `3587ec9b70b677121aa796467d5bb359ffb4d174`
- Required product commit message: `feat(ui): extract market health preview model`
- Checkpoint source: `signalguard-rs/phase-3/checkpoints/CHECKPOINT-0/3587ec9b70b677121aa796467d5bb359ffb4d174.md`

The product branch must contain exactly one normal commit above the assigned base.

## Ownership boundary

The worker owns implementation, focused tests, one product commit, normal push, one draft PR, and one connector report.

The worker must not merge, edit the phase branch directly, rewrite history, force-push, modify another worker branch, update Phase 3 control files, wire the model into JSX, or start a component/compositor task.

## Remote preflight

Before editing:

1. Verify `origin/refactor/dashboard-modules` and `origin/p3/mp07-market-health-preview` both equal `3587ec9b70b677121aa796467d5bb359ffb4d174`.
2. Check out only the assigned branch without history rewriting.
3. Verify clean state and comparison `0 0`.
4. Read exact-base versions of:
   - `web/src/pages/DashboardPage.tsx` read-only, especially `DASHBOARD_TABLE_PREVIEW_LIMIT`, `SymbolHealthShell`, table rows, and mobile cards;
   - `web/src/features/dashboard/types.ts` read-only;
   - `web/src/features/dashboard/marketOrder.ts` read-only;
   - `web/src/test/marketFixtures.ts` read-only;
   - P3-MP03 descriptors and P3-MP04 semantic fixtures read-only.

Stop and report a blocker if identity, base, cleanliness, or accepted DTO/order semantics differ.

## Goal

Create one pure, deterministic Market Health preview model that owns:

- canonical market ordering;
- preview limit calculation;
- stable row identity;
- observed versus non-observed metric exposure;
- preview metadata such as hidden count and `hasMore`.

This task does not render a table/card and does not modify current dashboard presentation.

## Required production API

Create a module exporting at least:

1. `MARKET_HEALTH_PREVIEW_LIMIT` with exact value `7`.
2. A readonly row-view-model type.
3. A pure function that maps one `DashboardSymbolSummary` to one row model.
4. A pure function that builds the ordered preview result from an array and optional limit.
5. A readonly preview result containing at least:
   - ordered `allRows`;
   - limited `rows`;
   - `limit`;
   - `totalCount`;
   - `hiddenCount`;
   - `hasMore`;
   - `isEmpty`.

Exact exported names may be chosen consistently and documented.

## Binding ordering semantics

- Reuse accepted `orderMarketEntries`; do not duplicate or replace market-order ownership.
- Known canonical markets follow the accepted canonical order.
- Extra markets preserve their relative input order after canonical markets.
- Do not mutate the input array.
- Do not inject missing Demo markets or synthesize a catalog; the input is already the API-owned summary catalog.
- Do not deduplicate, rename, or normalize source/availability locally.
- Preserve Demo/Live source exactly from each input row.

## Binding row-model semantics

Each row model must contain at least:

- stable identity key derived from explicit `source` and `symbol`, never from array index;
- `symbol`;
- `source`;
- `availability`;
- `observed` boolean;
- health score or `null`;
- health status or `null`;
- last trade price string or `null`;
- spread percentage or `null`;
- trades per minute or `null`;
- last-event age milliseconds or `null`.

Rules:

- `observed` is true only for `availability === "observed"`.
- For `configured`, `awaiting`, or `unavailable`, every health and market metric in the row model must be `null`, even if an invalid input object contains state or health data.
- For `observed`, preserve available health/state values exactly and use `null` only when the accepted DTO field is absent/null.
- Do not fabricate zero, dash strings, labels, tones, CSS classes, or fallback Demo values.
- Keep availability, freshness, and health distinct.
- Preserve numeric zero.

## Preview-limit semantics

- Default limit is `7`.
- A caller-supplied limit must be a finite non-negative integer.
- Reject invalid limits deterministically with a stable `TypeError` for non-finite/non-integer input and `RangeError` for negative input.
- Limit `0` yields zero preview rows while preserving `allRows` and metadata.
- `hiddenCount = max(totalCount - rows.length, 0)`.
- `hasMore` is true exactly when `hiddenCount > 0`.
- `isEmpty` is true exactly when total count is zero.

## Purity rules

The module must contain no JSX, React runtime, hook, DOM/browser access, current time, random value, locale formatter, network/cache/store access, query hook, CSS class, component, icon, color, or Replay public mode.

It may import `DashboardSymbolSummary` as a type and call accepted `orderMarketEntries`.

## Required tests

Prove at least:

1. exact default limit `7`;
2. canonical ordering for known markets;
3. extra-market relative order preservation;
4. input array and entries are not mutated;
5. stable identity uses source and symbol and never index;
6. observed rows preserve score/status/price/spread/trades/age including numeric zero;
7. all metrics are forced to `null` for configured, awaiting, and unavailable rows;
8. no Demo/source fallback is introduced;
9. fewer than, equal to, and greater than limit metadata;
10. limit `0` behavior;
11. deterministic rejection of negative, fractional, `NaN`, and infinite limits;
12. empty input result;
13. equal inputs return equal values;
14. no presentation, React, time, locale, network, or Replay dependency.

Use deterministic literal fixtures. No snapshots, sleeps, current time, backend, or network.

## Authorized paths

Only these new files may be added:

- `web/src/features/dashboard/marketHealthPreviewModel.ts`
- `web/src/features/dashboard/marketHealthPreviewModel.test.ts`

No existing product file may change.

## Forbidden scope

Do not modify:

- `web/src/pages/DashboardPage.tsx`;
- any page/app/router/component/CSS path;
- `web/src/features/dashboard/marketOrder.ts`;
- DTO, API, query, resource, adapter, identity, selected-symbol, or catalog files;
- timeline, anomaly-preview, or resource-state worker files;
- status descriptors, fixtures, tooltip, or smoke matrix;
- `web/src/app/GlobalMarketTicker.tsx`;
- package/lock/config files;
- backend, OpenAPI, CI, Docker, docs, deployment, or scripts.

Do not add a dependency or wire this model into current JSX.

## Verification

Run, when available:

1. focused preview-model tests;
2. full frontend tests;
3. typecheck;
4. lint;
5. build;
6. bundle check;
7. `git diff --check`;
8. exact two-path proof;
9. forbidden-path and ticker proof;
10. source-purity proof.

Report unavailable checks honestly. Do not commit after a failed required check.

## Publication

After all gates pass:

- commit exactly once with `feat(ui): extract market health preview model`;
- push normally to `p3/mp07-market-health-preview`;
- confirm ahead `1`, behind `0` against the assigned base;
- open one draft PR to `refactor/dashboard-modules`;
- publish one connector report at `signalguard-rs/phase-3/reports/P3-MP07/<FULL_PRODUCT_HEAD_SHA>.md`;
- do not merge or start another task.

If the phase branch advances after preflight, preserve the one-commit candidate and report moving-base divergence without rewriting.

## Delivery report

Record exact identity, PR, paths, exported API, ordering, row semantics, metric suppression, limit behavior, gates, unavailable checks, purity/ticker proof, divergence, and explicit no-merge/no-next-task statement.

Commit only the new report in `progeranna/connector`.

## Definition of done

P3-MP07 is delivered only when one verified product commit, one draft PR, and one immutable connector report exist for the exact head. The Orchestrator alone reviews and integrates it.