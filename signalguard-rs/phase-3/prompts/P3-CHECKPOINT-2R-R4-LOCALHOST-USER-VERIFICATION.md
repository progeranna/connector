# P3-CHECKPOINT-2R-R4 — Localhost product-owner verification

Status: `P3_CHECKPOINT_2R_R4_LOCALHOST_USER_VERIFICATION_AUTHORIZED`

## Worker mode

Dedicated local Codex localhost-handoff worker.

Use the local authenticated checkout, shell, Docker, and a real local browser as needed.

Use `$rust-development` for repository correctness and identity checks.

This is a **read-only integrated-product verification and handoff**. Product write lease: `NONE`.

Do not modify tracked product or test files. Do not create a product branch, commit, push, PR, merge, dependency change, lockfile change, generated contract change, test edit, or defect fix.

Do not update connector control files. Do not authorize the full Checkpoint 2R rerun.

The purpose of this worker is to prove the exact integrated merge is what is running locally, start a stable localhost preview backed by real repository services/data, perform a narrow readiness smoke, and hand the running URL to the product owner for manual verification.

The worker must not claim product-owner acceptance. Only the user/orchestrator can accept this step after manually inspecting the running localhost UI.

## Required connector authority

Before local work, fetch and read completely from `progeranna/connector`:

- `signalguard-rs/phase-3/control/CURRENT_EXECUTION.md`
- `signalguard-rs/phase-3/control/STATUS.md`
- `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-R4-INTEGRATION.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R4-INTEGRATION/23656c9b93a24bfc20ba8f417275564bb5b5d240.md`

Required current state:

`P3_CHECKPOINT_2R_R4_LOCALHOST_USER_VERIFICATION_AUTHORIZED`

The integration report authority is:

- publication commit: `f2189063dba447bd0dca4a83ee16120e4f31959e`
- report blob: `6a2a94ed57e01635d8fdaa4809170400bb572c65`
- integration status: `P3_CHECKPOINT_2R_R4_INTEGRATION_COMPLETE`

## Exact integrated product identity

Product repository:

`progeranna/signalguard-rs`

Target branch:

`refactor/dashboard-modules`

Exact integrated merge commit:

`23656c9b93a24bfc20ba8f417275564bb5b5d240`

Expected integrated tree:

`d8c0289a05b3646b3abc7056bd269b927e61d5c4`

Expected ordered parents:

1. `7dab5647d322339f5bd9d0514e5178522d5181c0`
2. `79abb161e7a731df7077d49b44481eaaf25bf762`

Before launching anything, fetch the authenticated product remote and prove:

- `origin/refactor/dashboard-modules` resolves exactly to `23656c9b93a24bfc20ba8f417275564bb5b5d240`;
- its tree is exactly `d8c0289a05b3646b3abc7056bd269b927e61d5c4`;
- the merge has the exact ordered parents above;
- there is no target drift.

Any identity mismatch is a hard blocker. Do not adapt to a newer commit.

## Clean local execution boundary

Use a new clean detached worktree at the exact integrated merge commit.

Do not reuse the R4 implementation worktree, prior Checkpoint worktrees, or any existing manual-QA worktree.

Keep all generated validation/handoff artifacts outside both repositories, preferably under a deterministic `/tmp/p3-checkpoint2r-r4-localhost-<date-time>` directory.

Before launch, record:

- exact `HEAD` SHA;
- exact tree SHA;
- detached-head state;
- `git status --porcelain` empty;
- `git diff --check` pass.

The worktree must remain clean while the localhost is running.

## Local service topology

Start an isolated local environment from the exact detached integrated commit.

Use repository-supported PostgreSQL, Redis, backend, frontend build/preview and replay/live mechanisms without tracked changes.

Choose free isolated local ports so existing user services are not disturbed. Record the exact chosen ports.

Requirements:

- PostgreSQL and Redis must be isolated from unrelated local project instances;
- backend must run from the exact integrated commit;
- frontend must be built from the exact integrated commit;
- serve a production-style preview, not an edited dev tree;
- the browser-facing localhost origin must be stable and reachable by the user;
- API routing may use an ordinary pass-through local reverse proxy created outside the repository if needed;
- do not mock/intercept/fabricate frontend API resources, selected-symbol storage, mode state, popup resources, market/anomaly data, navigation, favicon behavior, or runtime errors;
- Demo must use real deterministic Demo behavior from the product;
- Live must remain source `live` and must not silently fall back to Demo;
- no browser extension or request interception may hide console/network failures.

The preview must remain running after the worker returns `READY` so the user can open it manually.

Do not stop the preview/services on successful handoff. Stop them only if the setup is blocked or when the user later asks the local worker to tear them down.

## Narrow readiness validation before handoff

