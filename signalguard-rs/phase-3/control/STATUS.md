# SignalGuard RS Phase 3 — Status

Current state: `P3_CHECKPOINT_2R_RERUN_AFTER_R2_LOCAL_VALIDATION_AUTHORIZED`

## Mandatory current entry point

Read first:

`signalguard-rs/phase-3/control/CURRENT_EXECUTION.md`

Current execution publication:

- connector commit: `67d69c4088fa8d53c75c6c8573a49a52883d345f`
- blob: `4999a630e88fff3719f52b84a76ec0c562a33996`
- status: `P3_CHECKPOINT_2R_RERUN_AFTER_R2_LOCAL_VALIDATION_AUTHORIZED`

## Current accepted product

Product repository: `progeranna/signalguard-rs`

Target branch: `refactor/dashboard-modules`

Exact integrated identity:

- commit: `cbf5c543ada8752c273fbb2e91be029c9febc3d3`
- tree: `495d14862b0996766b5376358b99382124df9916`

Integrated work:

- P3-MP18R: PR #69
- P3-MP20R: PR #70
- Checkpoint 2R R1 reachability recovery: PR #71
- Checkpoint 2R R2 All Markets Back-focus recovery: PR #72

## Accepted R2 integration

R2 worker:

- branch: `p3/checkpoint2r-all-markets-back-focus`
- commit: `dee3f17919b21dec1fbe701e069103c064f05dd4`
- tree: `495d14862b0996766b5376358b99382124df9916`

PR #72:

- normal merge: `cbf5c543ada8752c273fbb2e91be029c9febc3d3`
- final tree: `495d14862b0996766b5376358b99382124df9916`
- exact effective diff: two modified files, +102 / -4

Exact-ref PR CI:

- synthetic merge: `2b66fa6e4aec329aa2d9bdc3999419f954891a3c`
- workflow run: `31255927646`, attempt 1, success, no rerun
- frontend job `93099145069`: success; exact synthetic checkout; 44/44 files, 614/614 tests, typecheck/lint/build/bundle passed
- rust job `93099145047`: success; exact synthetic checkout; formatting/API/OpenAPI/check/Clippy/tests/replay/Docker/shell gates passed
- tested synthetic tree = final tree = `495d14862b0996766b5376358b99382124df9916`
- bundle: 389599 bytes under unchanged 409600 / 409600 / 414720-byte limits

Integration report:

- path: `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R2-INTEGRATION/cbf5c543ada8752c273fbb2e91be029c9febc3d3.md`
- connector commit: `ff6ac3026f0332a7360d63c14baa0c8c482efeb5`
- blob: `84970533900d0f2687cfa7498701f9f8dcc8b64a`
- status: `P3_CHECKPOINT_2R_R2_INTEGRATION_COMPLETE`

## Current authorization

Only the full read-only Checkpoint 2R rerun after R2 is authorized.

Contract:

- path: `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-RERUN-AFTER-R2-LOCAL.md`
- connector commit: `cadc9092e9feaaa87d589da112ea5a2f281e6956`
- blob: `1c97fd7f8c1b05b0b53e2c180a05edd92eb49a77`
- status: `P3_CHECKPOINT_2R_RERUN_AFTER_R2_LOCAL_VALIDATION_AUTHORIZED`
- worker type: local Codex validation worker
- product write lease: `NONE`
- success marker: `P3_CHECKPOINT_2R_RERUN_AFTER_R2_COMPLETE`
- blocker marker: `P3_CHECKPOINT_2R_RERUN_AFTER_R2_BLOCKED`

The rerun must execute the full command/browser matrix from the integrated R2 head and explicitly revalidate:

- R1 View-all reachability on real Demo cardinalities;
- R2 exact two-step Back focus on desktop and mobile;
- Demo/Live × BTCUSDT/ETHUSDT × desktop/mobile behavior;
- pointer/keyboard/focus containment and close lifecycle;
- stale mode/symbol replacement protection;
- compatibility redirects and modal-only URL invariants;
- zero unexpected browser console errors/page errors/unhandled rejections;
- the previously observed `/favicon.ico` 404 from a fresh browser context;
- at least 16 deterministic screenshot artifacts with hashes.

A reproduced favicon console error is not pre-waived. The validation worker must block rather than fix it if it violates the zero-console acceptance contract.

## Authorization boundary

Not authorized until independent acceptance of the full rerun:

- any product modification or defect fix;
- favicon/static-asset cleanup;
- P3-W4-BRIDGE01;
- P3-W4-BRIDGE02;
- Wave 4 P3-MP21…P3-MP30;
- dialogs/accessibility;
- routing/loading/performance;
- responsive/final work;
- Phase 4 or later work.

## Binding continuation

```text
MP18R integrated
→ MP20R integrated
→ Checkpoint 2R BLOCKED
→ R1 integrated
→ Checkpoint 2R rerun BLOCKED on All Markets Back focus
→ R2 integrated
→ full Checkpoint 2R rerun after R2             [current]
→ independent checkpoint acceptance
→ P3-W4-BRIDGE01
→ P3-W4-BRIDGE02
→ P3-MP21…P3-MP30 and Checkpoint 3
```

## Permanent product direction

- `/` and `/dashboard` are the only visual console pages.
- `/symbols/:symbol` and `/anomalies` remain replacement redirects.
- Markets open Symbol Detail modal.
- Anomalies open exact UUID-keyed Anomaly Detail.
- All Anomalies rows never open Symbol Detail.
- Modal state remains local and ephemeral.
- Standalone detail pages and URL-backed modal state remain forbidden.
- Demo/Live isolation, public-Replay prohibition, ticker ownership, accessibility/focus guarantees, backend `/anomalies`, and bundle budgets remain protected.

Terminal state: `P3_CHECKPOINT_2R_RERUN_AFTER_R2_LOCAL_VALIDATION_AUTHORIZED`
