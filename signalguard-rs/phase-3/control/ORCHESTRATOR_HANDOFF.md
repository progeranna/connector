# SignalGuard RS Phase 3 — Orchestrator Handoff

Updated: 2026-08-10 01:54 +03:00

Purpose: durable restart context for a new orchestrator. This file is a control-plane handoff, not a product specification by itself. It summarizes current exact authority, accepted product identity, recovery history, worker protocol, permanent invariants, and the only legal continuation path.

## 1. Read order and authority precedence

A new orchestrator must read in this order before taking any action:

1. `signalguard-rs/phase-3/control/ORCHESTRATOR_HANDOFF.md`
2. `signalguard-rs/phase-3/control/CURRENT_EXECUTION.md`
3. `signalguard-rs/phase-3/control/STATUS.md`
4. the exact currently authorized contract named by `CURRENT_EXECUTION.md`
5. the reports/contracts explicitly referenced by that contract
6. `signalguard-rs/phase-3/control/IMPLEMENTATION_SEQUENCE.md`
7. `signalguard-rs/phase-3/control/MICRO_PHASE_LEDGER.md`
8. `signalguard-rs/phase-3/control/RESUMPTION_PLAN.md`

`CURRENT_EXECUTION.md`, `STATUS.md`, and the exact current contract are the live execution authority. Older project-bundle files such as uploaded `PROJECT_STATUS.md`, `WORKFLOW.md`, `AGENTS.md`, `HANDOFF_SPEC.md`, and historical phase documents remain useful for general discipline, but they must not override newer connector control-plane state.

If any identity or state in this handoff disagrees with a newer `CURRENT_EXECUTION.md`/`STATUS.md`, stop and resolve the newer connector evidence first.

## 2. Current exact state

Current state:

`P3_CHECKPOINT_2R_RERUN_AFTER_R3_LOCAL_VALIDATION_AUTHORIZED`

Current product repository:

`progeranna/signalguard-rs`

Target product branch:

`refactor/dashboard-modules`

Exact accepted integrated commit:

`7dab5647d322339f5bd9d0514e5178522d5181c0`

Exact accepted tree:

`d5ca241f173f2733d6699283084bf7435c0e9259`

The target branch was independently verified identical to this commit after R3 integration.

Current authorized action only:

`P3-CHECKPOINT-2R-RERUN-AFTER-R3 — Full combined modal-only recovery validation`

Current contract:

`signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-RERUN-AFTER-R3-LOCAL.md`

Contract publication commit:

`846b9b456e9577e4e50b3ed2123b50af15c6b8de`

Contract blob:

`8e9097eae024b004f9a794d6a65cb821eae9a397`

Contract status:

`P3_CHECKPOINT_2R_RERUN_AFTER_R3_LOCAL_VALIDATION_AUTHORIZED`

Worker type: dedicated local Codex validation worker using `$rust-development`.

Product write lease: `NONE`.

Success marker:

`P3_CHECKPOINT_2R_RERUN_AFTER_R3_COMPLETE`

Blocker marker:

`P3_CHECKPOINT_2R_RERUN_AFTER_R3_BLOCKED`

Do not authorize Bridge 01, Bridge 02, Wave 4, or any product mutation before this rerun is independently accepted.

## 3. Current accepted CI/bundle floor

Latest exact-ref R3 PR CI:

- PR: `#73`
- synthetic merge: `3b949b7e94f7a7ebe3d5e2b8e2bd2c8e10e59514`
- workflow run: `31309410396`
- attempt: `1`
- result: `success`
- frontend job: `93234775362`, success
- rust job: `93234775345`, success
- both jobs independently verified to checkout the exact synthetic merge SHA
- frontend: 44/44 Vitest files, 614/614 tests
- TypeScript: pass
- ESLint zero warnings: pass
- production build: pass
- bundle-policy tests: 25/25
- Rust formatting/API/OpenAPI/check/Clippy/tests/replay discovery/Docker/shell gates: pass
- no CI rerun was used

Current bundle measurements:

- initial JS: `389599` bytes
- largest JS: `389599` bytes
- total JS: `389599` bytes
- initial limit: `409600`
- largest limit: `409600`
- total limit: `414720`

Budget increases are forbidden unless a future explicit contract authorizes them. Do not weaken the bundle policy to make a phase pass.

## 4. Recovery/integration history that produced the current head

### Phase 3.5 accepted baseline

Final Phase 3.5 accepted SHA before the recovered Phase 3 work:

`09e0cbaa8cafd7c0523bb4ed539c01b2f7ad0b27`

The modal-only recovery predecessor was integrated by PR #68 and produced the original accepted Phase 3 base:

- commit: `ba31a348dc5055935c45f6be81073688caedd925`
- tree: `f629b6ea4339c92d03223c3bd8024cd4cb4571da`

### P3-MP18R — exact anomaly detail from Symbol Detail

Purpose: recover exact UUID-keyed anomaly activation from Symbol Detail while retaining Dashboard-owned modal navigation.

Important history: the original 10-file lease proved insufficient. A diagnostic found two additional stale tests, so the corrected R1 lease contained 12 exact paths. Do not repeat the original incomplete lease.

Accepted worker:

- branch: `p3/mp18r-exact-symbol-anomaly-detail`
- commit: `664daebc9bc63a761ea8db205f9ae345f0d0c622`
- tree: `65c816c76a5f9e31858cdcb29acd523e8a92c122`
- parent: `ba31a348dc5055935c45f6be81073688caedd925`
- message: `fix(ui): open exact anomaly detail from symbol detail`

Integration:

- PR #69
- final merge: `6142ec7004b75cda077a49ab37bcfdca01f7f8e8`
- final tree: `65c816c76a5f9e31858cdcb29acd523e8a92c122`
- integration report publication: connector commit `32a883eb79a713fbffee6d8fcc1f3f4cb347ef9d`

Behavior recovered:

- Symbol Detail anomaly activation opens exact UUID-keyed Anomaly Detail
- exact anomaly identity is not derived from symbol/type/position
- Back/focus semantics remain local-modal behavior
- no standalone anomaly page and no URL-backed modal state

### P3-MP20R — remove obsolete route/popup presentation residue

Purpose: remove obsolete route/popup presentation shape and make anomaly observed/threshold values surface-neutral direct strings.

Important execution-mode history: an original MP20R contract incorrectly targeted local Codex although the user had launched a GitHub web worker. That blocker was classified as `EXECUTION_MODE_MISMATCH`, not product drift. The local diagnostic produced during that mistake is superseded. The authoritative implementation contract was `P3-MP20R-WEB.md`.

Accepted worker:

- branch: `p3/mp20r-route-presentation-residue`
- commit: `1b09f69d79333872eeed47b00407b6ae09727822`
- tree: `d8f9e71e7aec5fcf7b472011a68247a6df42bbac`
- direct base: `6142ec7004b75cda077a49ab37bcfdca01f7f8e8`
- message: `refactor(ui): remove obsolete route presentation residue`
- exact lease: five files
- aggregate diff: +25/-46

Integration:

- PR #70
- final merge before Checkpoint 2R: `8bbef01d7d9979c4996954171a0e7c3748f02538`
- tree: `d8f9e71e7aec5fcf7b472011a68247a6df42bbac`
- implementation report publication: connector commit `9870049601679240e5d7ac0d9ce9428cfe2184a5`
- independent review: connector commit `79bfb5b37ea9ca3459e1fa5c9292cfd0d8a6d365`
- integration report publication: connector commit `56e6ca94551285aaa1f4d3edcb0daf42e8634132`

Formatting that must remain preserved:

- spread_spike / price_move: three-decimal percent
- event_lag_spike / stale_data / quote_stuck: ms below 1000, one-decimal seconds at/above 1000
- trade_burst: integer ` /m`
- depth_sequence_gap: observed ` gap`, threshold ` limit`
- unknown numeric: max three fractional digits
- null/NaN: `—`

### Checkpoint 2R first run — blocked on unreachable All modals

