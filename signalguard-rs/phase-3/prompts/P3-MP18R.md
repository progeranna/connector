# P3-MP18R — Exact anomaly detail from Symbol Detail

Status: `P3_MP18R_IMPLEMENTATION_AUTHORIZED`

## 1. Worker mode

Dedicated local Codex implementation worker.

Use the `$rust-development` skill.

This task requires a full local checkout, complete frontend validation, deterministic browser validation and screenshot capture. It is not a GitHub-web-only task.

Do not use an unverified repository copy. Do not modify connector control files except for the exact implementation report after the product commit is final and verified.

## 2. Authority

Read completely before changing product code:

- `signalguard-rs/phase-3/control/EXECUTION_PLAN.md`
- `signalguard-rs/phase-3/control/RESUMPTION_PLAN.md`
- `signalguard-rs/phase-3/control/MICRO_PHASE_LEDGER.md`
- `signalguard-rs/phase-3/control/IMPLEMENTATION_SEQUENCE.md`
- `signalguard-rs/phase-3/control/STATUS.md`
- `signalguard-rs/phase-3/reports/P3-RECOVERY-INVENTORIES/ba31a348dc5055935c45f6be81073688caedd925.md`

This contract is the immutable implementation authority for MP18R. Older route/page requirements are superseded by the modal-only product-owner decisions in `RESUMPTION_PLAN.md`.

## 3. Exact product identity

Product repository:

`progeranna/signalguard-rs`

Local repository root:

`/Users/anion/Desktop/work/git-signalguard-rs/signalguard-rs`

Phase branch:

`refactor/dashboard-modules`

Immutable product base:

`ba31a348dc5055935c45f6be81073688caedd925`

Expected base tree:

`f629b6ea4339c92d03223c3bd8024cd4cb4571da`

Assigned branch:

`p3/mp18r-exact-symbol-anomaly-detail`

Required worktree:

`/Users/anion/Desktop/work/git-signalguard-rs/worktrees/p3-mp18r`

Required single product commit:

`fix(ui): open exact anomaly detail from symbol detail`

Stop with `P3_MP18R_BLOCKED_BY_SCOPE_OR_IDENTITY` if the remote phase branch or local base is not exactly the immutable SHA/tree.

## 4. Binding modal-only invariants

- `/` and `/dashboard` are the only visual console pages.
- `/symbols/:symbol` and `/anomalies` remain replacement redirects to `/dashboard`.
- Market activation opens Symbol Detail modal.
- Anomaly activation opens Anomaly Detail by exact UUID.
- All Anomalies rows never open Symbol Detail.
- Modal state remains ephemeral local state.
- URL-synchronised modal state, modal deep links and standalone detail pages are forbidden.
- Demo and Live remain strictly isolated.
- Public Replay is forbidden.
- Backend `/anomalies` remains unchanged.
- Ticker ownership and behavior are protected.
- Bundle budgets remain unchanged.

## 5. Exact writable lease

### Production

- `web/src/pages/DashboardPage.tsx`
- `web/src/features/dashboard/SymbolDetailAnomalies.tsx`
- `web/src/features/dashboard/SymbolDetailHeader.tsx`
- `web/src/features/dashboard/SymbolDetailMetrics.tsx`
- `web/src/features/dashboard/symbolPopup.ts`

### Tests

- `web/src/pages/DashboardPage.popup.test.tsx`
- `web/src/features/dashboard/SymbolDetailAnomalies.test.tsx`
- `web/src/features/dashboard/SymbolDetailHeader.test.tsx`
- `web/src/features/dashboard/SymbolDetailMetrics.test.tsx`
- `web/src/features/dashboard/symbolPopup.test.ts`

No other product path may be modified, created, deleted, formatted or regenerated.

## 6. Forbidden adjacent paths

Explicitly forbidden:

- `web/src/features/dashboard/marketViewModel.ts`
- `web/src/features/dashboard/marketAdapters.ts`
- router and route files
- API clients and query-key files
- Zod schemas and generated API contracts
- `symbolMarketResource.ts`
- `symbolPopupResource.ts`
- selected-symbol or mode storage ownership
- shared Dialog extraction or architecture
- Wave 4 vocabulary, indicators or tooltip work
- global CSS
- `web/src/app/GlobalMarketTicker.tsx`
- `.sg-ticker-track` and ticker keyframes
- package manifests and lockfiles
- bundle budgets
- backend, Rust, migration or database paths

Do not perform opportunistic cleanup outside the exact lease.

## 7. Required controller identity

Anomaly Detail opened from Symbol Detail must retain only:

- exact anomaly UUID;
- parent `SymbolPopupIdentity`.

Do not store:

- a full `DashboardAnomaly` object;
- a `MarketAnomalyViewModel` object;
- a Dashboard-summary copy;
- route or URL modal state.

The exact anomaly must be resolved from the current active parent Symbol Detail resource:

`resource.anomalies.find(anomaly => anomaly.id === anomalyId)`

Never substitute by symbol, list index, position or a same-symbol anomaly from Dashboard summary.

## 8. Required product behavior

### Symbol Detail anomaly activation

1. Desktop anomaly rows become keyboard- and pointer-activatable.
2. Mobile anomaly cards open Anomaly Detail rather than Symbol Detail.
3. Both pass exact anomaly UUID.
4. Accessible names describe opening anomaly detail and include enough identity to distinguish same-symbol anomalies.
5. Desktop activation supports click, Enter and Space.
6. Both responsive variants carry exact `data-anomaly-id` ownership for focus restoration.

### Anomaly Detail resolution

1. Resolve exact UUID from the active Symbol Detail mode/symbol resource.
2. Assert parent identity remains exact.
3. Display only the selected anomaly.
4. Two anomalies with the same symbol but different UUIDs remain distinguishable.
5. No Dashboard-summary fallback is permitted for a symbol-resource-owned detail.

### Back and close semantics

1. Back from symbol-owned Anomaly Detail restores the same Symbol Detail identity.
2. Back restores focus to the exact visible originating row/card.
3. Close, Escape and backdrop close the complete active workflow and return focus according to the existing external-trigger behavior.
4. Do not reinterpret Close/Escape/backdrop as Back.
5. Preserve All Anomalies → Anomaly Detail → Back behavior.

### Responsive focus restoration

Both desktop and mobile variants can exist in the DOM with the same data identity.

Initial-focus resolution must select the visible matching element rather than a hidden responsive duplicate.

Use a deterministic fallback for jsdom/non-layout test environments without weakening real-browser visibility selection.

Do not implement the future shared Dialog primitive in this task.

### Mode and symbol replacement

1. Mode replacement while Symbol Detail is open replaces the parent identity and clears incompatible nested anomaly UUID state.
2. Symbol replacement clears incompatible nested anomaly UUID state.
3. Old mode/symbol content must disappear immediately.
4. Late old-resource responses must not render into the new identity.
5. Never carry an old UUID into another mode or symbol.

### Lease-owned cleanup

Remove:

- unreachable `SymbolPopupReturnContext` value `"anomalies"`;
- obsolete anomaly-to-symbol callback from `SymbolDetailAnomalies`;
- ignored single-literal `variant="popup"` prop from `SymbolDetailHeader` and `SymbolDetailAnomalies` where present;
- ignored single-literal `surface="popup"` prop from `SymbolDetailMetrics` where present;
- their exact leased tests and call sites.

Retain valid return contexts:

- `dashboard`;
- `symbols`.

Do not remove route/popup formatting from market view models; that is reserved for MP20R.

## 9. Required focused tests

Add or update tests proving:

1. desktop exact UUID click activation;
2. desktop Enter activation;
3. desktop Space activation;
4. mobile exact UUID activation;
5. no Symbol Detail anomaly activation invokes Symbol Detail;
6. same-symbol/different-UUID selection opens only the selected anomaly;
7. symbol-resource anomaly can open even when absent from `summary.recent_anomalies`;
8. no same-symbol Dashboard-summary substitution;
9. Back restores exact parent mode/symbol/return context;
10. Back restores exact visible desktop row at desktop layout;
11. Back restores exact visible mobile card at mobile layout;
12. hidden responsive duplicate is rejected;
13. mode replacement clears old UUID and old content;
14. symbol replacement clears old UUID and old content;
15. late old-resource results do not replace active content;
16. only `dashboard` and `symbols` SymbolPopup return contexts remain;
17. ignored popup-only props and their call sites are removed;
18. existing Dashboard, All Markets and All Anomalies flows remain intact;
19. existing Escape, backdrop, Close, focus containment and body-lock behavior remains green.

Use adapter-derived fixtures where possible so these tests do not depend on the route/popup formatting shape reserved for MP20R cleanup.

## 10. Local setup and identity verification

Before creating or changing the assigned worktree:

```bash
cd /Users/anion/Desktop/work/git-signalguard-rs/signalguard-rs

git fetch origin --prune

git rev-parse origin/refactor/dashboard-modules
git show -s --format=%T origin/refactor/dashboard-modules
```

Require exact output:

```text
ba31a348dc5055935c45f6be81073688caedd925
f629b6ea4339c92d03223c3bd8024cd4cb4571da
```

Create the assigned branch/worktree exactly from the immutable base. Do not reuse an unrelated worktree.

Before implementation verify:

```bash
git rev-parse HEAD
git show -s --format=%T HEAD
git status --short
git rev-list --count ba31a348dc5055935c45f6be81073688caedd925..HEAD
git rev-list --count HEAD..ba31a348dc5055935c45f6be81073688caedd925
```

Required initial state:

- exact HEAD and tree;
- clean worktree;
- ahead/behind `0 / 0`.

## 11. Focused validation

From `web/` run:

