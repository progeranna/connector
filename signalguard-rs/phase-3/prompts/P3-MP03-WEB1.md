# P3-MP03-WEB1 Contract — Pure Status Descriptor Model

## Execution role

You are an isolated GitHub web implementation worker for SignalGuard RS Phase 3 microphase `P3-MP03`.

Read this contract from `progeranna/connector`, implement the product change in `progeranna/signalguard-rs`, publish one product commit to the assigned remote branch, open one draft PR, and publish one delivery report back to the connector repository.

This is a remote GitHub workflow. Do not assume or reference a user-local path, local worktree, local Docker service, or local Codex session.

## Immutable repository identity

Product repository: `progeranna/signalguard-rs`

Connector repository: `progeranna/connector`

Assigned product branch: `p3/mp03-status-descriptors`

Required PR base: `refactor/dashboard-modules`

Exact assigned base SHA: `6b57938d87e05d3b4fa4858f9c34c27739877821`

Required product commit message: `feat(ui): define status descriptor model`

Inventory source:

`signalguard-rs/phase-3/inventory/P3-MP00/6b57938d87e05d3b4fa4858f9c34c27739877821.md`

The product branch must contain exactly one normal product commit above the assigned base.

## Ownership boundary

The worker owns implementation, tests, one product commit, normal push, one draft product PR, and one connector delivery report.

The worker must not merge, edit the phase branch directly, rewrite history, force-push, modify another worker branch, update Phase 3 control files, modify existing connector prompts, wire a caller, or start P3-MP04.

## Remote preflight

Before editing:

1. Fetch product refs.
2. Verify `origin/refactor/dashboard-modules` equals `6b57938d87e05d3b4fa4858f9c34c27739877821`.
3. Verify `origin/p3/mp03-status-descriptors` equals the same SHA.
4. Check out the assigned branch without rewriting history.
5. Verify clean state and comparison `0 0` against the phase branch.
6. Read exact-base versions of:
   - `web/src/shared/lib/status.ts`;
   - `web/src/features/dashboard/types.ts`;
   - `web/src/features/dashboard/marketViewModel.ts`;
   - `web/src/features/dashboard/marketAdapters.ts` read-only;
   - `web/src/pages/DashboardPage.tsx` read-only;
   - `web/src/app/AppShell.tsx` read-only;
   - `web/src/test/marketFixtures.ts` read-only;
   - the Phase 3 execution-plan semantic vocabulary.

Stop and report a blocker if identity, base, or cleanliness differs.

## Goal

Create one pure typed semantic descriptor model for:

- system status;
- market status;
- anomaly severity and detector display;
- Data Age classification;
- tooltip facts;
- time-fact semantics.

Do not wire JSX or change any visible label in this microphase.

The module must contain no JSX, React hook, DOM access, network/cache/store access, side effect, random value, or current-time dependency.

## Binding vocabulary

### System

Exact labels:

- `System Healthy`;
- `System Degraded`;
- `System Critical`;
- `System Offline`;
- `System Unknown`.

Typed keys: `healthy`, `degraded`, `critical`, `offline`, `unknown`.

### Market

Exact labels:

- `Market Healthy`;
- `Market Degraded`;
- `Market Critical`;
- `Market Stale`;
- `Market No Data`.

Typed keys: `healthy`, `degraded`, `critical`, `stale`, `no_data`.

Availability, freshness, and health remain distinct concepts. Do not collapse stale into unavailable or generic degradation.

### Anomaly

Severity vocabulary: `info`, `warning`, `critical`.

Current detector labels:

- `price_move` → `Price Move`;
- `spread_spike` → `Spread Spike`;
- `stale_data` → `Stale Data`;
- `trade_burst` → `Trade Burst`;
- `quote_stuck` → `Quote Stuck`;
- `event_lag_spike` → `Event Lag Spike`;
- `depth_sequence_gap` → `Depth Sequence Gap`.

Combined active labels must use:

`<Severity label> · <Detector label>`

Examples:

- `Warning · Spread Spike`;
- `Critical · Price Move`;
- `Info · Stale Data`.

No-active label: `No Active Anomalies`.

Unknown snake_case detector identifiers must format deterministically without throwing or mapping to another detector.

### Data Age

Exact labels:

- `Fresh`;
- `Delayed`;
- `Stale`;
- `No Data`.

Classifier inputs:

- `ageMs: number | null`;
- `delayedAfterMs: number`;
- `staleAfterMs: number`.