At product head `8bbef01d...`, command gates passed but the real Demo data contained seven markets and three recent anomalies while both `View all` controls were gated on `preview.hasMore`. Therefore required All Markets / All Anomalies real-browser flows were unreachable.

Original blocker report publication:

`e2f8993d0b84773bbf5958b3647b3741a2e6d415`

### R1 — View-all reachability recovery

Accepted worker:

- branch: `p3/checkpoint2r-view-all-reachability`
- commit: `f793b8447076a9feb8227447c2b851622475ef7c`
- tree: `9bdfdcf331ef08cdeaf8f21a8ab66adee3092fe8`
- base: `8bbef01d7d9979c4996954171a0e7c3748f02538`
- message: `fix(ui): keep dashboard modal entry points reachable`
- exact diff: three files, +98/-13

Product result:

- Market Health `View all` exists whenever the market collection is non-empty
- Recent Anomalies `View all` exists whenever the anomaly collection is non-empty
- empty collections still expose no View-all action
- preview limits were not changed
- no artificial Demo records were added

Integration:

- PR #71
- final merge: `9cedbeb9c9e5e59ad634123a3b2d6217555a5c96`
- tree: `9bdfdcf331ef08cdeaf8f21a8ab66adee3092fe8`
- implementation report publication: connector commit `a40dda39fda5fc0aed9571c3285bf3d9da4f7ad2`

### Checkpoint 2R rerun after R1 — blocked on All Markets second-Back focus

At `9cedbeb9...`, all command gates passed. The deterministic real-browser failure was:

`All Markets → BTCUSDT Symbol Detail → exact Anomaly Detail → Back → Back`

The first Back correctly restored the exact anomaly UUID trigger. The second Back remounted All Markets but focused `Close` instead of the originating BTCUSDT row/card. The cause was controller-local: All Anomalies already carried a return-focus identity while All Markets state was only `{type:"symbols"}` and supplied no `initialFocusSelector`.

Blocker report publication:

`6c4b2e6858b7ce2d8a348f3129e0e1aab3413e4b`

### R2 — All Markets Back focus recovery

Accepted worker:

- branch: `p3/checkpoint2r-all-markets-back-focus`
- commit: `dee3f17919b21dec1fbe701e069103c064f05dd4`
- tree: `495d14862b0996766b5376358b99382124df9916`
- base: `9cedbeb9c9e5e59ad634123a3b2d6217555a5c96`
- message: `fix(ui): restore all-markets back focus`
- exact diff: two files, +102/-4

Product result:

- All Markets return state carries optional exact `focusSymbol`
- Back from Symbol Detail can remount All Markets and request focus on the originating symbol
- shared modal `initialFocusSelector` and existing browser-visible focus selection are reused
- hidden responsive duplicates are not the intended focus target
- no `SymbolPopupIdentity`, anomaly UUID, shared Dialog, routes, resources, CSS, ticker, or Demo/Live semantics were changed

Integration:

- PR #72
- final merge: `cbf5c543ada8752c273fbb2e91be029c9febc3d3`
- tree: `495d14862b0996766b5376358b99382124df9916`
- integration report publication: connector commit `ff6ac3026f0332a7360d63c14baa0c8c482efeb5`

### Full Checkpoint 2R rerun after R2 — blocked on favicon console 404

At `cbf5c543...`, all automated command gates passed and R1/R2 focus behavior was no longer the first blocker. A fresh Chrome context automatically requested `/favicon.ico`; production preview returned 404, producing one deterministic unexpected browser console error. Page errors and unhandled promise rejections were zero.

The accepted tree had no favicon declaration and no favicon asset. This was classified as a separate pre-existing/static-document issue, not an R1/R2 regression.

Blocker report publication:

`974512cb1b9e934c25d5ccfc2c3874767dbf631d`

### R3 — prevent missing favicon browser request

Accepted worker:

