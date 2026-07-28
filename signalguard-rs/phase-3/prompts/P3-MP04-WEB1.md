# P3-MP04-WEB1 Contract — Deterministic Semantic Descriptor Fixtures

## Execution role

You are an isolated GitHub web implementation worker for SignalGuard RS Phase 3 microphase `P3-MP04`.

Read this immutable contract from `progeranna/connector`, implement the product change in `progeranna/signalguard-rs`, publish one normal product commit to the assigned remote branch, open one draft product PR, and publish one immutable delivery report back to the connector repository.

This is a remote GitHub workflow. Do not assume or reference a user-local path, local worktree, local Docker service, or local Codex session.

## Immutable repository identity

Product repository: `progeranna/signalguard-rs`

Connector repository: `progeranna/connector`

Assigned product branch: `p3/mp04-semantic-fixtures`

Required PR base: `refactor/dashboard-modules`

Exact assigned base SHA: `5e0b186fe1aa42d1b739077fff9b14832e8e3eb1`

Required product commit message: `test(ui): add deterministic semantic fixtures`

Required parent capability:

- accepted P3-MP03 descriptor model at `web/src/features/dashboard/statusDescriptors.ts`;
- P3-MP03 integration SHA `5e0b186fe1aa42d1b739077fff9b14832e8e3eb1`.

The product branch must contain exactly one normal product commit above the assigned base.

## Ownership boundary

The worker owns implementation, tests, one product commit, normal push, one draft product PR, and one connector delivery report.

The worker must not merge, edit the phase branch directly, rewrite history, force-push, modify another worker branch, update Phase 3 control files, modify existing connector prompts, wire fixtures into production UI, modify the descriptor model, or start Wave 1.

## Remote preflight

Before editing:

1. Fetch product refs.
2. Verify `origin/refactor/dashboard-modules` equals `5e0b186fe1aa42d1b739077fff9b14832e8e3eb1`.
3. Verify `origin/p3/mp04-semantic-fixtures` equals the same SHA.
4. Check out only the assigned branch without history rewriting.
5. Verify clean state and comparison `0 0` against the phase branch.
6. Read exact-base versions of:
   - `web/src/features/dashboard/statusDescriptors.ts`;
   - `web/src/features/dashboard/statusDescriptors.test.ts`;
   - `web/src/shared/lib/status.ts` read-only;
   - `web/src/test/uiSmokeMatrix.ts` read-only;
   - `web/src/test/marketFixtures.ts` read-only;
   - Phase 3 execution-plan Wave 0 and Checkpoint 0 requirements.
7. Inventory every exported descriptor key, detector mapping, Data Age state, tooltip-fact state, and time-fact key before creating fixtures.

Stop and report a blocker if identity, base, cleanliness, or accepted P3-MP03 exports differ.

## Goal

Create reusable, pure, deterministic fixture data and completeness tests for every accepted P3-MP03 semantic state.

The fixture layer is test infrastructure for later component and compositor work. It must not change any current product presentation, visible copy, route, resource behavior, API boundary, styling, or runtime behavior.

After this microphase, later tests can import one canonical fixture source instead of recreating status, anomaly, Data Age, detector, tooltip-fact, and time-fact examples ad hoc.

## Fixture design rules

The fixture module must:

- be plain TypeScript with no JSX;
- be deterministic and importable in a Node test environment;
- contain no React runtime import, hook, DOM access, network/cache/store access, timer, current-time call, locale formatter, random value, environment lookup, or side effect;
- use stable explicit string IDs;
- use readonly literal data where practical;
- preserve numeric zero and exact supplied display strings;
- avoid snapshots and sleeps;
- never introduce Replay as a public mode;
- not call the production functions under test while constructing expected fixture values.

Fixtures must provide explicit `input` and `expected` data. Completeness tests may call the accepted P3-MP03 pure functions and compare their results to fixture expectations.

Do not build expected values by calling the same production function during fixture creation; that would make the tests tautological.

## Required fixture groups

### 1. System status fixtures

Provide exactly one canonical fixture for every accepted system key:

- `healthy`;
- `degraded`;
- `critical`;
- `offline`;
- `unknown`.

