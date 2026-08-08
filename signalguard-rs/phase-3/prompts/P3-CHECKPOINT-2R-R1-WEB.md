# P3-CHECKPOINT-2R-R1-WEB — Restore modal entry-point reachability

Status: `P3_CHECKPOINT_2R_R1_WEB_IMPLEMENTATION_AUTHORIZED`

## Mode

Dedicated GitHub web implementation worker.

Use only connected GitHub tools. Do not use a local checkout, shell, Codex CLI, GitHub CLI or an unconnected repository copy.

## Authority

Read completely:

- `signalguard-rs/phase-3/control/CURRENT_EXECUTION.md`
- `signalguard-rs/phase-3/control/STATUS.md`
- `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-LOCAL.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-BLOCKER/8bbef01d7d9979c4996954171a0e7c3748f02538.md`

The blocker report is accepted as the sole basis for this recovery lease.

## Exact product identity

Repository: `progeranna/signalguard-rs`

Target branch: `refactor/dashboard-modules`

Immutable base commit:

`8bbef01d7d9979c4996954171a0e7c3748f02538`

Expected base tree:

`d8f9e71e7aec5fcf7b472011a68247a6df42bbac`

Assigned worker branch already exists and must still point exactly to the immutable base before any write:

`p3/checkpoint2r-view-all-reachability`

Required single product commit message:

`fix(ui): keep dashboard modal entry points reachable`

Stop before product mutation on any identity drift.

## Exact blocker

Checkpoint 2R command and CI gates passed, but browser validation was blocked because the accepted deterministic Demo response contains exactly 7 markets and 3 recent anomalies while both Dashboard `View all` actions render only when `preview.hasMore` is true.

This makes the required All Markets and All Anomalies modal flows unreachable despite the modal implementations being present.

This is a reachability defect only. Do not alter modal identity, routing, data resources, semantic vocabulary, styling or preview limits.

## Exact writable lease

Production:

- `web/src/pages/DashboardPage.tsx`

Tests:

- `web/src/pages/DashboardPage.test.tsx`
- `web/src/pages/DashboardPage.popup.test.tsx`

No fourth product path may be modified, created, deleted, formatted or regenerated.

## Required product result

1. Market Health `View all` is rendered whenever the Market Health collection is non-empty, including counts below and exactly equal to the preview limit.
2. Recent Anomalies `View all` is rendered whenever the Recent Anomalies collection is non-empty, including counts below and exactly equal to the preview limit.
3. Neither `View all` control is rendered for its corresponding empty collection.
4. Preview row counts, preview models and preview limits remain unchanged.
5. `preview.hasMore` semantics remain available to the preview models; this recovery changes only action reachability in the Dashboard caller.
6. `View all` copy, button styling and section placement remain unchanged.
7. All Markets continues to open the existing All Markets modal.
8. All Anomalies continues to open the existing All Anomalies modal.
9. Existing exact UUID, Back, focus, Demo/Live, symbol-selection and modal-close behavior remains unchanged.
10. No route navigation or URL-backed modal state is introduced.

The intended caller condition is collection non-emptiness, not `hasMore`. Do not satisfy the requirement by changing preview limits or fabricating extra Demo records.

## Required tests

Update the leased tests so they prove both sections independently across:

- empty collection: no corresponding `View all`;
- count below preview limit: corresponding `View all` exists;
- count exactly equal to preview limit: corresponding `View all` exists;
- count above preview limit: corresponding `View all` exists and existing full-list modal behavior remains intact.

Preserve existing modal-flow tests in `DashboardPage.popup.test.tsx` and add or adjust only the minimum assertions needed to prove real-Demo-count reachability for:

- 7 markets;
- 3 recent anomalies.

Remove stale source-contract assertions that require `preview.hasMore` to own the Dashboard action decision. Do not weaken unrelated assertions.

## Forbidden adjacent work

Do not modify:

- preview model files or constants;
- any API, schema, DTO, fixture or Demo data source;
- Symbol Detail, Anomaly Detail or modal controller logic except through the existing callbacks already present in `DashboardPage.tsx`;
- routes/router;
- CSS;
- status descriptors or Tooltip;
- ticker;
- package manifests, lockfiles or bundle budgets;
- backend/Rust/OpenAPI/migrations;
- semantic Bridge 01/02 or any Wave 4 implementation.

## Web-worker validation boundary

Perform static code review and exact diff validation through GitHub.

Do not claim to have run local Vitest, typecheck, lint, build, Cargo, Docker or browser validation.

Those gates must run later on the exact PR synthetic merge ref before integration, followed by a rerun of local Checkpoint 2R after integration.

The implementation report must contain:

`LOCAL_GATES_NOT_RUN_WEB_WORKER_PR_CI_AND_CHECKPOINT_RERUN_REQUIRED`

## Atomic delivery

Produce exactly one product commit whose sole parent is the immutable base and whose diff contains exactly the three leased files.

Move only `p3/checkpoint2r-view-all-reachability` to that commit. Do not modify `refactor/dashboard-modules`.

Do not open a PR and do not merge.

Publish connector report:

`signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R1/<PRODUCT_COMMIT_SHA>.md`

Connector commit message:

`docs(phase-3): publish Checkpoint 2R R1 implementation report`

The report must record:

- immutable base SHA/tree;
- worker commit SHA/tree and exact sole parent;
- exact three-file diff;
- static behavior evidence;
- test changes for empty/below/equal/above limit;
- no fourth product path;
- target branch unchanged;
- no PR or merge;
- validation-boundary marker;
- confirmation that Bridge 01/02 and Wave 4 did not begin.

Read back and verify the worker branch and connector report.

## Terminal result

Return:

`P3_CHECKPOINT_2R_R1_WEB_COMPLETE`

only after exact product commit, branch update and connector report publication are verified.

Return:

`P3_CHECKPOINT_2R_R1_WEB_BLOCKED_BY_IDENTITY_OR_SCOPE`

on identity drift, any fourth required path or inability to satisfy the exact recovery result.