This is not the full Checkpoint 2R rerun. Do not execute the full checkpoint matrix here.

Before handing the URL to the user, perform only enough automated/local validation to prove the integrated localhost is usable for manual product-owner inspection:

1. Build the frontend production bundle from the exact integrated commit.
2. Start the isolated backend/services and production preview.
3. Load `/dashboard` in a fresh real-browser context.
4. Prove the app renders real data and the browser can reach the real backend APIs.
5. Prove Demo mode is usable.
6. Prove Live mode is usable and visibly remains Live data/source rather than Demo fallback.
7. Perform the exact narrow R4 ownership smoke once on desktop:
   - establish Demo selected symbol `BTCUSDT`;
   - switch to Live while Symbol Detail/nested symbol-owned anomaly state is open;
   - establish Live selected symbol `ETHUSDT`;
   - open an exact Live ETH anomaly if available through the real UI/data;
   - return to Demo;
   - verify the nested Live UUID/detail is gone;
   - verify the still-open parent Symbol Detail is owned by Demo `BTCUSDT`, not stale `ETHUSDT`;
   - verify `returnContext` remains the originating symbols/All Markets context;
   - verify no hard reload is used to achieve the transition.
8. Verify there are zero unexpected console errors, page errors and unhandled promise rejections during this narrow smoke.
9. Record request failures. Do **not** blanket-ignore every `net::ERR_ABORTED`. If an aborted request occurs, record its concrete URL/resource type and explain why it is an expected stale-query cancellation. Any unexplained aborted asset/navigation/critical API request is a blocker for the handoff.
10. Verify `/favicon.ico` request count remains zero in the fresh context.

If the narrow smoke exposes a deterministic product failure, do not fix it. Capture the exact reproduction, keep product code untouched, stop success claims, and return the blocker marker.

## Product-owner handoff

On successful readiness, return a concise handoff containing:

- exact integrated commit and tree being served;
- exact localhost URL the user should open;
- exact backend/preview/proxy ports;
- confirmation that the detached worktree is clean;
- confirmation that the narrow R4 readiness smoke passed;
- any concrete expected aborted-query URLs observed, or state that none occurred;
- a short manual checklist for the user;
- the READY terminal marker.

### Manual checklist to give the user

The user should personally verify at minimum:

1. Open the supplied localhost `/dashboard` URL.
2. Confirm the page looks normal and is the expected current SignalGuard dashboard.
3. In Demo, use `BTCUSDT` and open the All Markets / Symbol Detail flow.
4. Open a visible anomaly detail from that symbol if available.
5. Switch to Live and confirm Live is visibly active and the UI remains responsive.
6. In Live, switch the selected symbol to `ETHUSDT` through the real UI and open its Symbol Detail; open an ETH anomaly detail if available.
7. Switch back to Demo while the symbol modal/nested detail flow is active.
8. Confirm the nested Live ETH anomaly disappears and the parent modal now shows **BTCUSDT**, matching the Demo header/selection — it must not remain ETHUSDT.
9. Confirm Back/Close still returns to the expected All Markets/symbol context rather than losing the modal context.
10. Look for stale ETHUSDT content after returning to Demo; none should remain in the open BTCUSDT modal.
11. Confirm there is no visible hard page reload, broken layout, blank state, unexpected error toast, or obvious console/runtime failure.
12. Optionally resize/use a narrow mobile-width browser window and repeat the final Live ETH → Demo BTC transition to visually confirm the same behavior.

The user may report either:

- **ACCEPTED** — behavior and UI look correct; or
- **BLOCKED** — with the exact visible problem/reproduction.

The worker must not infer acceptance from silence.

## Success and blocker markers

If the exact integrated localhost is running, the narrow readiness smoke passes, and the URL is ready for user inspection, return exactly:

`P3_CHECKPOINT_2R_R4_LOCALHOST_READY_FOR_USER`

If identity, startup, real-data readiness, narrow R4 smoke, console/runtime behavior, or cleanliness is blocked, return exactly:

`P3_CHECKPOINT_2R_R4_LOCALHOST_VERIFICATION_BLOCKED`

## Continuation boundary

This contract does not authorize:

- product modification or defect repair;
- any product branch/commit/push/PR/merge;
- connector control/status updates by the local worker;
- the full Checkpoint 2R rerun;
- independent checkpoint acceptance;
- `P3-W4-BRIDGE01`;
- `P3-W4-BRIDGE02`;
- P3-MP21…P3-MP30 / semantic Wave 4;
- dialogs/accessibility, routing/loading/performance, responsive/final, Phase 4, or later work.

After the worker returns `P3_CHECKPOINT_2R_R4_LOCALHOST_READY_FOR_USER`, the user must manually inspect the running URL and report acceptance or a blocker to the orchestrator. Only the orchestrator may then publish the next control transition.