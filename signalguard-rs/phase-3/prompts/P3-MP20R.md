# P3-MP20R — Remove obsolete route presentation residue

Status: `P3_MP20R_IMPLEMENTATION_AUTHORIZED`

## 1. Worker mode

Dedicated local Codex implementation worker.

Use the `$rust-development` skill.

This is a narrow sequential refactor on the integrated MP18R base. It removes obsolete route/popup display variants without changing rendered values, interaction, resource ownership or product semantics.

## 2. Authority

Read completely before product mutation:

- `signalguard-rs/phase-3/control/EXECUTION_PLAN.md`
- `signalguard-rs/phase-3/control/RESUMPTION_PLAN.md`
- `signalguard-rs/phase-3/control/MICRO_PHASE_LEDGER.md`
- `signalguard-rs/phase-3/control/IMPLEMENTATION_SEQUENCE.md`
- `signalguard-rs/phase-3/control/STATUS.md`
- `signalguard-rs/phase-3/reports/P3-MP18R-INTEGRATION/6142ec7004b75cda077a49ab37bcfdca01f7f8e8.md`
- `signalguard-rs/phase-3/reports/P3-MP20R-PREFLIGHT/6142ec7004b75cda077a49ab37bcfdca01f7f8e8.md`

The MP20R preflight supersedes only the preliminary three-file writable lease in the recovered ledger. It does not change roadmap intent, ordering or any product-owner invariant.

## 3. Immutable product identity

Product repository:

`progeranna/signalguard-rs`

Local repository:

`/Users/anion/Desktop/work/git-signalguard-rs/signalguard-rs`

Target phase branch:

`refactor/dashboard-modules`

Exact immutable integrated base:

`6142ec7004b75cda077a49ab37bcfdca01f7f8e8`

Expected base tree:

`65c816c76a5f9e31858cdcb29acd523e8a92c122`

Assigned branch:

`p3/mp20r-route-presentation-residue`

Assigned worktree:

`/Users/anion/Desktop/work/git-signalguard-rs/worktrees/p3-mp20r`

Required single product commit:

`refactor(ui): remove obsolete route presentation residue`

Before creating the worktree or modifying product files, fetch the remote and verify that `origin/refactor/dashboard-modules` resolves exactly to the immutable base and expected tree.

Stop with `P3_MP20R_BLOCKED_BY_MP18R_OR_SCOPE_CONFLICT` without product mutation on any identity drift.

## 4. Exact product result

The integrated product is modal-only. No consumer requires route-specific anomaly display values.

Implement exactly:

1. Delete `MarketDisplayVariants` from `marketViewModel.ts`.
2. Change `MarketAnomalyViewModel.observed` from a route/popup object to one direct display string.
3. Change `MarketAnomalyViewModel.threshold` from a route/popup object to one direct display string.
4. Delete `formatRouteAnomalyValue` from `marketAdapters.ts`.
5. Delete `anomalyDisplayVariants` from `marketAdapters.ts`.
6. Rename the surviving type-aware formatter so its name is surface-neutral and does not refer to popup parity.
7. Map observed and threshold directly to that surviving formatter.
8. Update `SymbolDetailAnomalies.tsx` to render `anomaly.observed` and `anomaly.threshold` directly.
9. Update the two focused test files to the direct-string shape.
10. Preserve every visible formatted value exactly.

Required preserved formatting:

- `spread_spike` and `price_move`: three decimal percentage values, e.g. `2.500%`;
- `event_lag_spike`, `stale_data`, `quote_stuck`: milliseconds below 1000 and one-decimal seconds at or above 1000;
- `trade_burst`: integer plus ` /m`;
- `depth_sequence_gap`: integer plus ` gap` for observed and ` limit` for threshold;
- unknown types: generic number formatting with maximum three fractional digits;
- null or `NaN`: `—`.

Preserve unchanged:

- anomaly UUID, symbol, type, severity, detected, detectedAt, context and value class;
- anomaly input order;
- exact desktop click/Enter/Space activation;
- exact mobile activation;
- `data-anomaly-id` identity;
- modal controller, nested Back, focus restoration and stale mode/symbol behavior;
- Demo/Live isolation;
- all visible copy and markup structure.

Do not introduce a replacement `route`, `popup`, `surface`, `variant` or multi-surface wrapper under another name.

## 5. Corrected exact writable lease

Production/model:

- `web/src/features/dashboard/marketViewModel.ts`
- `web/src/features/dashboard/marketAdapters.ts`
- `web/src/features/dashboard/SymbolDetailAnomalies.tsx`

Tests:

- `web/src/features/dashboard/marketAdapters.test.ts`
- `web/src/features/dashboard/SymbolDetailAnomalies.test.tsx`

The final product diff may contain only these five exact paths.

The reopening of `SymbolDetailAnomalies.tsx` and its test is authorized only for the observed/threshold data-shape conversion. MP18R interaction code in those files remains immutable in behavior.

## 6. Explicitly forbidden paths and work

Do not modify, create, delete, format or regenerate any other product path.

Especially forbidden:

- `web/src/pages/DashboardPage.tsx` and every DashboardPage test;
- `SymbolDetailHeader.tsx` and `SymbolDetailMetrics.tsx`;
- `symbolPopup.ts`, `symbolPopupResource.ts` or resource/query files;
- routes and router tests;
- API schemas or backend code;
- shared components;
- CSS or responsive classes;
- status descriptors, tooltip copy or semantic Wave 4 work;
- ticker files;
- package files, lockfiles, scripts or bundle budgets;
- Rust files, migrations, OpenAPI artifacts or Docker configuration.

Do not begin Checkpoint 2R, semantic Bridge 01/02, P3-MP21 or any later phase.

## 7. Focused tests

From `web/`, run:

```bash
npm run test:run -- \
  src/features/dashboard/marketAdapters.test.ts \
  src/features/dashboard/SymbolDetailAnomalies.test.tsx
```

Focused assertions must prove:

- exact direct observed/threshold strings for every supported anomaly type;
- null values remain `—`;
- no route or popup variant remains;
- rendered Symbol Detail values remain byte-for-byte equivalent to the former popup values;
- UUID identity and desktop/mobile activation remain unchanged;
- input order and non-mutation remain unchanged;
- identity mismatch protections remain unchanged.

## 8. Full validation

From `web/`:

```bash
node --test scripts/check-bundle-size.test.mjs
npm run test:run
npm run typecheck
npm run lint
npm run build
npm run bundle:check
```

From repository root:

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
git diff --check
```

Do not weaken tests, scripts, budgets or configuration to obtain a pass.

## 9. Exact residual audit

Before commit, prove across the product tree that none of these active anomaly-display concepts remain:

- `MarketDisplayVariants`;
- `formatRouteAnomalyValue`;
- `anomalyDisplayVariants`;
- `formatPopupAnomalyValue`;
- `observed.route`;
- `threshold.route`;
- `observed.popup`;
- `threshold.popup`;
- fixtures using `{ route, popup }` for `MarketAnomalyViewModel`.

The words `route` and `popup` may still legitimately exist in unrelated routing, modal identity, filenames and MP18R concepts. Do not remove unrelated occurrences.

Also verify:

- exactly five changed paths;
- no untracked files;
- no dependency or generated artifact drift;
- one initial JS asset unless the existing build topology independently changes without code outside the lease;
- all unchanged bundle limits pass;
- output values in focused tests match the accepted integrated base presentation.

## 10. Browser evidence

No browser screenshot is required because MP20R is a pure presentation-neutral data-shape refactor and Checkpoint 2R immediately follows integration.

Do not claim visual redesign or semantic changes.

## 11. Delivery

After every required gate passes:

1. Create exactly one product commit:
   `refactor(ui): remove obsolete route presentation residue`
2. Verify its exact parent is:
   `6142ec7004b75cda077a49ab37bcfdca01f7f8e8`
3. Verify exactly one commit ahead and zero behind.
4. Push only:
   `p3/mp20r-route-presentation-residue`
5. Do not open a PR.
6. Do not merge.
7. Do not amend, rebase, squash, force-push or tag.
8. Publish the connector implementation report at:
   `signalguard-rs/phase-3/reports/P3-MP20R/<PRODUCT_COMMIT_SHA>.md`
9. Connector report commit message:
   `docs(phase-3): publish MP20R implementation report`
10. Record the preflight correction, exact five-file diff, all gates and residual audit.
11. Read back and verify the product branch, product commit, connector report, report blob and connector commit.

## 12. Terminal result

Return exactly one:

- `P3_MP20R_COMPLETE`
- `P3_MP20R_BLOCKED_BY_MP18R_OR_SCOPE_CONFLICT`

Return success only after the product branch and connector report are both published and independently read back.
