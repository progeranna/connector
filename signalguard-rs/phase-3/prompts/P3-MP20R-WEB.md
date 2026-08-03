# P3-MP20R-WEB — Remove obsolete route presentation residue

Status: `P3_MP20R_WEB_IMPLEMENTATION_AUTHORIZED`

## 1. Execution mode correction

This contract supersedes the worker-mode requirements of:

`signalguard-rs/phase-3/prompts/P3-MP20R.md`

The earlier contract incorrectly required a local Codex checkout, local worktree and shell validation. The user executed a GitHub web worker, so `P3_MP20R_BLOCKED_BY_MP18R_OR_SCOPE_CONFLICT` was an execution-mode mismatch, not a product identity or lease conflict.

This replacement contract authorizes a GitHub web implementation worker using only connected GitHub tools.

The product objective, exact five-file lease, immutable base and required product commit message remain unchanged.

## 2. Tool restrictions

Use only connected GitHub tools.

Do not use:

- local checkout;
- shell;
- Codex CLI;
- GitHub CLI;
- filesystem repository copy;
- unconnected repository data.

Do not claim local test, browser or screenshot execution.

## 3. Authority

Read completely before writing:

- `signalguard-rs/phase-3/control/EXECUTION_PLAN.md`
- `signalguard-rs/phase-3/control/RESUMPTION_PLAN.md`
- `signalguard-rs/phase-3/control/MICRO_PHASE_LEDGER.md`
- `signalguard-rs/phase-3/control/IMPLEMENTATION_SEQUENCE.md`
- `signalguard-rs/phase-3/control/STATUS.md`
- `signalguard-rs/phase-3/reports/P3-MP18R-INTEGRATION/6142ec7004b75cda077a49ab37bcfdca01f7f8e8.md`
- `signalguard-rs/phase-3/reports/P3-MP20R-PREFLIGHT/6142ec7004b75cda077a49ab37bcfdca01f7f8e8.md`
- `signalguard-rs/phase-3/prompts/P3-MP20R.md`

This contract supersedes only the execution mode and validation mechanism of the previous MP20R contract. It does not broaden product scope.

## 4. Immutable product identity

Product repository:

`progeranna/signalguard-rs`

Target branch:

`refactor/dashboard-modules`

Exact immutable base:

`6142ec7004b75cda077a49ab37bcfdca01f7f8e8`

Expected base tree:

`65c816c76a5f9e31858cdcb29acd523e8a92c122`

Assigned branch:

`p3/mp20r-route-presentation-residue`

Required single product commit:

`refactor(ui): remove obsolete route presentation residue`

Before any write, verify that the target branch still resolves exactly to the immutable base and tree and that the assigned branch does not already exist.

Stop on drift.

## 5. Exact writable lease

Production/model:

1. `web/src/features/dashboard/marketViewModel.ts`
2. `web/src/features/dashboard/marketAdapters.ts`
3. `web/src/features/dashboard/SymbolDetailAnomalies.tsx`

Tests:

4. `web/src/features/dashboard/marketAdapters.test.ts`
5. `web/src/features/dashboard/SymbolDetailAnomalies.test.tsx`

The final commit tree may differ from the immutable base only in these five exact paths.

No other product path may be modified, created, deleted, reformatted or regenerated.

## 6. Exact product result

Implement exactly:

1. Delete `MarketDisplayVariants`.
2. Change `MarketAnomalyViewModel.observed` to one direct display string.
3. Change `MarketAnomalyViewModel.threshold` to one direct display string.
4. Delete `formatRouteAnomalyValue`.
5. Delete `anomalyDisplayVariants`.
6. Rename the surviving type-aware formatter so its name is surface-neutral and does not include `Popup`.
7. Map observed and threshold directly to that formatter.
8. Change `SymbolDetailAnomalies.tsx` to render direct strings.
9. Convert the two focused test files to the direct-string shape.
10. Preserve every rendered value exactly.

Required preserved formatting:

- `spread_spike` and `price_move`: three-decimal percentage, e.g. `2.500%`;
- `event_lag_spike`, `stale_data`, `quote_stuck`: milliseconds below 1000 and one-decimal seconds at or above 1000;
- `trade_burst`: integer plus ` /m`;
- `depth_sequence_gap`: integer plus ` gap` for observed and ` limit` for threshold;
- unknown types: generic number formatting with at most three fractional digits;
- null or `NaN`: `—`.

Preserve unchanged:

- UUID, symbol, type, severity, detected, detectedAt, context and value class;
- anomaly order;
- desktop click/Enter/Space activation;
- mobile activation;
- `data-anomaly-id`;
- modal controller, Back, focus restoration and stale mode/symbol behavior;
- Demo/Live isolation;
- visible copy, markup structure, styling and responsive classes.

Do not introduce a replacement route/popup/surface/variant wrapper under another name.

## 7. Atomic GitHub implementation

The worker must create exactly one product commit using GitHub Git Data operations:

1. Fetch all five files at the immutable base.
2. Construct complete replacement contents in memory.
3. Create one blob for each changed file.
4. Create one tree based on base tree `65c816c76a5f9e31858cdcb29acd523e8a92c122`, replacing only the five leased paths.
5. Create exactly one commit with parent `6142ec7004b75cda077a49ab37bcfdca01f7f8e8` and message:
   `refactor(ui): remove obsolete route presentation residue`
6. Create or move only branch `p3/mp20r-route-presentation-residue` to that commit without force.

Do not use the contents API sequentially on the product branch because that would create multiple product commits.

Do not modify the target branch.

## 8. Static verification before branch publication

Before creating the product commit, inspect the complete proposed contents and verify:

- TypeScript syntax is valid by inspection;
- all imports remain valid;
- no leased component prop or callback changes;
- all test fixtures match the direct-string type;
- every former popup-visible value remains exactly preserved;
- no non-leased file is needed.

Residual audit of proposed contents must show no active occurrence of:

- `MarketDisplayVariants`;
- `formatRouteAnomalyValue`;
- `anomalyDisplayVariants`;
- `formatPopupAnomalyValue`;
- `observed.route`;
- `threshold.route`;
- `observed.popup`;
- `threshold.popup`;
- `{ route, popup }` fixtures for `MarketAnomalyViewModel`.

The words `route` and `popup` may remain in unrelated repository concepts.

## 9. Branch and diff verification

After publication verify:

- branch head is the exact created commit;
- commit parent is exactly the immutable base;
- commit message is exact;
- branch is one commit ahead and zero behind;
- comparison contains exactly five modified files;
- no added, deleted or renamed path;
- no target-branch mutation;
- no existing or newly opened PR;
- no merge occurred.

## 10. Validation boundary

Because this is a GitHub web implementation worker, it does not execute local shell gates.

Do not report local Vitest, typecheck, lint, build, Cargo, Docker or browser results.

Those gates will run against the exact synthetic merge ref in the later dedicated integration worker before merge.

The implementation report must explicitly state:

`LOCAL_GATES_NOT_RUN_WEB_WORKER_PR_CI_REQUIRED_BEFORE_MERGE`

## 11. Connector report

Publish:

`signalguard-rs/phase-3/reports/P3-MP20R/<PRODUCT_COMMIT_SHA>.md`

Connector commit message:

`docs(phase-3): publish MP20R web implementation report`

Record:

- execution-mode correction;
- immutable base/tree;
- product commit/tree;
- exact parent and message;
- exact five-path diff;
- complete static residual audit;
- branch read-back;
- absence of PR/merge;
- the required validation-boundary marker;
- confirmation that Checkpoint 2R and later phases did not begin.

Read back and verify report path, report blob and connector commit.

## 12. Prohibitions

Do not:

- modify the target branch;
- open a PR;
- merge;
- modify any sixth product path;
- alter API, resources, controller, focus, routes, CSS, descriptors, ticker, packages, lockfiles, backend or budgets;
- begin Checkpoint 2R, semantic bridge, Wave 4 or later work;
- claim tests that were not executed.

## 13. Terminal result

Return exactly one:

- `P3_MP20R_WEB_COMPLETE`
- `P3_MP20R_WEB_BLOCKED_BY_IDENTITY_OR_SCOPE`

Return success only after the single product commit, assigned branch and connector report are published and read back.
