# SignalGuard RS Phase 3.5 — Frontend Hygiene and Bundle Recovery Plan

Status: `PLANNED_NOT_STARTED`

This is a control-plane document for `progeranna/signalguard-rs`. Product code remains in the product repository; worker contracts, reports, exact-head reviews, and integration records belong in `progeranna/connector`.

## 1. Authoritative starting point

Product repository:

`progeranna/signalguard-rs`

Phase branch:

`refactor/dashboard-modules`

Immutable Phase 3.5 starting SHA:

`c06082a97254bfa2f6ebd7e29a1ad753c4acc798`

Checkpoint 2 snapshot:

`signalguard-rs/phase-3/checkpoints/Checkpoint-2/signalguard-rs-refactor-dashboard-modules-c06082a97254.zip`

Checkpoint 2 snapshot SHA-256:

`493f8805fe38ee6f978340817ae8189f19a0bbe3684767a1e7a20041b69a846d`

Post-merge CI:

`30548108769` — success.

Frontend baseline:

- 42 test files;
- 607 tests;
- typecheck pass;
- lint pass with zero warnings/errors;
- production JS raw: `761856` bytes;
- production JS gzip: `220163` bytes;
- largest-JS budget: `761856` bytes;
- total-JS budget: `761856` bytes;
- headroom: `0` bytes.

Phase 4 is blocked until Phase 3.5 reaches its checkpoint.

## 2. Why this phase exists

The zero-byte bundle headroom is not, by itself, proof that the whole frontend is poorly written. It is evidence that the current composition has no capacity for safe feature growth.

The initial GitHub inspection identified concrete cleanup candidates:

1. `web/src/app/router.tsx` imports all route pages synchronously.
2. `DashboardPage` imports `TimelinePanel` synchronously, and `TimelinePanel` imports Recharts directly.
3. `HealthScore`, score-tone selection, text classes, and bar classes are duplicated across desktop, mobile, and dashboard-modal code.
4. Market-state formatting and availability/status wording are duplicated despite the existing `marketHealthPresentation.ts` owner.
5. Anomaly formatting and severity presentation are duplicated despite the existing `recentAnomaliesPresentation.ts` owner.
6. Reusable presentation fragments such as metric cards and empty-state blocks appear repeatedly.
7. Several tests inspect exact source text and import strings. Some guards have already become stale during valid refactors.
8. TypeScript strict mode is enabled, but unused-local and unused-parameter gates are not explicitly enabled.

Phase 3.5 must distinguish three different categories:

- proven dead code or dead exports;
- duplicated logic with one accepted semantic owner;
- intentional visual duplication that should remain local because abstraction would increase complexity or bundle size.

No code is removed merely because it looks similar.

## 3. Goals

1. Recover measurable production-bundle headroom without raising the existing budget.
2. Remove proven duplicate logic and dead code.
3. Establish one owner for market-health presentation semantics.
4. Establish one owner for anomaly presentation semantics.
5. Reduce initial route cost through measured code splitting.
6. Preserve all user-visible behavior and visual presentation unless a separate visual change is explicitly authorized.
7. Reduce brittle source-text tests while preserving meaningful architectural boundary guards.
8. Produce an accepted Phase 3.5 snapshot before Phase 4 starts.

## 4. Non-goals

Phase 3.5 does not authorize:

- new product features;
- Anomaly Explorer implementation;
- route redesign;
- visual redesign;
- copy changes;
- API or backend changes;
- trading, order routing, accounts, credentials, wallets, positions, or PnL;
- Demo fallback for Live;
- dependency upgrades unrelated to evidence-backed cleanup;
- increasing the bundle budget;
- changing browser targets to hide bundle growth;
- warning suppression;
- broad formatting churn;
- speculative shared abstractions without a measured benefit.

## 5. Permanent product invariants

All workers must preserve:

- `/`;
- `/dashboard`;
- `/symbols/:symbol`;
- `/anomalies`;
- symbol-detail popup behavior;
- Demo/Live isolation;
- resource identity of at least `(uiMode, symbol)`;
- no cross-symbol or cross-mode cache contamination;
- route and popup behavioral differences;
- desktop and mobile presentation;
- loading, error, empty, unavailable, and success states;
- current accessibility and keyboard behavior;
- read-only product semantics;
- the upper ticker behavior and presentation.