- branch: `p3/checkpoint2r-favicon-console`
- commit: `778b23b6a9dbb4e1b652e7a31349a35b707f3373`
- tree: `d5ca241f173f2733d6699283084bf7435c0e9259`
- base: `cbf5c543ada8752c273fbb2e91be029c9febc3d3`
- message: `fix(ui): prevent missing favicon request`
- exact product diff: only `web/index.html`, +1/-0

Exact implementation:

`<link rel="icon" href="data:image/svg+xml,%3Csvg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 1 1%22%3E%3C/svg%3E" />`

No favicon file/static asset was added.

Worker browser proof showed fresh Chrome contexts for `/dashboard` and `/` with zero `/favicon.ico` requests, zero console errors, zero page errors, and zero unhandled rejections, without request interception/mocking.

Independent R3 review:

- connector commit: `d58a9af0ec2fd78724011b6095828bd754909d5d`
- status: `P3_CHECKPOINT_2R_R3_FAVICON_ACCEPTED_FOR_INTEGRATION`

Integration:

- PR #73
- synthetic merge: `3b949b7e94f7a7ebe3d5e2b8e2bd2c8e10e59514`
- exact-ref CI: run `31309410396`, attempt 1, success
- final normal merge: `7dab5647d322339f5bd9d0514e5178522d5181c0`
- final tree: `d5ca241f173f2733d6699283084bf7435c0e9259`
- integration report: `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R3-INTEGRATION/7dab5647d322339f5bd9d0514e5178522d5181c0.md`
- integration report publication commit: `60ac20579fa1b51901fb0b3850e273989fdcf77f`

## 5. Permanent product invariants

These are not optional cleanup preferences. Preserve them unless a future explicit contract changes them.

### Navigation and modal ownership

- `/` and `/dashboard` are the only visual console pages.
- `/symbols/:symbol` and `/anomalies` are compatibility replacement redirects to `/dashboard`.
- Market activation opens Dashboard-owned Symbol Detail modal.
- Symbol Detail anomaly activation opens exact UUID-keyed Anomaly Detail.
- All Anomalies rows open exact Anomaly Detail, never Symbol Detail.
- View all anomalies opens All Anomalies modal.
- All Markets opens a Dashboard-owned modal and can drill into Symbol Detail.
- Modal state is local/ephemeral, not URL-synchronized.
- Standalone visual Symbol Detail/Anomalies pages are forbidden.
- Modal identity must never be serialized into the URL.
- Backend `/anomalies` API remains valid and must not be removed merely because the visual route redirects.

### Identity and isolation

- Exact anomaly ownership is by UUID, never display position or derived presentation identity.
- Symbol identity must remain canonical and resource/query ownership must remain symbol-specific.
- Demo and Live data are strictly isolated.
- Demo fixtures must never silently populate Live.
- Deferred/out-of-order resource results must not flash stale content after mode/symbol replacement.
- Missing data is explicit unavailable/null state, not data borrowed from another symbol/mode.
- Public Replay remains forbidden.
- Global ticker ownership is protected.

### Focus/accessibility behavior already recovered

- nested Anomaly Back restores exact visible anomaly trigger
- All Anomalies Back restores exact visible anomaly row/card
- All Markets nested second Back restores the exact originating visible market row/card
- hidden responsive duplicates must not receive restored focus
- direct modal initial focus remains correct
- Tab/Shift+Tab containment, Escape, explicit Close, backdrop close, and body-scroll lock/restoration are checkpoint obligations

### Vocabulary

Preserve established product vocabulary:

- System Healthy / Degraded / Critical / Offline / Unknown
- Market Healthy / Degraded / Critical / Stale / No Data
- Warning · Spread Spike
- Critical · Price Move
- Info · Stale Data
- No Active Anomalies
- Data Age: Fresh / Delayed / Stale / No Data
- Demo Mode / Live Mode

## 6. Worker-role protocol

### GitHub web implementation worker

Use for a contract that can be executed exclusively with connected GitHub data/writes. It must not claim local commands/browser execution. It creates only the authorized product commit on the assigned branch, publishes the connector report, and does not open a PR unless the contract explicitly says so.

### GitHub web integration worker

Use only after independent acceptance. It must:

1. re-verify exact target and worker identities;
2. verify worker ancestry/merge base and exact accepted diff;
3. create exactly the authorized PR;
4. resolve the PR synthetic merge SHA;
5. verify ordered parents/tree/effective diff and no merge-only content drift;
6. locate PR-triggered CI for that exact synthetic merge;
7. independently inspect job metadata/steps/logs and prove both Frontend and Rust checked out the exact synthetic SHA;
8. require first-attempt deterministic success unless the contract explicitly permits recovery;
9. normal-merge only after exact-ref CI succeeds;
10. verify final merge parents/tree/diff, target branch read-back, and unchanged worker branch;
11. publish connector integration report and update control state;
12. never start the next phase inside the integration worker.

Normal merge commit is the established integration method. Squash/rebase/amend/force-push are forbidden unless a future contract explicitly changes policy.

### Local Codex validation worker

Use when the contract requires local shell, isolated services, production build/preview, real browser, focus observation, screenshots, or local environment evidence. Current Checkpoint 2R is one of these tasks.

Validation workers are read-only unless an implementation contract explicitly gives a product lease. On a deterministic defect they must capture evidence and propose a smallest recovery lease, but must not fix the defect.

## 7. Never trust a worker terminal marker by itself

After any worker returns `...COMPLETE` or `...BLOCKED`, independently verify the durable evidence before advancing control state.

For implementation completion, verify at least:

- worker branch exact SHA/tree
- direct parent/base
- commit message
- ahead/behind and merge base
- exact changed filenames/stats
- connector implementation report identity/content
- no unexpected PR/merge if worker was not authorized to integrate

For integration completion, verify at least:

- PR number/title/base/head/draft/merged state
- synthetic merge SHA/tree/parents
- exact-ref CI run and job IDs
- decoded checkout SHA evidence
- required test/build/bundle/Rust gates
- final normal merge SHA/tree/ordered parents
- final effective diff and target branch identity
- worker branch unchanged
- connector integration report and control updates

For local validation completion/blocker, verify:

- exact product identity used
- command gates actually executed and honestly reported
- browser evidence and screenshot/request/log inventory
- clean detached worktree after cleanup
- no product write
- connector validation/blocker report

## 8. Current Checkpoint 2R rerun acceptance matrix

The current R3 rerun must be full, not a narrow favicon smoke.

Core matrix:

- Demo × Live
- BTCUSDT × ETHUSDT
- desktop `1440×900` × mobile `390×844`

Eight core cells.

Mandatory flow families:

1. Dashboard market → Symbol Detail
2. Symbol Detail exact anomaly → exact Anomaly Detail → Back
3. All Markets → Symbol Detail → exact Anomaly Detail → Back → Back
4. All Anomalies → exact Anomaly Detail → Back
5. direct `/symbols/BTCUSDT`, `/symbols/ETHUSDT`, `/anomalies` replacement redirects

Explicit R1 regression:

- real Demo non-empty View-all controls visible/focusable
- All Markets and All Anomalies actually open
- no injected records

Explicit R2 regression on desktop and mobile:

`All Markets → BTCUSDT Symbol Detail → exact anomaly → Back → Back`

Require first Back exact anomaly UUID trigger and second Back exact visible BTCUSDT All Markets trigger; hidden responsive duplicates must not receive focus.

Explicit R3 regression:

- fresh contexts for `/dashboard` and `/`
- embedded favicon declaration served
- `/favicon.ico` request count exactly zero
- no request interception/mock/proxy suppression
- global unexpected console errors = 0
- page errors = 0
- unhandled promise rejections = 0

Also verify pointer, Enter, Space, mobile card activation, Tab/Shift+Tab containment, Close/Escape/backdrop, body lock/restoration, rapid Demo↔Live and BTC↔ETH replacement, no stale flash/fallback, URL invariants, and at least 16 deterministic screenshots with SHA-256 hashes outside repositories.

On first deterministic acceptance failure: stop success claims for unexecuted cells, capture exact evidence, publish blocker report, and do not patch product code.

## 9. Required current success/blocker handling