Each fixture must include at least:

- stable fixture ID;
- key input;
- exact expected key;
- exact expected visible label;
- expected existing `StatusTone` value;
- exact expected explanatory description from the accepted descriptor model.

### 2. Market status fixtures

Provide exactly one canonical fixture for every accepted market key:

- `healthy`;
- `degraded`;
- `critical`;
- `stale`;
- `no_data`.

Each fixture must include the same expected descriptor fields as system fixtures. Keep stale, no-data, availability, and generic degradation semantically distinct.

### 3. Anomaly severity fixtures

Provide exactly one canonical fixture for every accepted severity:

- `info`;
- `warning`;
- `critical`.

Each severity fixture must include:

- stable ID;
- severity input;
- known detector input;
- exact expected severity descriptor;
- exact expected detector label;
- exact expected combined active label using `<Severity label> · <Detector label>`.

Use the accepted examples across the group so the fixtures include:

- `Info · Stale Data`;
- `Warning · Spread Spike`;
- `Critical · Price Move`.

Also provide one explicit no-active-anomalies fixture for `No Active Anomalies` and its neutral tone/description.

### 4. Detector label fixtures

Provide canonical fixtures covering:

- every current known detector identifier exactly once;
- at least one unknown normal snake_case identifier;
- one identifier containing repeated/leading/trailing underscores;
- the empty identifier.

Expected labels must be literal and deterministic. Unknown identifiers must not map to a different known detector.

### 5. Data Age fixtures

Use fixed canonical thresholds:

- `delayedAfterMs = 1000`;
- `staleAfterMs = 5000`.

Provide explicit cases covering at least:

- `ageMs = null` → `no_data`;
- `ageMs = 0` → `fresh`;
- `ageMs = 999` → `fresh`;
- `ageMs = 1000` → `delayed`;
- `ageMs = 4999` → `delayed`;
- `ageMs = 5000` → `stale`;
- one value above the stale boundary → `stale`.

Each case must include:

- stable ID;
- full input object;
- expected Data Age key;
- exact expected descriptor label, tone, and description.

Also include explicit invalid-input fixtures for:

- negative age;
- non-finite age;
- negative delayed threshold;
- non-finite delayed threshold;
- negative stale threshold;
- non-finite stale threshold;
- reversed thresholds.

Each invalid fixture must specify the exact expected error class and stable error message. Do not execute throwing functions while constructing fixture data.

### 6. Tooltip fact fixtures

Provide canonical fixtures proving:

- normal non-empty string is preserved;
- numeric zero is preserved;
- explicit display text such as `0 ms` is preserved;
- empty string is omitted;
- `null` is omitted;
- `undefined` is omitted.

Each fixture must contain stable input and literal expected output or expected `null`.

### 7. Time fact fixtures

Provide exactly one canonical fixture for every accepted time key:

- `last_evaluated` → `Last evaluated`;
- `last_event` → `Last event`;
- `detected` → `Detected`.

Supply explicit display values. At least one case must preserve numeric zero. Do not call `Date.now`, `new Date`, locale formatting, or implicit date formatting.

## Required exports

Use clear exported readonly groups. Exact symbol names may be chosen consistently, but the module must export:

- system status fixtures;
- market status fixtures;
- anomaly severity fixtures;
- no-active-anomalies fixture;
- detector fixtures;
- valid Data Age fixtures;
- invalid Data Age fixtures;
- tooltip fact fixtures;
- time fact fixtures;
- one deterministic grouped inventory and/or flattened inventory suitable for unique-ID completeness checks.

Do not export React nodes, classes, colors, icons, Tailwind classes, or components.

## Required completeness tests

Tests must prove at least:

1. every system key appears exactly once;
2. every market key appears exactly once;
3. every anomaly severity appears exactly once;
4. every current detector identifier appears exactly once in the known-detector fixtures;
5. all four Data Age states are represented;
6. exact Data Age boundary behavior matches the accepted model;
7. every invalid Data Age fixture throws the specified error class and message;
8. exact descriptor labels, tones, descriptions, detector labels, and active anomaly labels match fixtures;
9. no-active-anomalies semantics match exactly;
10. tooltip facts preserve zero and explicit display text while omitting only the specified absent/empty values;
11. all three time-fact keys and labels are covered exactly once;
12. all fixture IDs are unique and group order is deterministic;
13. fixture construction is non-tautological and does not call production functions to create expected values;
14. fixture source has no JSX, React runtime import, hook, DOM/current-time/random/network/cache/store/locale dependency;
15. Replay does not appear as a public mode concept;
16. imports require no browser globals.

Use no snapshots, sleeps, random values, current time, locale-dependent assertions, backend service, or network call.

## Authorized product paths

- new `web/src/test/statusDescriptorFixtures.ts`;
- new `web/src/test/statusDescriptorFixtures.test.ts`.

No existing product file may change.

## Forbidden product paths

Do not modify:

- `web/src/features/dashboard/statusDescriptors.ts`;
- `web/src/features/dashboard/statusDescriptors.test.ts`;
- `web/src/test/uiSmokeMatrix.ts`;
- `web/src/test/uiSmokeMatrix.test.ts`;
- `web/src/test/marketFixtures.ts`;
- `web/src/shared/lib/status.ts`;
- `web/src/shared/components/Tooltip.tsx`;
- any page/app/component/router file;
- `web/src/app/GlobalMarketTicker.tsx`;
- `web/src/shared/styles/globals.css`;
- API/query/resource/adapter/identity files;
- `web/package.json` or lockfiles;
- build/test/style configuration;
- backend, OpenAPI, CI, Docker, docs, deployment, or scripts;
- ticker behavior or styling.

Do not add a dependency. Do not wire fixtures into current production code. Do not begin P3-MP05 or any other Wave 1 task.

## Required verification

Run, when available:

1. focused semantic-fixture tests;
2. `cd web && npm run test:run`;
3. `cd web && npm run typecheck`;
4. `cd web && npm run lint`;
5. `cd web && npm run build`;
6. `cd web && npm run bundle:check`;
7. `git diff --check`;
8. exact two-path proof;
9. forbidden-path, generic-palette, tooltip, and ticker proof;
10. proof that the fixture module imports in Node without browser globals;
11. proof that expected fixture data is literal and is not generated by calls to the production functions under test.

Report unavailable checks honestly. Do not commit after a failed required check.

## Product publication

After successful verification:

1. stage only the two authorized new paths;
2. create exactly one commit with message `test(ui): add deterministic semantic fixtures`;
3. push normally to `p3/mp04-semantic-fixtures`;
4. confirm ahead `1`, behind `0` relative to the exact assigned base;
5. open one draft PR to `refactor/dashboard-modules` titled `test(ui): add deterministic semantic fixtures`;
6. include exact base/head, paths, fixture inventory, verification, and connector report path in the PR body;
7. do not merge.

If `refactor/dashboard-modules` advances after successful preflight, do not rewrite the worker branch. Preserve the one-commit candidate, report the moving-base divergence honestly, and leave refreshed merge-tree handling to the Orchestrator.

## Connector delivery report

Create exactly one new connector report after product head and draft PR exist:

`signalguard-rs/phase-3/reports/P3-MP04/<FULL_PRODUCT_HEAD_SHA>.md`

Include:

- exact task, branch, assigned base, and product head;
- product commit message;
- draft PR number and URL;
- exact changed paths;
- exported fixture groups and exact counts;
- system/market/anomaly/Data Age/detector/fact/time coverage;
- stable-ID and deterministic-order evidence;
- non-tautological expected-data proof;
- focused/full tests and all frontend gates;
- unavailable checks and reasons;
- forbidden-path, palette, tooltip, and ticker proof;
- final ahead/behind count;
- explicit no-merge/no-Wave-1 statement.

Commit only this new report in `progeranna/connector`. Do not modify connector control, status, prompt, inventory, review, or integration files.

## Definition of done

`P3-MP04-WEB1` is delivered only when the exact assigned remote branch contains one verified product commit, one draft PR targets the phase branch, and one immutable connector report records the exact product head and evidence. The Orchestrator alone reviews and integrates it.