## 6. Execution model

### 6.1 Worker classes

#### Local Codex workers

Use local Codex workers for:

- full-repository static analysis;
- bundle composition and sourcemap analysis;
- high-conflict production files;
- router changes;
- Timeline/Recharts splitting;
- package, TypeScript, lint, build, or CI configuration;
- any candidate requiring authoritative local `npm ci`, full tests, build, and bundle measurement.

Every Codex implementation prompt must include:

`Use the $rust-development skill.`

#### Web workers

Use web workers for:

- read-only GitHub code inventory;
- exact duplicate-block review;
- isolated leaf-module candidates with narrow path leases;
- test-only ownership-guard modernization;
- independent exact-head diff review;
- independent PR review after CI.

Web workers must not edit high-conflict files unless explicitly leased by the Orchestrator.

#### Orchestrator

Only the Orchestrator may:

- accept an audit finding as authoritative;
- publish path leases;
- create product PRs when worker policy requires it;
- mark PRs ready;
- merge PRs;
- update control status;
- authorize the next wave;
- close Checkpoint 3.5.

Workers do not merge their own PRs.

### 6.2 Worktree isolation

Each writable worker receives a separate worktree:

`/Users/anion/Desktop/work/git-signalguard-rs/worktrees/p35-mpXX`

Rules:

- never share a writable worktree;
- start from the exact assigned SHA;
- one logical normal commit per worker unless an explicit repair contract authorizes a follow-up commit;
- no rebase, amend, reset, force-push, or history rewriting;
- no worker merges;
- no product artifacts, prompts, reports, snapshots, logs, or control files are committed to the product repository.

### 6.3 Reports

Reports belong under:

`signalguard-rs/phase-3.5/reports/<TASK>/<SHA>.md`

Read-only audit outputs belong under:

`signalguard-rs/phase-3.5/inventory/<TASK>/<BASE_SHA>.md`

Worker contracts belong under:

`signalguard-rs/phase-3.5/prompts/<TASK>.md`

Status belongs under:

`signalguard-rs/phase-3.5/control/STATUS.md`

## 7. Parallel execution graph

```text
Checkpoint 2
    |
    v
Wave 0: MP00 audits (four parallel read-only workers)
    |
    v
MP00 consolidation and exact path leases
    |
    +--------------------+--------------------+
    v                    v                    v
Wave 1 MP01          Wave 1 MP02          Wave 1 MP03
Health score         Timeline formatter   Anomaly presentation
consolidation        reuse                consolidation
    |                    |                    |
    +--------------------+--------------------+
                         v
                Wave 1 integration gate
                         |
                         v
                    Wave 2 MP04
          Dashboard market-health consolidation
                         |
                         v
                    Wave 2 MP05
              Dead exports/dependencies cleanup
                         |
              +----------+----------+
              v                     v
         Wave 2 MP06A          Wave 2 MP06B
       test guards:           test guards:
       market/timeline        anomaly/symbol
              |                     |
              +----------+----------+
                         v
                Wave 2 integration gate
                         |
              +----------+----------+
              v                     v
         Wave 3 MP07           Wave 3 MP08
       route splitting       chart splitting
              |                     |
              +----------+----------+
                         v
                    Wave 3 MP09
                 bundle policy update
                         |
                         v
                  Checkpoint 3.5
                         |
                         v
                    Phase 4 P4-MP01
```

## 8. Wave 0 — Parallel read-only audit

All Wave 0 workers start from:

`c06082a97254bfa2f6ebd7e29a1ad753c4acc798`

They make no product commit and no product branch mutation.

### P3.5-MP00A — Bundle composition audit

Preferred worker: local Codex.

Purpose:

- produce the current Vite/Rollup chunk graph;
- identify the entry dependency chain;
- measure Recharts and other dependency contribution;
- identify modules duplicated across emitted chunks, if any;
- record raw and gzip size by asset;
- test route-level and chart-level split prototypes without committing them;
- estimate initial-chunk and total-JS impact.

Temporary analysis tools may be used outside the repository or without lockfile mutation. No analysis dependency is committed during MP00A.

Output:

`inventory/P3.5-MP00A/<BASE_SHA>.md`