Classification:

- `null` → `no_data`;
- `ageMs < delayedAfterMs` → `fresh`;
- `delayedAfterMs <= ageMs < staleAfterMs` → `delayed`;
- `ageMs >= staleAfterMs` → `stale`.

Reject invalid negative/non-finite values, negative thresholds, and `delayedAfterMs > staleAfterMs` deterministically. Do not silently correct thresholds.

## Descriptor contract

Define a small reusable descriptor containing at least:

- stable semantic key;
- exact visible label;
- existing `StatusTone` compatible tone;
- one short explanatory sentence suitable for a tooltip.

The module may import the `StatusTone` type but must not modify `web/src/shared/lib/status.ts`.

Do not embed Tailwind classes, React nodes, icons, colors, or component names.

## Tooltip fact/time model

Define pure typed structures for later composition:

- tooltip fact with `label` and `value`;
- exact time labels `Last evaluated`, `Last event`, `Detected`.

Preserve supplied display values. Do not call `Date.now()` or format dates implicitly. Optional empty/null facts may be omitted, but numeric zero and non-empty strings must not be lost through truthiness checks.

## Tone requirements

Use existing tones only:

- healthy/fresh → `healthy`;
- degraded/delayed/warning → `degraded` or `warning` as appropriate;
- critical/stale/critical anomaly → `critical`;
- offline/no data/unknown/no active anomalies → `neutral` unless a tested existing non-alarming tone is more precise;
- info anomaly → `info`.

Do not add a `StatusTone` value.

## Required tests

Prove at least:

- exact system, market, and Data Age keys/labels;
- exact anomaly combined examples and no-active label;
- all current detector mappings;
- deterministic unknown snake_case formatting;
- null/fresh/delayed/stale and exact-boundary behavior;
- deterministic rejection of invalid Data Age inputs;
- all tones are valid existing `StatusTone` values;
- tooltip facts/time labels preserve zero and explicit supplied values;
- equal inputs return equal values with no time/DOM dependency;
- no Replay public-mode concept appears;
- no JSX or React runtime dependency is introduced.

Use no snapshots, sleeps, random values, current time, or locale-dependent assertions.

## Authorized product paths

- new `web/src/features/dashboard/statusDescriptors.ts`;
- new `web/src/features/dashboard/statusDescriptors.test.ts`.

No existing product file may change.

## Forbidden product paths

Do not modify:

- `web/src/shared/lib/status.ts`;
- `web/src/features/dashboard/types.ts`;
- `web/src/features/dashboard/marketViewModel.ts`;
- `web/src/features/dashboard/marketAdapters.ts`;
- API/query/resource/identity files;
- any page/app component;
- `web/src/app/GlobalMarketTicker.tsx`;
- `web/src/shared/styles/globals.css`;
- `web/package.json` or lockfiles;
- build/test/style config;
- backend, OpenAPI, CI, Docker, docs, deployment, or scripts;
- ticker behavior or styling.

Do not add a dependency. Do not wire descriptors into current UI. Do not create P3-MP04 fixtures.

## Required verification

Run, when available:

1. focused descriptor tests;
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
3. push normally to `p3/mp03-status-descriptors`;
4. confirm ahead `1`, behind `0` relative to `origin/refactor/dashboard-modules`;
5. open one draft PR to `refactor/dashboard-modules` titled `feat(ui): define status descriptor model`;
6. include exact base/head, paths, verification, and connector report path in the PR body;
7. do not merge.

## Connector delivery report

Create exactly one new connector report:

`signalguard-rs/phase-3/reports/P3-MP03/<FULL_PRODUCT_HEAD_SHA>.md`

Include:

- exact task, branch, base, and product head;
- product commit message;
- draft PR number/URL;
- exact changed paths;
- exported types/functions;
- exact vocabulary and tone mappings;
- Data Age boundaries and validation;
- detector formatting behavior;
- tooltip fact/time semantics;
- focused/full tests and all frontend gates;
- unavailable checks and reasons;
- forbidden-path/ticker proof;
- final ahead/behind count;
- explicit no-merge/no-next-task statement.

Commit only this new report in `progeranna/connector`. Do not modify connector control, status, prompt, inventory, review, or integration files.

## Definition of done

`P3-MP03-WEB1` is delivered only when the assigned remote branch contains one verified product commit, a draft PR targets the exact phase branch, and an immutable connector report records the product head and evidence. The Orchestrator alone reviews and integrates it.