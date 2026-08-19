# P3-CHECKPOINT-2R-RERUN-AFTER-R3 — Independent blocker review

Status: `P3_CHECKPOINT_2R_RERUN_AFTER_R3_BLOCKER_REVIEW_AUTHORIZED`

## Mode

Dedicated independent GitHub web review worker.

Use only the connected GitHub tools.

Do not use a local checkout, shell, Codex CLI, GitHub CLI, filesystem repository copy, browser automation, or unconnected repository data.

This is a read-only product review. Product write lease: `NONE`.

The worker may publish only the review report authorized below in `progeranna/connector`. It must not modify product code, branches, pull requests, control files, status files, prior reports, or any other connector path.

## Reviewed blocker authority

Connector repository:

`progeranna/connector`

Blocker report:

`signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-AFTER-R3-BLOCKER/7dab5647d322339f5bd9d0514e5178522d5181c0.md`

Blocker publication commit:

`e83b4cfeb5c6b334eb94b833c39e666dc27450e7`

Expected blocker blob:

`e4e222259996fafac7c8fc8a20b3f4630772a255`

Reported status:

`P3_CHECKPOINT_2R_RERUN_AFTER_R3_BLOCKED`

Checkpoint contract:

`signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-RERUN-AFTER-R3-LOCAL.md`

Checkpoint contract publication commit:

`846b9b456e9577e4e50b3ed2123b50af15c6b8de`

Expected checkpoint contract blob:

`8e9097eae024b004f9a794d6a65cb821eae9a397`

Read both completely before forming a conclusion.

## Exact accepted product identity

Product repository:

`progeranna/signalguard-rs`

Target branch:

`refactor/dashboard-modules`

Exact accepted commit:

`7dab5647d322339f5bd9d0514e5178522d5181c0`

Expected tree:

`d5ca241f173f2733d6699283084bf7435c0e9259`

The accepted commit has ordered parents:

1. `cbf5c543ada8752c273fbb2e91be029c9febc3d3`
2. `778b23b6a9dbb4e1b652e7a31349a35b707f3373`

First independently prove the target branch is still exactly the accepted identity. A drifted target is a hard review blocker.

## Required independent review

Review the blocker evidence without assuming its diagnosis is correct.

At minimum:

1. Verify the blocker report is immutable at the exact publication commit/blob above.
2. Verify the product target has zero commit/file drift from the accepted commit.
3. Inspect the exact accepted product source relevant to Dashboard modal replacement and per-mode selected-symbol ownership.
4. Inspect existing popup tests relevant to mode/symbol replacement.
5. Determine whether the reported browser state is internally consistent with the source:
   - after `Demo/BTCUSDT → Live/BTCUSDT → Live/ETHUSDT → Demo`;
   - header resolves to Demo's stored selected symbol `BTCUSDT`;
   - nested Live anomaly UUID clears;
   - an already-open Symbol Detail parent can remain owned by `ETHUSDT`.
6. Determine whether this violates the checkpoint requirement that stale mode/symbol identity disappear immediately and that the open modal be owned by the resolved selected symbol of the new mode.
7. Confirm whether R1 View-all reachability, R2 Back-focus restoration, R3 favicon behavior, routes, API/resources, ticker ownership, CSS, bundle policy, and backend behavior are outside the causal surface.
8. Independently determine the smallest safe recovery lease. Do not accept the proposed lease merely because the blocker report proposed it.

## Expected recovery decision if the blocker is accepted

If independently supported, authorize the orchestrator to prepare a new narrow recovery micro-phase:

`P3-CHECKPOINT-2R-R4 — Reconcile open Symbol Detail ownership on mode replacement`

The expected maximum product lease is:

- production: `web/src/pages/DashboardPage.tsx`
- tests: `web/src/pages/DashboardPage.popup.test.tsx`

The intended behavioral correction is limited to atomically reconciling an open Symbol Detail parent to both the new mode and that mode's resolved selected symbol while continuing to clear stale nested anomaly UUID state.

The reviewer may narrow this lease further. It must reject any need to broaden the lease unless the exact accepted source proves broader ownership is necessary.

Forbidden adjacent scope includes:

- routes or URL-backed modal state;
- CSS or visual redesign;
- ticker code;
- API/resource models or backend code;
- R2 focus-return logic except insofar as the reviewer verifies it is not causal;
- favicon/static assets;
- dependencies or lockfiles;
- bundle budgets;
- Bridge01/Bridge02;
- semantic Wave 4 or any later phase work.

## Report publication

On completion, publish exactly one new report:

`signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-AFTER-R3-BLOCKER-REVIEW/7dab5647d322339f5bd9d0514e5178522d5181c0.md`

The report must record:

- exact reviewed connector authority and blobs;
- exact product identity and remote drift result;
- source/test evidence inspected;
- independent causal conclusion;
- accepted or rejected blocker classification;
- exact smallest recovery lease if accepted;
- protected adjacent scope;
- next allowed orchestration step.

Do not update `CURRENT_EXECUTION.md` or `STATUS.md`; the orchestrator owns the next control transition.

## Terminal markers

If the blocker is independently accepted and R4 is required:

`P3_CHECKPOINT_2R_RERUN_AFTER_R3_BLOCKER_ACCEPTED_R4_REQUIRED`

If the evidence is insufficient, contradictory, product identity has drifted, or the proposed causal surface cannot be independently verified:

`P3_CHECKPOINT_2R_RERUN_AFTER_R3_BLOCKER_REVIEW_BLOCKED`

No product fix, implementation branch, PR, merge, Bridge work, or later work is authorized by this review contract.