```bash
npm ci
npm run test:run -- \
  src/pages/DashboardPage.popup.test.tsx \
  src/features/dashboard/SymbolDetailAnomalies.test.tsx \
  src/features/dashboard/SymbolDetailHeader.test.tsx \
  src/features/dashboard/SymbolDetailMetrics.test.tsx \
  src/features/dashboard/symbolPopup.test.ts
```

If the script does not forward file arguments, invoke the existing Vitest binary with the repository's protected thread settings. Do not modify `package.json`.

Then run:

```bash
node --test scripts/check-bundle-size.test.mjs
npm run test:run
npm run typecheck
npm run lint
npm run build
npm run bundle:check
```

## 12. Repository validation

From the repository root run unchanged global gates:

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

No backend output change is expected. Any generated or product diff outside the lease is a blocker.

## 13. Bundle constraints

Do not raise or weaken budgets.

Current accepted baseline:

- initial raw JS: `387239` bytes;
- direct gzip: `110799` bytes;
- one initial JS asset;
- zero async JS assets.

Budgets remain:

- initial: `409600`;
- largest: `409600`;
- total: `414720`.

Require no new dependency, package drift, duplicate emitted module IDs or unexpected asset-topology change.

## 14. Browser validation

Use a deterministic production preview with mocked APIs on ports that do not conflict with the existing manual-QA environment.

Do not stop or modify services using:

- `5173`;
- `8080`;
- `5432`;
- `6379`.

Validate at:

- desktop `1440×900`;
- mobile width `390` with stable height near `844`.

Cover:

- Demo and Live;
- BTCUSDT and ETHUSDT;
- Dashboard → Symbol Detail → exact Anomaly Detail → Back;
- All Markets → Symbol Detail → exact Anomaly Detail → Back;
- two same-symbol anomalies with different UUIDs;
- pointer activation;
- desktop Enter and Space activation;
- visible responsive focus restoration;
- mode replacement while detail is open;
- symbol replacement while detail is open;
- Close, Escape and backdrop behavior;
- Tab and Shift+Tab containment;
- body scroll lock;
- pathname remains `/` or `/dashboard`;
- zero console errors, page errors and unhandled rejections.

Capture at least eight deterministic screenshots covering changed Symbol Detail and Anomaly Detail states across both modes and viewports, with BTCUSDT and ETHUSDT represented.

Record screenshot paths and SHA-256 hashes in the implementation report. Remove temporary browser artifacts before committing unless the repository already owns an authorized evidence location inside the lease; no product screenshot files are authorized by this contract.

## 15. Diff and residual audit

Before committing run:

```bash
git diff --check
git diff --stat
git diff --name-status ba31a348dc5055935c45f6be81073688caedd925
```

Verify every path belongs to the exact lease.

Audit active source and tests for:

- Symbol Detail anomaly labels that still say market detail;
- Symbol Detail anomaly callbacks that still open Symbol Detail;
- `SymbolPopupReturnContext` value `"anomalies"`;
- ignored `variant="popup"` and `surface="popup"` props in the leased components;
- stale full anomaly objects stored in controller state;
- UUID resolution by symbol/index rather than exact ID.

Do not remove `route` formatting from `marketViewModel` or `marketAdapters`; that belongs to MP20R.

## 16. Product delivery

After every required gate passes, create exactly one product commit:

`fix(ui): open exact anomaly detail from symbol detail`

Verify:

- exact parent `ba31a348dc5055935c45f6be81073688caedd925`;
- exactly one commit ahead and zero behind;
- no merge commit;
- exact changed-path allowlist;
- clean worktree after commit.

Push only:

`p3/mp18r-exact-symbol-anomaly-detail`

Do not open a PR. Do not merge. Do not amend, rebase, squash, force-push, tag or rewrite history.

## 17. Connector implementation report

After the product commit and remote branch are verified, publish exactly:

`signalguard-rs/phase-3/reports/P3-MP18R/<PRODUCT_COMMIT_SHA>.md`

Use one connector commit:

`docs(phase-3): publish MP18R implementation report`

The report must include:

- contract commit and blob;
- exact product base and tree;
- product commit, parent and tree;
- exact changed paths;
- lease and forbidden-path audit;
- controller identity design;
- UUID source-resolution evidence;
- responsive focus-resolution evidence;
- focused and full test counts;
- frontend/global validation results;
- bundle bytes and topology;
- browser matrix;
- screenshot paths and hashes;
- console/page/unhandled-error counts;
- remote branch verification;
- clean worktrees;
- confirmation that no PR or merge was created.

Read back and verify the report blob and connector commit.

## 18. Terminal result

Return:

`P3_MP18R_COMPLETE`

only after all gates pass, the exact single product commit is pushed and the connector report is published and verified.

Return:

`P3_MP18R_BLOCKED_BY_SCOPE_OR_IDENTITY`

when the exact base, lease, behavior or required validation cannot be satisfied. Do not commit after a failed required gate.
