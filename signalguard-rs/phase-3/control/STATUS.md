# SignalGuard RS Phase 3 — Status

Current state: `WAVE_0_WEB_WORKERS_AUTHORIZED`

## Authoritative inputs

Authoritative execution plan:

`signalguard-rs/phase-3/control/EXECUTION_PLAN.md`

Plan creation commit:

`8787f58d0d7b9fc64e8678af83ac2933bcf44b5b`

Final Phase 2 / authoritative starting `main` SHA:

`6b57938d87e05d3b4fa4858f9c34c27739877821`

Phase 2 final merge record:

`signalguard-rs/phase-2/integration/PHASE-2/6b57938d87e05d3b4fa4858f9c34c27739877821.md`

Phase 2-to-main PR:

`https://github.com/progeranna/signalguard-rs/pull/23`

Exact-head CI run:

`30286016632` — success.

## Product branch and previews

Phase 3 branch:

`refactor/dashboard-modules`

Initial and current Phase 3 branch SHA:

`6b57938d87e05d3b4fa4858f9c34c27739877821`

The branch was created directly from the final merged Phase 2 main SHA and contains no Phase 3 product commit yet.

Required preview model:

- stable accepted preview: local integration/compositor checkout of `refactor/dashboard-modules`, port `5173`;
- candidate comparison preview: temporary local checkout of one exact reviewed candidate, port `5174`.

Visible changes require:

`CODE_ACCEPTED → INTEGRATED_TO_PREVIEW → USER_UI_ACCEPTED`

## Binding execution model

- implementation microphases and parallel waves are executed by isolated GitHub web workers;
- each web worker reads one immutable prompt from `progeranna/connector`;
- each web worker works only on its assigned remote product branch;
- each web worker creates exactly one normal product commit, pushes normally, opens one draft PR to the exact phase branch, and writes one immutable connector delivery report;
- web workers never merge;
- the Orchestrator independently reviews exact heads, PR diffs, CI, path leases, semantics, and delivery reports before integration;
- local Codex is not the implementation executor for Wave 0; it may be used later only for local preview/integration/compositor duties when explicitly authorized;
- unavailable checks are reported honestly and are never represented as passed.

## Binding product invariants

- the upper ticker is not modified;
- dashboard composition is not redesigned;
- existing public routes remain;
- Demo and Live remain the only public modes;
- strict Phase 2 Demo/Live and symbol identity isolation remains;
- popup and symbol route both remain;
- desktop tables and mobile cards remain;
- extraction, wiring, semantic copy, tooltip content, accessibility migration, route splitting, and styling are separate tasks;
- no Phase 3 task may repeat Phase 2 data-boundary work.

## P3-MP00 — Complete

Task:

Post-Phase-2 route, component, visual, responsive, test, dialog, and high-conflict path inventory.

Result:

`ACCEPT`

Inventory:

`signalguard-rs/phase-3/inventory/P3-MP00/6b57938d87e05d3b4fa4858f9c34c27739877821.md`

Inventory commit:

`1a6668b47b5bce1dd04fd6aed40560311543ad62`

P3-MP00 made no product change and no product commit. It confirmed the exact starting tree, permanently forbade ticker paths/behavior, reserved router/AppShell/DashboardPage as high-conflict paths, and published non-overlapping Wave 0 leases.

## Superseded execution contracts

The following files were incorrectly published for local Codex/worktree execution and must not be executed:

- `signalguard-rs/phase-3/prompts/P3-MP01.md` at `445068e77e3b3764b9012e3ff9b24769fa4fe59b`;
- `signalguard-rs/phase-3/prompts/P3-MP02.md` at `ef2d4ec1765e68324c0cc3330e5e7ee42ffa638d`;
- `signalguard-rs/phase-3/prompts/P3-MP03.md` at `b7fe66442d85de7ef46c921257d72bc1dbb1a26f`.

Status for all three:

`SUPERSEDED_AS_EXECUTION_SOURCE`

They remain immutable historical artifacts and are replaced by the WEB1 contracts below.

## Active Wave 0 web workers

P3-MP01, P3-MP02, and P3-MP03 are independently executable in parallel from the same exact base. No candidate is authoritative until independently reviewed at its exact pushed head.

### P3-MP01-WEB1 — Reusable UI smoke matrix

