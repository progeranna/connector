# P3-MP01-WEB1 Contract — Reusable UI Smoke Matrix

## Execution role

You are an isolated GitHub web implementation worker for SignalGuard RS Phase 3 microphase `P3-MP01`.

Read this contract from the connector repository, implement the product change in `progeranna/signalguard-rs`, publish one product commit to the assigned remote branch, open one draft pull request, and publish one delivery report back to the connector repository.

This task is executed entirely through remote GitHub repositories. Do not assume or reference any user-local path, local worktree, local Docker service, or local Codex session.

## Immutable repository identity

Product repository: `progeranna/signalguard-rs`

Connector repository: `progeranna/connector`

Assigned product branch: `p3/mp01-ui-smoke-matrix`

Required PR base: `refactor/dashboard-modules`

Exact assigned base SHA: `6b57938d87e05d3b4fa4858f9c34c27739877821`

Required product commit message: `test(ui): define reusable smoke matrix`

Inventory source:

`signalguard-rs/phase-3/inventory/P3-MP00/6b57938d87e05d3b4fa4858f9c34c27739877821.md`

The product branch must contain exactly one normal product commit above the assigned base.

## Ownership boundary

The worker owns:

- implementation;
- focused and full verification available in the web-worker environment;
- exactly one product commit;
- normal push to the assigned branch;
- one draft product PR;
- one connector delivery report.

The worker must not:

- merge any PR;
- edit `refactor/dashboard-modules` directly;
- amend, rebase, reset, squash, or force-push;
- modify a different worker branch;
- modify Phase 3 control/status files;
- modify existing connector prompts;
- start another microphase;
- claim an unavailable check passed.

## Remote preflight

Before editing:

1. Fetch the product repository refs.
2. Verify `origin/refactor/dashboard-modules` equals `6b57938d87e05d3b4fa4858f9c34c27739877821`.
3. Verify `origin/p3/mp01-ui-smoke-matrix` equals the same SHA.
4. Check out `p3/mp01-ui-smoke-matrix` without rewriting history.
5. Verify the checkout is clean and the comparison against the phase branch is `0 0`.
6. Read the exact-base versions of:
   - `web/src/app/router.tsx`;
   - `web/src/app/marketNavigationIsolation.test.tsx`;
   - `web/src/features/dashboard/marketDataIsolation.test.tsx`;
   - `web/src/pages/DashboardPage.popup.test.tsx`;
   - `web/src/pages/SymbolDetailPage.test.tsx`;
   - `web/src/features/dashboard/symbolPopupResource.test.tsx`;
   - `web/src/test/marketFixtures.ts`;
   - `web/src/test/setup.ts`;
   - `web/vitest.config.ts`;
   - `web/package.json` read-only.

Stop without editing and report a blocker if the refs, base, cleanliness, or branch identity differ.

## Goal

Create a typed, deterministic, reusable smoke-matrix manifest and executable completeness tests for the existing public UI. This is test infrastructure only. It must not change production presentation, runtime behavior, API behavior, routes, or CSS.

The manifest must explicitly cover:

- public modes: exactly `demo`, `live`;
- canonical markets: exactly `BTCUSDT`, `ETHUSDT`;
- surfaces: dashboard, symbol detail route, symbol detail popup;
- responsive targets: desktop and mobile with deterministic named widths;
- states: loading, error, empty, unavailable/non-observed, observed success;
- steady-state render;
- Demo → Live and Live → Demo;
- BTC → ETH and ETH → BTC;
- route → route and popup → popup;
- route/popup parity;
- late response after mode switch;
- late response after symbol switch;
- invalid or missing Live symbol without Demo fallback.

Represent, but do not falsely mark as already implemented, later Wave 5 dialog requirements:

- Escape close;
- backdrop close;
- focus containment;
- initial focus;
- focus return;
- body scroll lock.

## Design requirements