If local Codex returns:

`P3_CHECKPOINT_2R_RERUN_AFTER_R3_COMPLETE`

then a separate GitHub web checkpoint acceptance step must independently verify the report and exact current product identity. Do not directly start Bridge 01 from the Codex marker.

Only after independent checkpoint acceptance may the orchestrator authorize `P3-W4-BRIDGE01`.

If local Codex returns:

`P3_CHECKPOINT_2R_RERUN_AFTER_R3_BLOCKED`

then:

- independently read the blocker report;
- verify exact base/product cleanliness;
- classify product vs environmental defect;
- verify the proposed smallest lease against accepted source;
- publish a new narrow recovery contract only after evidence;
- do not let the validation worker implement its own fix;
- Bridge 01/02 and Wave 4 remain blocked.

## 10. Recovered roadmap after Checkpoint 2R

Authoritative resumption plan publication:

- commit `2f52a34a119c288792d68d80107fe6dfec79c8e7`
- state `P3_RESUMPTION_BASELINE_ACTIVE`

Authoritative micro-phase ledger publication:

- commit `426c971a40630eef3c2a45651eff27d22a14b780`
- state `P3_MICRO_PHASE_LEDGER_RECOVERED`

Authoritative implementation sequence publication:

- commit `5dc82e1cf06190f1027f4c5ce16f70a1aa09f76f`

Recovered continuation sequence:

```text
P3-MP18R
→ P3-MP20R
→ Checkpoint 2R
→ P3-W4-BRIDGE01
→ P3-W4-BRIDGE02
→ MP21 / MP22 / MP24        [parallel only because leases/dependencies permit]
→ MP23 / MP25 / MP27        [parallel only because leases/dependencies permit]
→ MP26
→ MP28
→ MP29
→ MP30
→ Checkpoint 3
→ MP31
→ MP31A
→ MP32 / MP33 / MP34        [parallel only because leases/dependencies permit]
→ MP35
→ MP36 / MP37B              [parallel only because leases/dependencies permit]
→ MP37A
→ MP38
→ MP40 only if MP38 accepted
→ MP41
→ MP42 and MP43             [serialize AppShell ownership]
→ MP44 / MP45               [test-first parallel]
→ MP46
→ Phase 4
```

The R1/R2/R3 Checkpoint recovery micro-phases are inserted before Bridge 01 and do not alter the recovered downstream order.

MP39 is superseded by accepted implementation and must not be resurrected as a planned micro-phase.

Phase 4 remains blocked pending Phase 3 completion through MP46. Historical Phase 4 planning directions that conflict with the resumed Phase 3 roadmap are superseded. The explicit blocking publication is connector commit `1fc22a73c00d652a7fba64a445a916222eebea01`.

## 11. Parallelism discipline

The user wants maximal safe parallelism, not indiscriminate parallelism.

Parallelize only when all of these are true:

- dependencies are already accepted/integrated;
- writable leases do not overlap;
- neither task owns a shared controller/AppShell path that creates ordering ambiguity;
- connector control explicitly permits both tasks;
- each worker has an immutable exact base appropriate for its task.

Never run a downstream phase speculatively while its predecessor checkpoint/integration is pending.

## 12. User/workflow preferences relevant to orchestration

- Prefer GitHub web workers for implementation/integration when the task is executable through connected GitHub tools.
- Use local Codex only when the contract genuinely requires local shell/browser/service execution, as the current Checkpoint does.
- Do not switch execution mode silently.
- The user commonly returns only a terminal marker. Always perform independent verification before advancing.
- Give reusable exact worker prompts with repository/path/ref/commit/blob/status identities and explicit stop conditions.
- Do not make implementation workers merge or start the next phase.
- Keep product leases exact and narrow; do not broaden on intuition.
- Preserve a durable connector report for every implementation/review/integration/checkpoint transition.

## 13. Connector/GitHub tool behavior that has mattered