- authoritative web-worker contract: `signalguard-rs/phase-3/prompts/P3-MP01-WEB1.md`;
- contract commit: `a7f426388f3ee7f334320a632924cc0d61cf1947`;
- product branch: `p3/mp01-ui-smoke-matrix`;
- required PR base: `refactor/dashboard-modules`;
- exact initial remote SHA: `6b57938d87e05d3b4fa4858f9c34c27739877821`;
- required commit: `test(ui): define reusable smoke matrix`;
- authorized files: new `web/src/test/uiSmokeMatrix.ts`, new `web/src/test/uiSmokeMatrix.test.ts`, optional `web/src/test/marketFixtures.ts` only when strictly necessary;
- required worker delivery: one product commit, one draft PR, one connector report under `signalguard-rs/phase-3/reports/P3-MP01/<HEAD>.md`;
- status: `WEB_WORKER_EXECUTION_AUTHORIZED`.

### P3-MP02-WEB1 — Accessible tooltip primitive

- authoritative web-worker contract: `signalguard-rs/phase-3/prompts/P3-MP02-WEB1.md`;
- contract commit: `ae0960f71553b64b1ee11e29500601214fd71162`;
- product branch: `p3/mp02-tooltip-primitive`;
- required PR base: `refactor/dashboard-modules`;
- exact initial remote SHA: `6b57938d87e05d3b4fa4858f9c34c27739877821`;
- required commit: `feat(ui): add accessible tooltip primitive`;
- authorized files: new `web/src/shared/components/Tooltip.tsx`, new `web/src/shared/components/Tooltip.test.tsx`;
- no caller migration, global CSS, package, or dependency change;
- required worker delivery: one product commit, one draft PR, one connector report under `signalguard-rs/phase-3/reports/P3-MP02/<HEAD>.md`;
- status: `WEB_WORKER_EXECUTION_AUTHORIZED`.

### P3-MP03-WEB1 — Pure status descriptor model

- authoritative web-worker contract: `signalguard-rs/phase-3/prompts/P3-MP03-WEB1.md`;
- contract commit: `18396d1572e69337a5a7ca6c72790c07decf5cfe`;
- product branch: `p3/mp03-status-descriptors`;
- required PR base: `refactor/dashboard-modules`;
- exact initial remote SHA: `6b57938d87e05d3b4fa4858f9c34c27739877821`;
- required commit: `feat(ui): define status descriptor model`;
- authorized files: new `web/src/features/dashboard/statusDescriptors.ts`, new `web/src/features/dashboard/statusDescriptors.test.ts`;
- no JSX, caller wiring, shared tone-palette edit, or P3-MP04 fixture work;
- required worker delivery: one product commit, one draft PR, one connector report under `signalguard-rs/phase-3/reports/P3-MP03/<HEAD>.md`;
- status: `WEB_WORKER_EXECUTION_AUTHORIZED`.

### P3-MP04 — Blocked by P3-MP03 acceptance

Task:

Deterministic semantic fixtures for all accepted descriptor states.

Status:

`BLOCKED_BY_P3_MP03`

No branch or execution contract is published yet. Its exact base will be the accepted and integrated P3-MP03 phase SHA, not the original Wave 0 base.

## Common Wave 0 forbidden scope

All active workers must leave unchanged:

- `web/src/pages/DashboardPage.tsx`;
- `web/src/pages/SymbolDetailPage.tsx`;
- `web/src/pages/AnomaliesPage.tsx`;
- `web/src/app/AppShell.tsx`;
- `web/src/app/GlobalMarketTicker.tsx`;
- `web/src/app/router.tsx`;
- `web/src/shared/styles/globals.css`;
- all established Phase 2 API/query/resource/identity/adapter files except the new isolated descriptor path leased to MP03;
- `web/package.json` and lockfiles;
- build/test/style configuration;
- backend, OpenAPI, contract, CI, Docker, deployment, docs, and scripts;
- all ticker text, structure, order, scrolling, animation, and CSS.

No active worker owns another worker's leased path.

## Checkpoint 0

After independently accepted Wave 0 candidates are integrated into `refactor/dashboard-modules`:

- run full combined frontend gates;
- create/update the stable local preview checkout;
- confirm the stable preview remains visually identical to final Phase 2;
- confirm the ticker is byte-for-byte unchanged;
- record combined-tree CI;
- then authorize P3-MP04 from the accepted P3-MP03 result.

## Next actions

1. Dispatch three isolated web workers using only the immutable WEB1 prompt URLs/commits above.
2. Workers implement remotely, push one normal commit, open draft PRs, and publish connector reports.
3. Independently inspect exact remote heads, reports, changed paths, CI, and ticker proof.
4. Integrate only accepted exact heads into `refactor/dashboard-modules`.
5. Keep P3-MP04 blocked until P3-MP03 is accepted and integrated.
6. Do not begin Wave 1 or any visible semantic caller migration before Checkpoint 0 closes.

Only the Orchestrator updates this file.