1. Add a pure TypeScript manifest with exported literal unions/types and readonly scenario collections.
2. Give every scenario a stable unique identifier.
3. Keep ordering deterministic.
4. Do not depend on React, DOM globals, timers, network requests, localStorage, or TanStack Query.
5. Do not execute tests or side effects on import.
6. Prefer named scenario groups over one opaque Cartesian-product array.
7. No production code may import the manifest.
8. Do not create screenshots or generated snapshots.
9. Do not introduce Replay as a public mode.

## Required tests

Prove at least:

- exact mode, market, surface, viewport, and state vocabularies;
- every required mode × symbol × surface identity has an observed-success scenario;
- every surface has desktop and mobile coverage;
- every required switch/race/parity scenario exists;
- invalid/missing Live identity explicitly forbids Demo fallback;
- dialog requirements are represented without claiming all focus behavior currently passes;
- scenario IDs are unique and collections deterministic;
- no scenario contains a Replay public mode;
- importing the manifest has no side effect and requires no DOM setup.

Tests must use no sleeps or snapshots.

## Authorized product paths

- new `web/src/test/uiSmokeMatrix.ts`;
- new `web/src/test/uiSmokeMatrix.test.ts`.

Optional only when strictly necessary:

- `web/src/test/marketFixtures.ts`.

A correct implementation should normally change only the two new files.

## Forbidden product paths

Do not modify:

- production `.ts` or `.tsx` files outside `web/src/test`;
- `web/src/pages/DashboardPage.tsx`;
- `web/src/pages/SymbolDetailPage.tsx`;
- `web/src/app/AppShell.tsx`;
- `web/src/app/GlobalMarketTicker.tsx`;
- `web/src/app/router.tsx`;
- `web/src/shared/styles/globals.css`;
- existing API/query/resource/adapter/identity files;
- `web/package.json` or lockfiles;
- build/test/style configuration;
- backend, OpenAPI, CI, Docker, deployment, docs, or scripts;
- ticker text, structure, order, scrolling, animation, or CSS.

Do not add a dependency.

## Required verification

Run, when available in the web-worker environment:

1. focused smoke-matrix test;
2. `cd web && npm run test:run`;
3. `cd web && npm run typecheck`;
4. `cd web && npm run lint`;
5. `cd web && npm run build`;
6. `cd web && npm run bundle:check`;
7. `git diff --check`;
8. exact changed-path proof against the assigned base;
9. forbidden-path and ticker proof.

Report unavailable checks honestly with the exact reason. Do not commit after a failed required check.

## Product publication

After successful verification:

1. stage only authorized product paths;
2. create exactly one commit with the required message;
3. push normally to `p3/mp01-ui-smoke-matrix`;
4. confirm ahead `1`, behind `0` relative to `origin/refactor/dashboard-modules`;
5. open one draft PR to `refactor/dashboard-modules` titled `test(ui): define reusable smoke matrix`;
6. include exact base SHA, exact head SHA, changed paths, verification, and the connector report path in the PR body;
7. do not merge the PR.

## Connector delivery report

After the product head and draft PR exist, create exactly one new report:

`signalguard-rs/phase-3/reports/P3-MP01/<FULL_PRODUCT_HEAD_SHA>.md`

The report must include:

- task and branch;
- exact base and product head;
- product commit message;
- draft PR number and URL;
- exact changed paths;
- matrix dimensions and scenario groups;
- deterministic/unique-ID evidence;
- proof Replay is absent as a public mode;
- focused/full test results;
- typecheck/lint/build/bundle results;
- unavailable checks with reasons;
- forbidden-path/ticker proof;
- final ahead/behind count;
- worktree/repository cleanliness evidence available to the worker;
- explicit statement that no merge and no next task occurred.

Commit only this new report in the connector repository with a concise documentation commit. Do not modify connector control files, status files, prompts, inventories, reviews, or integration records.

## Definition of done

`P3-MP01-WEB1` is delivered only when the exact remote branch contains one verified product commit, a draft PR targets the exact phase branch, and a connector report records the immutable product head and evidence. The Orchestrator alone reviews and integrates it.