### P3.5-MP00B — Duplicate implementation audit

Preferred worker: web worker.

Purpose:

- enumerate exact duplicate or near-duplicate production blocks;
- identify the current semantic owner for each block;
- distinguish exact duplication from intentional route/popup variants;
- rank findings by risk, expected byte reduction, and conflict surface.

Required focus:

- `HealthScore` and score-tone helpers;
- market-health formatting and availability/status labels;
- anomaly formatting and severity classes;
- metric cards;
- empty-state blocks;
- interactive table-row keyboard handlers;
- modal and section headings.

Output:

`inventory/P3.5-MP00B/<BASE_SHA>.md`

### P3.5-MP00C — Dead code, exports, dependencies, and cycles audit

Preferred worker: local Codex.

Purpose:

- run one-shot unused-local and unused-parameter TypeScript checks;
- inventory unused exported symbols;
- inventory files with no production/test importers;
- audit package dependencies and devDependencies;
- detect import cycles;
- inspect unreachable or compatibility-only branches;
- classify every result as confirmed, probable, or false positive.

No package or lockfile mutation is allowed.

Output:

`inventory/P3.5-MP00C/<BASE_SHA>.md`

### P3.5-MP00D — Test-guard maintainability audit

Preferred worker: web worker.

Purpose:

- identify tests that read production source as raw text;
- identify exact-class or exact-import assertions that protect real contracts;
- identify stale or overbroad guards that have blocked valid refactors;
- propose behavioral, type-level, or targeted boundary replacements;
- preserve guards for resource identity, forbidden dependencies, mutation, ordering, and ticker ownership.

Output:

`inventory/P3.5-MP00D/<BASE_SHA>.md`

### MP00 consolidation gate

The Orchestrator consolidates MP00A–D into:

`signalguard-rs/phase-3.5/inventory/P3.5-MP00/c06082a97254bfa2f6ebd7e29a1ad753c4acc798.md`

That consolidated inventory must publish:

- accepted findings;
- rejected false positives;
- exact Wave 1 path leases;
- measured bundle baselines;
- expected reduction ranges;
- files reserved as high conflict;
- whether each conditional later task remains justified.

No production worker starts before this gate is accepted.

## 9. Wave 1 — Parallel semantic-owner consolidation

Wave 1 workers may execute concurrently from the same accepted base because their writable path leases do not overlap.

The initial expected base is the Phase 3.5 starting SHA. The Orchestrator may replace it with a later exact accepted SHA before publishing contracts.

### P3.5-MP01 — Consolidate health-score presentation

Preferred worker: local Codex or tightly scoped web implementation worker.

Provisional path lease:

- new canonical health-score component/helper path under `web/src/features/dashboard/`;
- `MarketHealthDesktopTable.tsx` and focused tests;
- `MarketHealthMobileCards.tsx` and focused tests.

Forbidden:

- `DashboardPage.tsx`;
- `TimelinePanel.tsx`;
- router;
- package/configuration;
- visual or copy changes.

Required result:

- one implementation of score tone, text class, bar class, minimum width, compact layout, and regular layout for desktop/mobile preview callers;
- duplicate implementations removed from leased callers;
- no production-bundle increase against exact base;
- preferred raw reduction.

### P3.5-MP02 — Reuse market-health presentation in TimelinePanel

Preferred worker: local Codex.

Provisional path lease:

- `TimelinePanel.tsx`;
- `TimelinePanel.test.tsx`.

The existing `marketHealthPresentation.ts` may be modified only if MP00 proves a missing general-purpose contract and no other Wave 1 worker owns it.

Required result:

- remove local copies of market price, percent, compact-number, age, status, and availability formatting where semantics are identical;
- preserve timeline-specific date, domain, tooltip, and anomaly-marker semantics;
- no DOM or visual change;
- no production-bundle increase.

### P3.5-MP03 — Consolidate dashboard anomaly presentation

Preferred worker: local Codex because `DashboardPage.tsx` is high conflict.

Provisional path lease:

- `DashboardPage.tsx`;
- `DashboardPage.test.tsx`;
- `recentAnomaliesPresentation.ts` and focused tests only when needed.

Required result:

- dashboard anomaly modals reuse the canonical anomaly type/value/time/severity semantics;
- route/popup and preview/modal copy differences remain explicit;
- no resource, query, popup-lifecycle, or modal-ownership change;
- no production-bundle increase;
- no other worker touches `DashboardPage.tsx` during MP03.

### Wave 1 integration

Work may run in parallel. Integration is sequential.

For each candidate:

1. verify exact branch head and single logical commit;
2. inspect exact diff and path lease;
3. run focused tests;
4. run full frontend gates;
5. run build and bundle check;
6. open a draft PR only after candidate acceptance;
7. require merge-ref CI against the current phase branch;
8. merge with a normal merge commit only after independent review;
9. verify post-merge CI before integrating the next high-risk candidate.

Branches from the same base are not rebased. Current-base merge-ref CI is authoritative.

## 10. Wave 2 — Integrated cleanup and dead-code removal

### P3.5-MP04 — Consolidate Dashboard market-health presentation

Dependency:

- MP01 accepted and integrated;
- MP03 accepted and integrated.

Preferred worker: local Codex.

Primary writable path:

- `DashboardPage.tsx` and focused tests.

Purpose:

- migrate dashboard full-market modal callers to the accepted health-score owner;
- reuse accepted market-health formatting and availability/status owners;
- remove remaining dashboard-local duplicate score and formatting helpers;
- preserve all modal and popup behavior.

No other worker may edit `DashboardPage.tsx` during MP04.

### P3.5-MP05 — Confirmed dead exports, files, and dependencies

Dependency:

- MP04 integrated;
- MP00C inventory refreshed against the integrated tree.

Preferred worker: local Codex.

Rules:

- remove only confirmed unused symbols/files/dependencies;
- every deletion requires importer evidence and full test/build proof;
- no broad cleanup based solely on one static-analysis tool;
- no new dependency is introduced merely to enforce the audit;
- package or lockfile changes require a separate exact dependency justification;
- no production-bundle increase;
- zero runtime behavior change.

### P3.5-MP06A — Modernize market-health and timeline source guards

Preferred worker: web test worker.

Scope:

- test files for market-health desktop/mobile, timeline, and their presentation owners;
- no production file changes.

Purpose:

- replace stale raw-source coupling with behavior or focused boundary tests;
- retain exact guards for mutation, order, identity, query/network ownership, and forbidden fallback.

### P3.5-MP06B — Modernize anomaly and symbol-detail source guards

Preferred worker: separate web test worker.

Scope:

- anomaly preview/modal/symbol-detail test files;
- no production file changes.

Purpose:

- remove only brittle implementation-shape assertions;
- retain route/popup differences, row identity, callbacks, accessibility, and resource-identity guards.

MP06A and MP06B may run in parallel after MP05 because their test path leases must not overlap.

## 11. Wave 3 — Bundle graph recovery

Wave 3 starts only after semantic consolidation and dead-code cleanup are integrated. This ensures code splitting is measured on the cleaned tree rather than hiding duplication in async chunks.

### P3.5-MP07 — Route-level code splitting

Preferred worker: local Codex.

Primary path lease:

- `web/src/app/router.tsx`;
- router-focused tests and loading-boundary tests.

Purpose:

- lazy-load `/anomalies`;
- lazy-load symbol-detail route where contract-safe;
- preserve `/`, `/dashboard`, `/symbols/:symbol`, and `/anomalies` behavior;
- provide deterministic loading UI;
- preserve URL navigation and direct deep links;
- record initial and total JS before/after.

### P3.5-MP08 — Timeline/Recharts lazy boundary

Preferred worker: local Codex.

Primary path lease:

- `DashboardPage.tsx`, `TimelinePanel.tsx`, and focused tests only as required by the accepted design.

Purpose:

- move Recharts out of the initial application dependency graph where feasible;
- preserve the timeline shell, loading/error/empty states, selected symbol, and query ownership;
- avoid remount loops or duplicate requests;
- record initial and total JS before/after.

MP07 and MP08 may execute concurrently only after the Orchestrator confirms non-overlapping exact path leases. If MP08 requires router changes, it becomes sequential after MP07.

### P3.5-MP09 — Bundle policy refinement

Dependency:

- MP07 and MP08 integrated.

Preferred worker: local Codex.

Purpose:

- make bundle reporting distinguish entry/initial cost from total JS where reproducibly possible;
- retain total-JS non-regression protection;
- lower, never raise, limits when the cleaned measured baseline supports it;
- keep CI output deterministic and actionable;
- document every metric and asset-selection rule.

No warning threshold is raised to hide large chunks.

## 12. Quantitative acceptance targets

Every production PR must satisfy:

- exact-base raw total JS does not increase;
- existing `761856`-byte largest and total budgets remain unchanged until MP09;
- if a candidate increases production JS, it is rejected or repaired before merge;
- all test, typecheck, lint, build, and bundle gates pass.

Phase-level targets:

- mandatory positive headroom before Phase 4;
- minimum target: `8192` raw bytes of total-JS headroom;
- preferred target: `16384` raw bytes of total-JS headroom;
- preferred initial-entry asset below Vite's `500 KiB` advisory threshold after code splitting;
- no total-JS budget increase;
- no hidden regression through moving code between chunks.

If the minimum headroom target cannot be reached, Phase 3.5 remains open and the report must explain measured blockers. The budget is not raised automatically.

## 13. Validation gates

Each production candidate must run, at minimum:

```bash
cd web
npm ci
npm run test:run
npm run typecheck
npm run lint
npm run build
npm run bundle:check
```

Repository-level gates remain:

```bash
cargo fmt --check
cargo run --quiet --bin export-api-contract -- --check
cargo run --quiet --bin export-api-contract -- --validate
cargo check
cargo clippy --all-targets --all-features -- -D warnings
cargo test
cargo test --test replay_e2e
docker compose config
docker compose --profile app config
bash -n scripts/demo-replay.sh
bash -n scripts/smoke.sh
```

Before every commit:

```bash
git status --short
git diff --check
git diff --stat
git diff
```

No commit is created after a failed required gate.

## 14. Visual verification

Any task that can alter rendering, loading boundaries, responsive wrappers, modal content, chart loading, or route transitions requires localhost comparison.

Stable accepted preview:

- phase branch;
- port `5173`.

Candidate preview:

- exact candidate head;
- port `5174`.

Required surfaces:

- `/`;
- `/dashboard`;
- `/symbols/BTCUSDT`;
- `/symbols/ETHUSDT`;
- `/anomalies`;
- dashboard market popup;
- dashboard anomaly popup;
- symbol popup from all return contexts;
- desktop and mobile widths;
- Demo and Live modes;
- loading, error, empty, unavailable, and success states.

No visible change is accepted unless separately authorized.

## 15. Checkpoint 3.5

Checkpoint 3.5 requires:

- all accepted cleanup PRs merged into the phase branch;
- post-merge CI green on the final integrated SHA;
- full local frontend and Rust gates green;
- visual parity accepted;
- bundle raw/gzip, asset graph, initial cost, total cost, budgets, and headroom recorded;
- no budget increase;
- a fresh `git archive` snapshot outside the product repository;
- SHA-256 checksum;
- final status ledger;
- obsolete verified worktrees removed;
- repository clean;
- Phase 4 not started before the checkpoint closes.

Checkpoint directory:

`signalguard-rs/phase-3.5/checkpoints/Checkpoint-3.5/`

Expected terminal status:

`P3_5_CHECKPOINT_COMPLETE`

## 16. Stop conditions

Stop a worker or integration when:

- assigned base or path lease differs;
- the worktree is unexpectedly dirty;
- a required path is owned by another active worker;
- visual behavior changes without authorization;
- Demo/Live or symbol identity changes;
- production JS increases;
- the existing bundle budget is modified upward;
- a required gate fails;
- source-text guards are deleted without replacement contract coverage;
- an analysis tool reports a result that cannot be independently verified;
- a worker attempts to merge its own PR;
- a branch requires rebase, amend, reset, force-push, or history rewrite.

## 17. Immediate next action

Publish four separate read-only worker contracts for:

- P3.5-MP00A;
- P3.5-MP00B;
- P3.5-MP00C;
- P3.5-MP00D.

Run them in parallel from exact product SHA:

`c06082a97254bfa2f6ebd7e29a1ad753c4acc798`

Do not authorize any Wave 1 implementation until the Orchestrator accepts and consolidates all four inventories.