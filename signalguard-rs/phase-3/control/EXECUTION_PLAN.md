# SignalGuard RS Phase 3 — Micro-Phase Execution Plan

Status: `AUTHORITATIVE_PLANNING_BASELINE`

Planned product branch: `refactor/dashboard-modules`

This document replaces the earlier coarse Phase 3 decomposition. Phase 3 will be executed as a sequence of very small, independently testable, independently reviewable micro-phases arranged into parallel waves.

The plan combines:

- the original Phase 3 dashboard modularization, dialog accessibility, routing, code-splitting, reduced-motion, responsive and error-boundary work;
- the agreed semantic UI changes for system, market, anomaly and data-age indicators;
- the requirement that the upper ticker remain unchanged;
- continuous local UI/UX verification on a stable preview branch.

The exact starting SHA and exact path leases will be finalized only after Phase 2 is complete and audited. The wave structure, user-visible invariants, acceptance model and parallelism rules in this document are binding.

## 1. Product invariants

Phase 3 must preserve:

- existing public routes;
- both the deep-link symbol route and the symbol popup workflow;
- all existing dashboard sections;
- desktop tables and mobile cards;
- Demo and Live as the only public UI data modes;
- strict Demo/Live data isolation established in Phase 2;
- current overall composition unless a specific micro-phase explicitly changes one semantic label, tooltip, accessibility behavior or loading/error boundary;
- the upper ticker exactly as currently implemented.

The following are forbidden across the entire phase unless a later user-approved contract explicitly overrides this document:

- redesigning the dashboard layout;
- removing or merging pages;
- replacing the popup with mandatory route navigation;
- adding a public Replay mode;
- mixing Demo, Live or replay data;
- modifying ticker text, structure, order, scrolling behavior, animation or CSS;
- combining data-layer, semantic-copy, component-extraction and styling changes into one commit;
- introducing unrelated backend or product features.

## 2. Micro-phase size contract

Each micro-phase must normally satisfy all of the following:

- one concrete behavior or extraction;
- one product commit;
- one worker branch;
- one draft PR;
- usually one to three production files;
- focused tests for the changed behavior;
- no opportunistic cleanup;
- no scope expansion without a replacement contract;
- no worker-managed merge.

Extraction, wiring, visual copy, tooltip content, accessibility migration, route splitting and bundle-budget changes must be separate tasks.

## 3. Parallel execution model

Recommended active capacity:

- four to six implementation workers;
- one local Codex integration/compositor worker;
- one independent orchestrator/reviewer.

Two active workers may not own the same production path.

High-conflict paths receive a single owner per wave, especially:

- `DashboardPage.tsx`;
- router composition;
- global CSS;
- the shared dialog primitive;
- `package.json` and lockfiles;
- the stable preview worktree.

Workers create code, tests, one commit, one branch, one draft PR and one connector report. The orchestrator independently inspects exact diffs, checks, CI, semantics and path ownership before integration.

## 4. Local preview model

### Stable preview

- worktree: `worktrees/p3-preview`;
- branch: `refactor/dashboard-modules`;
- default port: `5173`;
- contains only independently accepted and integrated changes.

### Candidate preview

- worktree: `worktrees/p3-candidate-preview`;
- temporary checkout of one worker candidate;
- default port: `5174`.

This permits side-by-side review:

- `localhost:5173` — stable accepted Phase 3 state;
- `localhost:5174` — one candidate before integration.

Any user-visible task has three acceptance states:

1. `CODE_ACCEPTED`;
2. `INTEGRATED_TO_PREVIEW`;
3. `USER_UI_ACCEPTED`.

A visible change is not complete until the user has had a practical localhost review opportunity. A rejected UI detail receives a narrow repair contract; the rest of the wave does not need to be discarded.

## 5. Mandatory gates

Every worker runs focused tests and all repository gates relevant to its scope.

Frontend workers normally run:

- focused tests;
- `npm run test:run`;
- `npm run typecheck`;
- `npm run lint`;
- `npm run build`;
- `npm run bundle:check`;
- `git diff --check`;
- changed-path and repository-hygiene checks.

If Rust or shared contract code is affected, the complete Rust gates are also required.

After each accepted integration wave, the same full frontend gates run again on the combined phase tree.

## 6. UI smoke matrix

The reusable smoke matrix must cover at least:

- Demo and Live;
- BTCUSDT and ETHUSDT;
- dashboard, symbol route and symbol popup;
- desktop and mobile widths;
- loading, error, empty, unavailable and success states;
- rapid mode and symbol switching;
- route/popup data parity;
- no stale data flash from a previous symbol or mode;
- dialog keyboard behavior where relevant.

## 7. Wave 0 — Baseline and safe fan-out

### P3-MP00 — Post-Phase-2 route, component and visual inventory

Create the exact starting inventory and verify that the phase branch starts from the final accepted Phase 2 SHA.

### P3-MP01 — Reusable local UI smoke matrix

