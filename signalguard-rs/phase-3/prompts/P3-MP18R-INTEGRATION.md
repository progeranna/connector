# P3-MP18R — Integration contract

Status: `P3_MP18R_INTEGRATION_AUTHORIZED`

## 1. Worker mode

Dedicated GitHub web integration worker.

Use only connected GitHub tools. Do not use a local checkout, shell, Codex CLI or an unconnected repository copy.

This contract authorizes PR creation, PR CI verification, a normal merge commit, exact read-back verification and connector control-plane publication for MP18R only.

## 2. Authority

Read completely before any write:

- `signalguard-rs/phase-3/prompts/P3-MP18R.md`
- `signalguard-rs/phase-3/prompts/P3-MP18R-DIAGNOSTIC.md`
- `signalguard-rs/phase-3/prompts/P3-MP18R-R1.md`
- `signalguard-rs/phase-3/reports/P3-MP18R-DIAGNOSTIC/ba31a348dc5055935c45f6be81073688caedd925.md`
- `signalguard-rs/phase-3/reports/P3-MP18R/664daebc9bc63a761ea8db205f9ae345f0d0c622.md`
- `signalguard-rs/phase-3/reports/P3-MP18R-REVIEW/664daebc9bc63a761ea8db205f9ae345f0d0c622.md`
- `signalguard-rs/phase-3/control/MICRO_PHASE_LEDGER.md`
- `signalguard-rs/phase-3/control/IMPLEMENTATION_SEQUENCE.md`
- `signalguard-rs/phase-3/control/STATUS.md`

The independent review status must be:

`P3_MP18R_IMPLEMENTATION_ACCEPTED_FOR_INTEGRATION`

## 3. Exact product identities

Product repository:

`progeranna/signalguard-rs`

Target branch:

`refactor/dashboard-modules`

Exact immutable target base:

`ba31a348dc5055935c45f6be81073688caedd925`

Expected target base tree:

`f629b6ea4339c92d03223c3bd8024cd4cb4571da`

Worker branch:

`p3/mp18r-exact-symbol-anomaly-detail`

Exact immutable worker commit:

`664daebc9bc63a761ea8db205f9ae345f0d0c622`

Expected worker tree:

`65c816c76a5f9e31858cdcb29acd523e8a92c122`

Worker commit message:

`fix(ui): open exact anomaly detail from symbol detail`

Stop with `P3_MP18R_INTEGRATION_BLOCKED_BY_IDENTITY_DRIFT` if either branch resolves differently, if the worker branch is not exactly one commit ahead and zero behind, or if the merge base is not the immutable target base.

## 4. Exact accepted diff

The compare from target base to worker head must contain exactly twelve modified paths and no additions, deletions or renames:

- `web/src/features/dashboard/SymbolDetailAnomalies.test.tsx`
- `web/src/features/dashboard/SymbolDetailAnomalies.tsx`
- `web/src/features/dashboard/SymbolDetailHeader.test.tsx`
- `web/src/features/dashboard/SymbolDetailHeader.tsx`
- `web/src/features/dashboard/SymbolDetailMetrics.test.tsx`
- `web/src/features/dashboard/SymbolDetailMetrics.tsx`
- `web/src/features/dashboard/symbolPopup.test.ts`
- `web/src/features/dashboard/symbolPopup.ts`
- `web/src/features/dashboard/symbolPopupResource.test.tsx`
- `web/src/pages/DashboardPage.popup.test.tsx`
- `web/src/pages/DashboardPage.test.tsx`
- `web/src/pages/DashboardPage.tsx`

Expected totals:

- additions: 496;
- deletions: 102;
- total worker commits: one.

Stop on any path or commit drift.

## 5. Binding invariants

Preserve exactly:

- `/` and `/dashboard` are the only visual console pages;
- `/symbols/:symbol` and `/anomalies` remain replacement redirects;
- market activation opens Symbol Detail modal;
- Symbol Detail anomaly activation opens exact UUID-keyed Anomaly Detail;
- All Anomalies rows never open Symbol Detail;
- modal state remains local and ephemeral;
- no URL-backed modal state or standalone detail page;
- strict SymbolPopup return contexts are `dashboard | symbols` only;
- Demo and Live remain isolated;
- public Replay remains forbidden;
- backend `/anomalies` remains unchanged;
- ticker ownership and bundle budgets remain unchanged.

The integration worker must not modify product code or worker history.

## 6. Pull request creation

Before creating the PR, search all open and closed PRs for the exact worker branch.

If an existing unmerged PR with exact base/head identities exists, reuse it only when its metadata and head are exact.

Otherwise create exactly one PR:

- base: `refactor/dashboard-modules`
- head: `p3/mp18r-exact-symbol-anomaly-detail`
- title: `fix(ui): open exact anomaly detail from symbol detail`
- draft: false

The body must record:

- target base SHA/tree;
- worker SHA/tree;
- corrected twelve-path lease;
- original, diagnostic and R1 contract identities;
- implementation and independent-review report paths;
- modal-only invariants;
- no product scope outside MP18R;
- required normal merge method.

