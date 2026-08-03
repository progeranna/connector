# P3-MP18R-R1 — Test-lease correction for exact anomaly detail

Status: `P3_MP18R_R1_IMPLEMENTATION_AUTHORIZED`

## 1. Mode

Continuation of the same local Codex implementation worker and the same preserved worktree.

Use the `$rust-development` skill.

Do not restart from a clean checkout. Do not recreate, reset, restore, clean, stash, rebase or discard the current worktree. Preserve all current uncommitted MP18R implementation work.

## 2. Authority

Read completely:

- `signalguard-rs/phase-3/prompts/P3-MP18R.md`
- `signalguard-rs/phase-3/prompts/P3-MP18R-DIAGNOSTIC.md`
- `signalguard-rs/phase-3/reports/P3-MP18R-DIAGNOSTIC/ba31a348dc5055935c45f6be81073688caedd925.md`
- `signalguard-rs/phase-3/control/MICRO_PHASE_LEDGER.md`
- `signalguard-rs/phase-3/control/IMPLEMENTATION_SEQUENCE.md`
- `signalguard-rs/phase-3/control/STATUS.md`

This R1 addendum changes only the writable test lease and the recovery instruction below. Every unchanged requirement from the original MP18R contract remains binding.

## 3. Immutable product identity

- Product repository: `progeranna/signalguard-rs`
- Immutable base: `ba31a348dc5055935c45f6be81073688caedd925`
- Base tree: `f629b6ea4339c92d03223c3bd8024cd4cb4571da`
- Assigned branch: `p3/mp18r-exact-symbol-anomaly-detail`
- Existing worktree: `/Users/anion/Desktop/work/git-signalguard-rs/worktrees/p3-mp18r`
- Required single product commit: `fix(ui): open exact anomaly detail from symbol detail`

The existing worktree was diagnosed at the immutable base with zero commits ahead/behind, ten uncommitted leased-file changes and no untracked files.

Stop with `P3_MP18R_R1_BLOCKED_BY_SCOPE_OR_IDENTITY` if the existing worktree no longer has that preserved identity or if unexplained additional paths are present.

## 4. Corrected exact writable lease

### Original production lease — unchanged

- `web/src/pages/DashboardPage.tsx`
- `web/src/features/dashboard/SymbolDetailAnomalies.tsx`
- `web/src/features/dashboard/SymbolDetailHeader.tsx`
- `web/src/features/dashboard/SymbolDetailMetrics.tsx`
- `web/src/features/dashboard/symbolPopup.ts`

### Original focused-test lease — unchanged

- `web/src/pages/DashboardPage.popup.test.tsx`
- `web/src/features/dashboard/SymbolDetailAnomalies.test.tsx`
- `web/src/features/dashboard/SymbolDetailHeader.test.tsx`
- `web/src/features/dashboard/SymbolDetailMetrics.test.tsx`
- `web/src/features/dashboard/symbolPopup.test.ts`

### R1 added test-only lease

- `web/src/features/dashboard/symbolPopupResource.test.tsx`
- `web/src/pages/DashboardPage.test.tsx`

The final product diff may contain at most these twelve exact paths.

No additional production path is authorized.

## 5. Mandatory recovery actions

1. Keep all valid current implementation work in the preserved worktree.
2. In `symbolPopup.ts`, restore strict `SymbolPopupReturnContext` typing.
3. Remove the temporary workaround that accepts arbitrary `string` values or normalizes unsupported return contexts.
4. Update `symbolPopupResource.test.tsx` so popup resource identity uses a valid remaining return context and continues proving presentation context is not added to server requests.
5. Update `DashboardPage.test.tsx` retained-source assertions to require the accepted prop-free wiring:
   - no `variant="popup"` on `SymbolDetailHeader`;
   - no `surface="popup"` on `SymbolDetailMetrics`;
   - no `variant="popup"` on `SymbolDetailAnomalies`;
   - exact anomaly-detail callback instead of `onOpenSymbolDetail`.
6. Do not satisfy stale tests by reintroducing obsolete source strings in comments, dead code or compatibility shims.
7. Re-run the residual audit for all removed concepts.

## 6. Added focused validation

In addition to the original focused suite, run:

```bash
npm run test:run -- \
  src/features/dashboard/symbolPopupResource.test.tsx \
  src/pages/DashboardPage.test.tsx
```

The complete focused set is now seven test files:

- `DashboardPage.popup.test.tsx`
- `SymbolDetailAnomalies.test.tsx`
- `SymbolDetailHeader.test.tsx`
- `SymbolDetailMetrics.test.tsx`
- `symbolPopup.test.ts`
- `symbolPopupResource.test.tsx`
- `DashboardPage.test.tsx`

Then rerun every original required full gate:

- full Vitest;
- typecheck;
- lint;
- build;
- bundle tests and bundle check;
- Rust/global repository gates;
- exact diff and residual audits;
- deterministic browser matrix and screenshots.

## 7. Diff audit

Before commit, verify:

- every changed path is one of the twelve exact paths;
- no untracked file exists;
- the strict return-context union contains only valid contexts;
- no `"anomalies"` SymbolPopup return context remains in active source or tests;
- no removed popup-only prop remains in active source or stale source-string tests;
- no Symbol Detail anomaly callback opens Symbol Detail;
- no same-symbol or summary fallback replaces exact UUID ownership.

## 8. Delivery — unchanged

After all gates pass:

- create exactly one product commit: `fix(ui): open exact anomaly detail from symbol detail`;
- parent must be `ba31a348dc5055935c45f6be81073688caedd925`;
- push only `p3/mp18r-exact-symbol-anomaly-detail`;
- do not open a PR or merge;
- publish the implementation report at `signalguard-rs/phase-3/reports/P3-MP18R/<PRODUCT_COMMIT_SHA>.md` using connector commit message `docs(phase-3): publish MP18R implementation report`;
- include original contract, diagnostic and R1 identities in the report.

## 9. Terminal result

Return `P3_MP18R_COMPLETE` only after the complete original delivery succeeds under the corrected twelve-file lease.

Return `P3_MP18R_R1_BLOCKED_BY_SCOPE_OR_IDENTITY` if the preserved identity, corrected lease or required validation cannot be satisfied.