Codify the Demo/Live, BTC/ETH, route/popup and responsive test matrix without changing production presentation.

### P3-MP02 — Tooltip primitive foundation

Create one accessible tooltip primitive with no caller migrations.

### P3-MP03 — Pure status vocabulary and descriptor model

Create pure typed descriptors for:

- system status;
- market status;
- anomaly severity plus detector display;
- data-age classification;
- tooltip facts and time semantics.

No JSX wiring in this task.

### P3-MP04 — Deterministic semantic fixtures

Add stable fixtures for all statuses, anomaly severities, data ages and tooltip states.

Parallelism:

- MP01, MP02 and MP03 may run together;
- MP04 follows MP03.

Checkpoint 0: stable localhost must remain visually identical to the final Phase 2 UI.

## 8. Wave 1 — Pure dashboard models

### P3-MP05 — Timeline normalization

Extract timestamp, price and invalid-point normalization.

### P3-MP06 — Timeline chart-domain calculation

Extract deterministic Y-domain, empty-domain and bounds behavior.

### P3-MP07 — Market Health preview model

Extract sorting, preview limits and row view models.

### P3-MP08 — Recent Anomalies preview model

Extract sorting, preview limits and stable anomaly identity.

### P3-MP09 — Dashboard resource-state mapping

Extract loading, error, empty and success state mapping.

Parallelism:

- MP05, MP07, MP08 and MP09 may run together;
- MP06 follows MP05.

No layout or visible-copy changes are allowed in this wave.

## 9. Wave 2 — Independent dashboard components

### P3-MP10 — Timeline panel component

Create the timeline feature component and focused tests.

### P3-MP11 — Market Health desktop table

Create the desktop-only health table component.

### P3-MP12 — Market Health mobile cards

Create the mobile-only health cards component.

### P3-MP13 — Recent Anomalies desktop table

Create the desktop-only anomaly table component.

### P3-MP14 — Recent Anomalies mobile cards

Create the mobile-only anomaly cards component.

These five tasks may run in parallel and must not edit the dashboard composition file simultaneously.

### P3-MP15 — Dashboard compositor wiring

One compositor worker replaces inline JSX with the accepted components. It may not change data logic, labels, tooltips, CSS semantics or user-visible behavior.

Checkpoint 1: user verifies desktop and mobile dashboard composition, timeline, Market Health, Recent Anomalies, view-all actions, row clicks, Demo/Live and BTC/ETH.

## 10. Wave 3 — Shared symbol-detail presentation

Phase 2 already supplies common market resources, adapters and view models. This wave must not repeat data-boundary work.

### P3-MP16 — Shared symbol-detail header/status section

### P3-MP17 — Shared symbol metrics/state section

### P3-MP18 — Shared symbol anomaly section

These three tasks may run in parallel.

### P3-MP19 — Route migration to shared sections

Migrate `/symbols/:symbol` while preserving deep-link behavior.

### P3-MP20 — Popup migration to shared sections

Migrate the symbol popup while preserving modal behavior and existing entry points.

MP19 and MP20 may run together after MP16–MP18 are accepted because they own different containers.

Checkpoint 2: user compares BTC and ETH route versus popup in Demo and Live across loading, error, no-data and success states.

## 11. Wave 4 — Agreed semantic UI changes

This wave implements the previously approved semantic indicator work. It must not modify composition or the ticker.

### Binding visible vocabulary

System:

- `System Healthy`;
- `System Degraded`;
- `System Critical`;
- `System Offline`;
- `System Unknown`.

Market:

- `Market Healthy`;
- `Market Degraded`;
- `Market Critical`;
- `Market Stale`;
- `Market No Data` or the exact user-approved compact equivalent.

Anomaly indicator:

- `Warning · Spread Spike`;
- `Critical · Price Move`;
- `Info · Stale Data`;
- `No Active Anomalies`.

Data age:

- visible heading `Data Age`;
- `Fresh`;
- `Delayed`;
- `Stale`;
- `No Data`.

Public modes remain:

- `Demo Mode`;
- `Live Mode`.

Replay may remain an internal runtime mechanism but is not a third public UI mode. Live may not silently display demo or replay fallback data.

### Wave 4A — Parallel visible indicators

#### P3-MP21 — System status indicator

Replace ambiguous global status copy with entity-qualified system copy and focused tooltip facts.

#### P3-MP22 — Chart anomaly indicator

Display severity and detector together above the chart.

#### P3-MP23 — Data Age indicator

Replace `Freshness` with `Data Age`, classify the state and explain age versus stale threshold.

#### P3-MP24 — Market Health table vocabulary

Use explicit market-state terminology and row-level status explanations.

#### P3-MP25 — Recent Anomalies severity semantics

Add short explanations for Critical, Warning and Info severity.

MP21–MP25 may run together only after component extraction provides non-overlapping ownership.

### Wave 4B — Parallel contextual tooltips

#### P3-MP26 — Selected-market status indicator