Do not add unrelated labels, reviewers or comments.

## 7. PR identity and merge-ref verification

After PR creation, fetch and verify:

- PR base branch and base SHA are exact;
- PR head branch and head SHA are exact;
- PR is open and mergeable or becomes mergeable after GitHub computes the merge ref;
- no requested source change exists;
- synthetic PR merge commit/ref exists.

The synthetic merge ref must:

- have first parent `ba31a348dc5055935c45f6be81073688caedd925`;
- have second parent `664daebc9bc63a761ea8db205f9ae345f0d0c622`;
- have tree `65c816c76a5f9e31858cdcb29acd523e8a92c122`;
- contain exactly the accepted twelve-path effective diff from the target base.

Any conflict resolution or tree difference is a blocker. Do not edit the worker branch or target branch.

## 8. Required PR CI

Locate the workflow run associated with the exact synthetic merge-ref SHA.

Require both jobs:

- Rust;
- Frontend.

Both jobs must be `completed` with conclusion `success`.

Verify all available step summaries are successful, including:

### Rust

- checkout;
- formatting;
- generated API contract check;
- OpenAPI validation;
- cargo check;
- Clippy with warnings denied;
- tests;
- replay target;
- Docker Compose checks;
- shell syntax checks.

### Frontend

- checkout;
- dependency installation;
- tests;
- typecheck;
- lint;
- production build;
- bundle policy.

The checkout/log evidence must identify the exact synthetic merge-ref commit being tested.

Do not merge while any job is queued, in progress, cancelled, skipped or unsuccessful.

If CI fails, stop with `P3_MP18R_INTEGRATION_BLOCKED_BY_CI`. Do not rerun or modify product history unless a separate recovery contract is issued.

## 9. Merge operation

After exact PR identity and CI success, merge using GitHub normal merge method only:

- merge method: `merge`;
- expected head SHA: `664daebc9bc63a761ea8db205f9ae345f0d0c622`.

Do not squash or rebase.

Do not override the worker commit message or rewrite worker history.

Do not delete the worker branch during this contract unless the GitHub merge action performs no such deletion by default.

## 10. Post-merge verification

Fetch the final merge commit and target branch.

Require:

- target branch resolves to the final merge commit;
- final commit is a two-parent normal merge;
- ordered parent 1 is `ba31a348dc5055935c45f6be81073688caedd925`;
- ordered parent 2 is `664daebc9bc63a761ea8db205f9ae345f0d0c622`;
- final tree is `65c816c76a5f9e31858cdcb29acd523e8a92c122`;
- comparison from old base to final target is ahead by two, behind by zero;
- effective changed-path inventory remains exactly the accepted twelve files;
- PR is closed and merged;
- worker commit remains immutable.

The tested merge-ref tree and final merge tree must be identical. This tree identity is the binding remote validation even when the connector cannot enumerate a separate push-triggered final-SHA run.

## 11. Connector integration publication

After successful merge and read-back, publish exactly:

`signalguard-rs/phase-3/reports/P3-MP18R-INTEGRATION/<FINAL_MERGE_SHA>.md`

The report must include:

- every authority commit/blob;
- implementation and review report identities;
- exact target and worker identities;
- exact PR number/title/base/head;
- synthetic merge-ref SHA, parents and tree;
- CI run and job IDs;
- all CI job conclusions;
- final merge SHA, ordered parents and tree;
- final target-branch read-back;
- exact twelve-path effective diff;
- confirmation of no squash, rebase, amend or force-push;
- confirmation that MP20R has not begun;
- cleanup state and any retained worker branch.

Update:

`signalguard-rs/phase-3/control/STATUS.md`

The final state must be:

`P3_MP18R_INTEGRATED_MP20R_NOT_AUTHORIZED`

The status must record the final merge SHA/tree and identify the next allowed control-plane action as preparation and review of a separate P3-MP20R implementation contract from the integrated merge SHA.

Use the minimum sequential connector commits. Read back and verify both files, resulting blobs and connector commits.

Do not modify any other connector path.

## 12. Authorization boundary

This contract authorizes only MP18R integration.

It does not authorize:

- P3-MP20R implementation;
- Checkpoint 2R;
- semantic bridge;
- P3-MP21 through P3-MP30;
- dialog/accessibility work;
- routing/loading/performance work;
- responsive/final work;
- new product Phase 4.

## 13. Terminal result

Return exactly one:

- `P3_MP18R_INTEGRATION_COMPLETE`
- `P3_MP18R_INTEGRATION_BLOCKED_BY_IDENTITY_DRIFT`
- `P3_MP18R_INTEGRATION_BLOCKED_BY_PR_CONFLICT`
- `P3_MP18R_INTEGRATION_BLOCKED_BY_CI`
- `P3_MP18R_INTEGRATION_BLOCKED_BY_MERGE_VERIFICATION`
- `P3_MP18R_INTEGRATION_BLOCKED_BY_CONNECTOR_PUBLICATION`
