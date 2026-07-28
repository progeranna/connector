# P3-MP09-WEB1 Contract — Pure Dashboard Resource-State Mapping

## Execution role

You are an isolated GitHub web implementation worker for SignalGuard RS Phase 3 microphase `P3-MP09`.

Read this immutable contract from `progeranna/connector`, implement the product change in `progeranna/signalguard-rs`, publish one normal product commit to the assigned remote branch, open one draft PR, and publish one immutable delivery report back to the connector repository.

This is a remote GitHub workflow. Do not assume a user-local path, worktree, Docker service, or local Codex session.

## Immutable identity

- Product repository: `progeranna/signalguard-rs`
- Connector repository: `progeranna/connector`
- Assigned branch: `p3/mp09-dashboard-resource-state`
- Required PR base: `refactor/dashboard-modules`
- Exact assigned base SHA: `3587ec9b70b677121aa796467d5bb359ffb4d174`
- Required product commit message: `feat(ui): extract dashboard resource states`
- Checkpoint source: `signalguard-rs/phase-3/checkpoints/CHECKPOINT-0/3587ec9b70b677121aa796467d5bb359ffb4d174.md`

The product branch must contain exactly one normal product commit above the assigned base.

## Ownership boundary

The worker owns implementation, focused tests, one product commit, normal push, one draft PR, and one connector delivery report.

The worker must not merge, edit the phase branch directly, rewrite history, force-push, modify another worker branch, update Phase 3 control files, wire the state model into React/query code, or start a component/compositor task.

## Remote preflight

Before editing:

1. Fetch product refs.
2. Verify `origin/refactor/dashboard-modules` equals `3587ec9b70b677121aa796467d5bb359ffb4d174`.
3. Verify `origin/p3/mp09-dashboard-resource-state` equals the same SHA.
4. Check out only the assigned branch without history rewriting.
5. Verify clean state and comparison `0 0` against the phase branch.
6. Read exact-base versions of:
   - `web/src/pages/DashboardPage.tsx` read-only, especially current loading/error/data precedence;
   - `web/src/features/dashboard/types.ts` read-only;
   - `web/src/features/dashboard/api.ts` read-only for query-result shape context only;
   - `web/src/features/dashboard/symbolMarketResource.ts` read-only for accepted resource-state vocabulary and stale-data precedence patterns;
   - `web/src/test/marketFixtures.ts` read-only;
   - Phase 3 Checkpoint 0 and Wave 1 requirements.

Stop and report a blocker if identity, base, cleanliness, or the accepted dashboard summary type differs.

## Goal

Create one pure deterministic mapping from dashboard query facts into an explicit resource-state model for later dashboard compositor use.

The model must distinguish:

- initial loading with no data;
- blocking error with no data;
- empty data;
- successful data;
- successful or empty cached data while a background refresh is running;
- successful or empty cached data while a background refresh has failed.

This task must not call React hooks, TanStack Query, APIs, retry functions, or rendering code. No current page is migrated in this microphase.

## Required input model

Define one readonly input type containing at least:

- `data: DashboardSummary | null | undefined`;
- `isLoading: boolean`;
- `isFetching: boolean`;
- `isError: boolean`;
- `error: unknown`.

The mapper must not mutate the supplied summary or error.

## Required output model

Export one discriminated union and one pure resolver function.

Use exact top-level status values:

- `loading`;
- `error`;
- `empty`;
- `success`.

### Loading state

Contains at least:

- `status: "loading"`;
- no summary payload;
- no refresh error;
- `isRefreshing: false`.

### Error state

Contains at least:

- `status: "error"`;
- original blocking `error` value by reference;
- no summary payload;
- `isRefreshing: false`.

Do not format or replace the error.

### Empty state

Contains at least:

- `status: "empty"`;
- exact summary payload by reference when data exists, otherwise `null`;
- `reason` with exact values `no-data` or `no-markets-and-anomalies`;
- `isRefreshing`;
- `refreshError: unknown | null`.

### Success state

Contains at least:

- `status: "success"`;
- exact summary payload by reference;
- `isRefreshing`;
- `refreshError: unknown | null`.

Exact exported type/function names may be chosen consistently and documented.

## Binding precedence

Resolve in this exact semantic order.

### 1. Usable data wins over background query flags

When `data` exists:

- never return blocking `loading` or blocking `error`;
- classify the data as `empty` or `success`;
- `isRefreshing` is true exactly when `isFetching` is true;
- `refreshError` is the original error exactly when `isError` is true, otherwise `null`;
- preserve `data` by reference;
- do not erase cached data because a background fetch failed.

`isLoading` may also be true in a supplied edge-case input, but existing data still wins.

### 2. No data plus loading

When no data exists and either `isLoading` or `isFetching` is true:

- return `loading`;
- loading takes precedence over an accompanying error flag while the request is actively loading/fetching and no data exists.

### 3. No data plus error

When no data exists, no loading/fetching is active, and `isError` is true:

- return blocking `error` with the original error value.

### 4. No data and idle

When no data exists and no loading/fetching/error condition applies:

- return `empty`;
- `summary` is `null`;
- `reason` is `no-data`;
- `isRefreshing` is false;
- `refreshError` is null.

## Empty-summary semantics

A supplied `DashboardSummary` is empty exactly when:

- `summary.symbols.length === 0`; and
- `summary.recent_anomalies.length === 0`.

Then return `empty` with reason `no-markets-and-anomalies`.

A summary is `success` when either collection is non-empty. Do not use pipeline/service status to redefine emptiness.

Do not inject canonical Demo markets, fallback symbols, anomalies, source, metrics, or presentation copy.

## Identity and source preservation

For any state containing data:

- preserve the exact `DashboardSummary` object by reference;
- therefore preserve its explicit `source`, symbols, availability states, and anomalies unchanged;
- do not clone, reorder, normalize, filter, or adapt the payload;
- do not synthesize Demo into Live or vice versa.

## Purity rules

The production module must contain no:

- JSX or React runtime import;
- React hook;
- TanStack Query import;
- API/query call or retry callback;
- DOM/browser access;
- current time, timer, randomness, locale formatting, environment lookup, IO, network, cache, or store access;
- CSS class, color, icon, component, visible copy, or error formatting;
- public Replay mode concept.

It may import `DashboardSummary` as a type only.

## Required tests

Use deterministic focused tests proving at least:

1. no data + initial loading → `loading`;
2. no data + fetching → `loading`;
3. no data + fetching + error flag → `loading` precedence;
4. no data + idle error → blocking `error` preserving error reference;
5. no data + idle/no error → `empty/no-data`;
6. data with no symbols and no anomalies → `empty/no-markets-and-anomalies`;
7. data with symbols only → `success`;
8. data with anomalies only → `success`;
9. data with both → `success`;
10. cached success data + fetching → success with `isRefreshing=true`;
11. cached empty data + fetching → empty with `isRefreshing=true`;
12. cached success data + background error → success preserving summary and refresh-error references;
13. cached empty data + background error → empty preserving summary and refresh-error references;
14. data wins even when `isLoading=true`;
15. source, symbols, availability, and anomalies are preserved without cloning or mutation;
16. input object, summary, arrays, and error are not mutated;
17. equal inputs produce equal values except for intentionally preserved object references;
18. no React/query/time/locale/network/Replay dependency.

Use no snapshots, sleeps, random values, current time, backend service, or network call.

## Authorized product paths

Only these new files may be added:

- `web/src/features/dashboard/dashboardResourceState.ts`
- `web/src/features/dashboard/dashboardResourceState.test.ts`

No existing product file may change.

## Forbidden product paths

Do not modify:

- `web/src/pages/DashboardPage.tsx`;
- any page, app, router, component, CSS, or current fixture path;
- `web/src/features/dashboard/api.ts`;
- DTO, query-key, resource, adapter, identity, selected-symbol, catalog, or order files;
- timeline, market-health, or anomaly-preview worker files;
- status descriptors, semantic fixtures, tooltip, or smoke matrix;
- `web/src/app/GlobalMarketTicker.tsx`;
- `web/package.json`, lockfiles, or build/test/style configuration;
- backend, OpenAPI, CI, Docker, docs, deployment, or scripts.

Do not add a dependency or wire the model into current JSX/query hooks.

## Required verification

Run, when available:

1. focused dashboard-resource-state tests;
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

After all gates pass:

1. stage only the two authorized new paths;
2. create exactly one commit with message `feat(ui): extract dashboard resource states`;
3. push normally to `p3/mp09-dashboard-resource-state`;
4. confirm ahead `1`, behind `0` relative to the exact assigned base;
5. open one draft PR to `refactor/dashboard-modules` titled `feat(ui): extract dashboard resource states`;
6. include exact base/head, paths, state precedence, verification, and report path in the PR body;
7. do not merge.

If the phase branch advances after successful preflight, preserve the one-commit candidate and report moving-base divergence without rewriting.

## Connector delivery report

Create exactly one new report:

`signalguard-rs/phase-3/reports/P3-MP09/<FULL_PRODUCT_HEAD_SHA>.md`

Record exact identity, PR, paths, exported union/function, precedence, cached-data behavior, empty semantics, reference/source preservation, tests/gates, unavailable checks, purity/ticker proof, final divergence, and explicit no-merge/no-next-task statement.

Commit only the new report in `progeranna/connector`.

## Definition of done

P3-MP09 is delivered only when one verified product commit, one draft PR, and one immutable connector report exist for the exact head. The Orchestrator alone reviews and integrates it.