Display entity-qualified market status and facts including score, active issue, last event and last evaluation.

#### P3-MP27 — Demo/Live mode tooltip

Keep visible labels unchanged while explaining source and isolation.

#### P3-MP28 — Health-score tooltip

Explain the composite score without changing scoring behavior.

#### P3-MP29 — Observed/threshold tooltip

Explain observed value, threshold and exceeded-by value where data exists.

#### P3-MP30 — Unified tooltip copy and format audit

Normalize tooltips to:

- entity title;
- one short explanation;
- one to three facts;
- `Last evaluated`, `Last event` or `Detected` as appropriate;
- approximately four to six lines.

The upper ticker is a forbidden path and forbidden behavior throughout Wave 4.

Checkpoint 3: each visible micro-phase is reviewed independently on localhost. The user may approve or request a narrow repair for one label or tooltip without blocking unrelated semantic workers.

## 12. Wave 5 — Accessible dialogs

### P3-MP31 — Shared accessible dialog primitive

Implement:

- portal;
- focus trap;
- initial focus;
- focus return;
- Escape close;
- backdrop close;
- body scroll lock;
- accessible label and description support.

After MP31 is accepted, run in parallel:

### P3-MP32 — Symbol popup migration

### P3-MP33 — All-markets dialog migration

### P3-MP34 — All-anomalies dialog migration

### P3-MP35 — Keyboard and focus regression matrix

Checkpoint 4: user verifies Tab containment, Escape, backdrop close, focus return, body scroll lock and unchanged popup entry points.

## 13. Wave 6 — Routing and loading architecture

### P3-MP36 — 404 page

Add a user-facing not-found route without changing valid routes.

### P3-MP37 — Route/component error boundary

Add recoverable error handling distinct from 404 behavior.

MP36 and MP37 may run in parallel.

Then execute sequentially:

### P3-MP38 — Page-level lazy route imports

### P3-MP39 — Recharts-heavy dashboard chunk extraction

### P3-MP40 — Suspense and lazy-load failure fallback

### P3-MP41 — Bundle measurement and budget update

Each performance commit must report its measured bundle effect independently.

Checkpoint 5: user verifies all routes, unknown URL, deep-link refresh and visible loading/failure fallbacks.

## 14. Wave 7 — Accessibility and responsive hardening

### P3-MP42 — Keyboard semantics for mode and symbol selectors

### P3-MP43 — Reduced motion for charts, dialogs and route transitions

Ticker behavior and ticker CSS remain forbidden.

### P3-MP44 — Timeline responsive regression suite

### P3-MP45 — Health and anomaly responsive regression suite

MP42–MP45 may run in parallel with strict path leases.

### P3-MP46 — Final desktop/mobile route-dialog smoke

Run the complete phase smoke matrix and document final user-visible behavior.

## 15. Parallel wave capacity

Expected implementation concurrency:

- Wave 0: three workers;
- Wave 1: four workers;
- Wave 2: five component workers, then one compositor;
- Wave 3: three shared-section workers, then two migration workers;
- Wave 4A: five semantic workers;
- Wave 4B: four or five tooltip workers;
- Wave 5: one primitive worker, then three migration workers;
- Wave 6: two routing workers, then sequential performance workers;
- Wave 7: four hardening workers, then final smoke.

Workers are released only when their exact base, dependencies and path leases are immutable.

## 16. Integration and user-review policy

For every worker candidate:

1. verify exact base and one-commit discipline;
2. inspect every patch independently;
3. verify path lease and forbidden paths;
4. verify focused and full gates;
5. require exact-head CI success;
6. write connector report and orchestrator verdict;
7. integrate only accepted exact head;
8. update stable preview;
9. provide the user with a focused localhost checklist for visible changes;
10. record `USER_UI_ACCEPTED` or issue a narrow repair.

A wave closes only when combined-tree CI is green and every visible item in that wave has been offered for user review.

## 17. Final Phase 3 acceptance

Before `refactor/dashboard-modules` may merge into `main`:

- all required micro-phases are accepted or explicitly removed by a documented replan;
- all public routes remain functional;
- popup and route workflows both remain functional;
- Demo/Live and BTC/ETH isolation passes;
- desktop/mobile and loading/error/empty/success smoke passes;
- dialogs pass keyboard and focus checks;
- semantic indicators and tooltips have user approval;
- ticker is unchanged;
- bundle result is measured and accepted;
- full Rust/frontend CI is green;
- the user performs the final localhost visual review.

## 18. Planning status

Current status: `WAITING_FOR_PHASE_2_COMPLETION`

Before launching P3-MP00, the orchestrator must audit the final Phase 2 file graph and publish:

- exact Phase 3 starting SHA;
- exact branch;
- exact worktrees;
- exact path leases;
- adjusted micro-phase names if Phase 2 made any item redundant;
- first-wave immutable worker contracts.

The orchestrator may combine or remove a micro-phase only through a documented plan update that preserves the product invariants and user-review model above.
