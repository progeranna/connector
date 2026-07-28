# P3-MP02-WEB1 Contract — Accessible Tooltip Primitive

## Execution role

You are an isolated GitHub web implementation worker for SignalGuard RS Phase 3 microphase `P3-MP02`.

Read this contract from `progeranna/connector`, implement the product change in `progeranna/signalguard-rs`, publish one product commit to the assigned remote branch, open one draft PR, and publish one delivery report back to the connector repository.

This is a remote GitHub workflow. Do not assume or reference a user-local path, local worktree, local Docker service, or local Codex session.

## Immutable repository identity

Product repository: `progeranna/signalguard-rs`

Connector repository: `progeranna/connector`

Assigned product branch: `p3/mp02-tooltip-primitive`

Required PR base: `refactor/dashboard-modules`

Exact assigned base SHA: `6b57938d87e05d3b4fa4858f9c34c27739877821`

Required product commit message: `feat(ui): add accessible tooltip primitive`

Inventory source:

`signalguard-rs/phase-3/inventory/P3-MP00/6b57938d87e05d3b4fa4858f9c34c27739877821.md`

The product branch must contain exactly one normal product commit above the assigned base.

## Ownership boundary

The worker owns implementation, tests, one product commit, normal push, one draft product PR, and one connector delivery report.

The worker must not merge, edit the phase branch directly, rewrite history, force-push, modify another worker branch, update Phase 3 control files, change existing connector prompts, migrate a caller, or start another microphase.

## Remote preflight

Before editing:

1. Fetch product refs.
2. Verify `origin/refactor/dashboard-modules` equals `6b57938d87e05d3b4fa4858f9c34c27739877821`.
3. Verify `origin/p3/mp02-tooltip-primitive` equals the same SHA.
4. Check out the assigned branch without history rewriting.
5. Verify clean state and comparison `0 0` against the phase branch.
6. Read exact-base versions of:
   - `web/src/shared/components/StatusBadge.tsx`;
   - `web/src/shared/components/ErrorPanel.tsx`;
   - `web/src/shared/styles/globals.css` read-only;
   - `web/src/test/setup.ts`;
   - `web/vitest.config.ts`;
   - `web/package.json` read-only;
   - `web/src/pages/DashboardPage.tsx` read-only for future caller context.

Stop and report a blocker if identity, base, or cleanliness differs.

## Goal

Create one small accessible, dependency-free, reusable tooltip primitive with focused tests. Do not migrate any caller and do not change any current production surface.

The primitive must:

- expose content through `role="tooltip"`;
- connect trigger and tooltip with `aria-describedby` only while available;
- open on pointer hover and keyboard focus;
- close on pointer leave and focus leaving the combined group;
- close on Escape while open;
- preserve the trigger's existing handlers and accessible name;
- generate collision-free IDs for multiple instances;
- require no global CSS, provider, portal, or third-party dependency;
- remain a tooltip rather than a dialog, menu, or click-only disclosure;
- work under React Strict Mode.

## Narrow API

Use one exported `Tooltip` component with a narrow API such as:

- `content: React.ReactNode`;
- exactly one trigger child or an equivalently narrow render-trigger contract;
- optional stable `id` only when useful for testing/composition.

Do not add speculative delays, providers, registries, portals, positioning libraries, animation systems, or compound APIs.

If cloning a trigger, compose rather than overwrite handlers and refs where practical. A wrapper-based API must not break keyboard focus or trigger semantics.

## Required interaction tests

Prove at least:

- tooltip absent before interaction;
- hover opens and pointer leave closes;
- focus opens and blur/focus departure closes;
- Escape closes without activating the trigger;
- correct `aria-describedby` relationship;
- existing click/pointer/focus handlers still run;
- accessible trigger name unchanged;
- multiple instances have independent IDs and state;
- rerender creates no duplicate live IDs;
- unmount leaks no document listener;
- no portal/root/provider required.

Use no sleeps or snapshots. Do not add a package for tests.

## Authorized product paths

- new `web/src/shared/components/Tooltip.tsx`;
- new `web/src/shared/components/Tooltip.test.tsx`.

No existing product file may change.

## Forbidden product paths

Do not modify:

- `web/src/pages/DashboardPage.tsx`;
- `web/src/pages/SymbolDetailPage.tsx`;
- `web/src/app/AppShell.tsx`;
- `web/src/app/GlobalMarketTicker.tsx`;
- `web/src/app/router.tsx`;
- `web/src/shared/styles/globals.css`;
- existing shared components;
- API/query/resource/adapter/identity files;
- `web/package.json` or lockfiles;
- build/test/style config;
- backend, OpenAPI, CI, Docker, docs, deployment, or scripts;
- ticker behavior or styling.

Do not migrate Recharts `Tooltip` or any current badge/header/chart/table caller. Do not add a dependency.

## Required verification

Run, when available:

1. focused tooltip tests;
2. `cd web && npm run test:run`;
3. `cd web && npm run typecheck`;
4. `cd web && npm run lint`;
5. `cd web && npm run build`;
6. `cd web && npm run bundle:check`;
7. `git diff --check`;
8. exact two-path proof;
9. forbidden-path and ticker proof.

Report unavailable checks honestly. Do not commit after a failed required check.

## Product publication

After successful verification:

1. stage only the two authorized paths;
2. create exactly one commit with the required message;
3. push normally to `p3/mp02-tooltip-primitive`;
4. confirm ahead `1`, behind `0` relative to `origin/refactor/dashboard-modules`;
5. open one draft PR to `refactor/dashboard-modules` titled `feat(ui): add accessible tooltip primitive`;
6. include exact base/head, paths, verification, and connector report path in the PR body;
7. do not merge.

## Connector delivery report

Create exactly one new connector report after product head and draft PR exist:

`signalguard-rs/phase-3/reports/P3-MP02/<FULL_PRODUCT_HEAD_SHA>.md`

Include:

- exact task, branch, base, and product head;
- product commit message;
- draft PR number/URL;
- exact changed paths;
- component API;
- hover/focus/blur/Escape behavior;
- ARIA ID/description evidence;
- existing-handler and accessible-name preservation;
- multiple-instance/Strict Mode evidence;
- focused/full tests and all frontend gates;
- unavailable checks and reasons;
- forbidden-path/ticker proof;
- final ahead/behind count;
- explicit no-merge/no-next-task statement.

Commit only this new report in `progeranna/connector`. Do not modify connector control, status, prompt, inventory, review, or integration files.

## Definition of done

`P3-MP02-WEB1` is delivered only when the exact assigned remote branch contains one verified product commit, one draft PR targets the exact phase branch, and one immutable connector report records the product head and evidence. The Orchestrator alone reviews and integrates it.