- `compare_commits` is reliable for ancestry, ahead/behind, merge-base, and effective file diffs.
- `fetch_commit_workflow_runs` exposes PR-triggered runs and may be page-limited; use exact synthetic merge identity.
- `get_commit_combined_status` can be empty even when GitHub Actions exists; do not treat an empty combined status as proof that CI did not run.
- For CI acceptance, use workflow run jobs plus job steps/logs and verify the exact checkout SHA in decoded logs.
- `fetch_file` provides current blob SHA and should precede sequential connector `update_file` writes.
- Connector code/file search can lag newly published files; exact commit-message search plus exact path fetch is often more reliable immediately after publication.
- File search results and connector file references are not local filesystem paths; do not invent sandbox paths from them.
- Never call a branch-creating tool merely to discover whether a branch exists.

## 14. Superseded/mistaken artifacts to avoid

### MP20R execution-mode mistake

The original `P3-MP20R.md` local-Codex direction and the local diagnostic created after the mode mismatch are superseded. The accepted product work came through `P3-MP20R-WEB.md` and its reports/integration chain.

Do not interpret the old mode-mismatch blocker as a product defect.

### Accidental connector branch

An accidental connector branch named:

`tmp-do-not-use`

was created earlier from connector SHA `91d00cdcf90ecd27adc7a26dc6accfa5dee23814` with no intended unique work. It is not part of the roadmap or product authority. Do not use it as a source or target. Delete only as separate housekeeping if the user explicitly wants it cleaned up and the available connector supports safe branch deletion.

## 15. Source-of-truth caution about historical project artifacts

The uploaded/project-control bundle documents an older orchestration model with snapshot/handoff ZIPs and historical status values. Its general safety rules remain useful: atomic commits, exact scope, honest verification, no secret/build artifacts, no next-phase drift. However the current active project has moved to a connector-backed Phase 3 execution model with exact GitHub web workers, connector reports, exact-ref PR CI, and local Codex only for browser-capable validation.

Do not roll the project back to the older W09/main-snapshot workflow merely because those files exist. Current connector Phase 3 control is authoritative.

## 16. New-orchestrator startup checklist

Before replying to the user or issuing another worker prompt:

1. Fetch `CURRENT_EXECUTION.md` and `STATUS.md` from connector `main`.
2. Confirm both name the same state and current contract.
3. Fetch the current contract and verify its blob if the control file supplies one.
4. Compare `7dab5647d322339f5bd9d0514e5178522d5181c0` to `refactor/dashboard-modules`; it must be identical unless a newer accepted transition exists in connector.
5. Check whether a new Checkpoint rerun success/blocker report has appeared since this handoff was written.
6. If the user supplies a terminal marker, independently verify the report/evidence before changing control state.
7. If current state is still `P3_CHECKPOINT_2R_RERUN_AFTER_R3_LOCAL_VALIDATION_AUTHORIZED`, the only legitimate user action is to run/finish that local Codex validation contract.
8. If rerun succeeds, perform separate GitHub web checkpoint acceptance before Bridge 01.
9. If rerun blocks, authorize no fix until the blocker is independently reviewed against current source.
10. Never begin Bridge 02 or Wave 4 simply because Bridge 01 is planned; follow the recovered dependency chain exactly.

## 17. Current terminal continuation

```text
MP18R integrated            PR #69
→ MP20R integrated          PR #70
→ Checkpoint 2R BLOCKED     View-all reachability
→ R1 integrated             PR #71
→ Checkpoint rerun BLOCKED  All Markets second-Back focus
→ R2 integrated             PR #72
→ Checkpoint rerun BLOCKED  favicon console 404
→ R3 integrated             PR #73
→ full Checkpoint 2R rerun after R3        [CURRENT AUTHORIZED ACTION]
→ independent checkpoint acceptance
→ P3-W4-BRIDGE01
→ P3-W4-BRIDGE02
→ semantic Wave 4 P3-MP21…P3-MP30
→ Checkpoint 3
→ remaining recovered Phase 3 sequence through MP46
→ Phase 4
```

Terminal handoff state:

`P3_CHECKPOINT_2R_RERUN_AFTER_R3_LOCAL_VALIDATION_AUTHORIZED`
