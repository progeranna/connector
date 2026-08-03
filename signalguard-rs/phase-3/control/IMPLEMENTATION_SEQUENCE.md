# SignalGuard RS Phase 3 — Authoritative Implementation Sequence

Status: `P3_MP18R_IMPLEMENTATION_AUTHORIZED`

## 1. Immutable execution identity

- Product repository: `progeranna/signalguard-rs`
- Phase branch: `refactor/dashboard-modules`
- Current accepted product SHA: `ba31a348dc5055935c45f6be81073688caedd925`
- Current accepted product tree: `f629b6ea4339c92d03223c3bd8024cd4cb4571da`
- Authoritative ledger: `signalguard-rs/phase-3/control/MICRO_PHASE_LEDGER.md`
- Consolidated evidence: `signalguard-rs/phase-3/reports/P3-RECOVERY-INVENTORIES/ba31a348dc5055935c45f6be81073688caedd925.md`

The phase branch was verified identical to the accepted product SHA immediately before synthesis publication. No product branch, commit or pull request was created by synthesis.

## 2. Binding continuation sequence

```text
P3-MP18R
→ P3-MP20R
→ Checkpoint 2R
→ P3-W4-BRIDGE01
→ P3-W4-BRIDGE02
→ P3-MP21 / P3-MP22 / P3-MP24          [W4-G2 parallel]
→ P3-MP23 / P3-MP25 / P3-MP27          [W4-G3 parallel]
→ P3-MP26                               [W4-G4]
→ P3-MP28                               [W4-G5]
→ P3-MP29                               [W4-G6]
→ P3-MP30                               [W4-G7 audit]
→ Checkpoint 3
→ P3-MP31
→ P3-MP31A
→ P3-MP32 / P3-MP33 / P3-MP34          [D1 parallel]
→ P3-MP35
→ P3-MP36 / P3-MP37B                    [R1 parallel, disjoint leases]
→ P3-MP37A                              [R2; follows MP36]
→ P3-MP38                               [measured experiment]
→ P3-MP40 only if P3-MP38 is accepted
→ P3-MP41                               [measurement checkpoint]
→ P3-MP42 and P3-MP43                   [H1; serialize AppShell ownership]
→ P3-MP44 / P3-MP45                     [H2 test-first parallel]
→ P3-MP46                               [final smoke]
→ only then a new product Phase 4
```

`P3-MP39` is `SUPERSEDED_BY_ACCEPTED_IMPLEMENTATION` and is deliberately absent from implementation work.

## 3. Current authorization — P3-MP18R only

### Objective

`P3-MP18R — exact anomaly detail from Symbol Detail`

### Exact base

`ba31a348dc5055935c45f6be81073688caedd925`

The implementation contract must stop if `refactor/dashboard-modules` no longer resolves to this SHA.

### Required branch and commit

- Branch: `p3/mp18r-exact-symbol-anomaly-detail`
- Single product commit: `fix(ui): open exact anomaly detail from symbol detail`

### Exact writable lease

Production:

```text
web/src/pages/DashboardPage.tsx
web/src/features/dashboard/SymbolDetailAnomalies.tsx
web/src/features/dashboard/SymbolDetailHeader.tsx
web/src/features/dashboard/SymbolDetailMetrics.tsx
web/src/features/dashboard/symbolPopup.ts
```

Tests:

```text
web/src/pages/DashboardPage.popup.test.tsx
web/src/features/dashboard/SymbolDetailAnomalies.test.tsx
web/src/features/dashboard/SymbolDetailHeader.test.tsx
web/src/features/dashboard/SymbolDetailMetrics.test.tsx
web/src/features/dashboard/symbolPopup.test.ts
```

### Required product result

1. Desktop and mobile Symbol Detail anomaly activation opens Anomaly Detail by exact UUID.
2. Controller identity stores the exact anomaly UUID plus parent `SymbolPopupIdentity`; it does not store a stale full anomaly object.
3. The anomaly is resolved from the current active mode/symbol resource.
4. Back restores the same Symbol Detail identity and the exact visible triggering row/card.
5. Focus restoration must not select a hidden responsive duplicate.
6. Mode or symbol replacement clears incompatible anomaly detail and cannot flash stale content.
7. No Symbol Detail anomaly activation opens Symbol Detail.
8. Remove the unreachable Symbol Detail return context `"anomalies"`.
9. Remove ignored single-literal popup-only props `variant="popup"` and `surface="popup"` from the leased shared sections.
10. Preserve Dashboard → Symbol Detail, All Markets → Symbol Detail and All Anomalies → exact Anomaly Detail.

### Forbidden adjacent paths and behavior

- `web/src/features/dashboard/marketViewModel.ts`
- `web/src/features/dashboard/marketAdapters.ts`
- router or route files
- API, Zod schema, query-key or resource-identity files
- shared Dialog architecture
- Wave 4 vocabulary or tooltip work
- global CSS
- `web/src/app/GlobalMarketTicker.tsx`, ticker selectors and ticker keyframes
- package manifests, lockfiles or bundle budgets
- URL-backed modal state, standalone pages or public Replay

### Focused tests

- exact desktop UUID activation;
- exact mobile UUID activation;
- Anomaly Detail resolution from the current Symbol Detail resource;
- exact Back identity;
- exact visible row/card focus restoration;
- Demo/Live replacement and BTC/ETH replacement clear stale anomaly detail;
- no full anomaly object retained in controller state;
- no anomaly activation calls Symbol Detail;
- removed return context and ignored literal props have no remaining call sites.

### Full gates

From `web/`:

```text
npm run test:run -- src/pages/DashboardPage.popup.test.tsx \
  src/features/dashboard/SymbolDetailAnomalies.test.tsx \
  src/features/dashboard/SymbolDetailHeader.test.tsx \
  src/features/dashboard/SymbolDetailMetrics.test.tsx \
  src/features/dashboard/symbolPopup.test.ts
npm run test:run
npm run typecheck
npm run lint
npm run build
npm run bundle:check
```

Also require repository-root `git diff --check`, exact changed-path allowlist, one-commit discipline, no generated/untracked residue and exact-head CI.

### Browser and screenshot acceptance

Run pointer and keyboard flows for:

- Demo and Live;
- BTCUSDT and ETHUSDT;
- `1440×900` and width `390` mobile;
- Dashboard → Symbol Detail → exact Anomaly Detail → Back;
- All Markets → Symbol Detail → exact Anomaly Detail → Back;
- rapid mode and symbol replacement while detail is open;
- Tab/Shift+Tab containment, Escape, Close and exact focus restoration;
- zero unexpected console errors.

Capture at least one changed-state screenshot for each mode/viewport combination, with both BTCUSDT and ETHUSDT represented across the set.

### Terminal markers

- Success: `P3_MP18R_COMPLETE`
- Blocker: `P3_MP18R_BLOCKED_BY_SCOPE_OR_IDENTITY`

## 4. P3-MP20R — recorded but not authorized

P3-MP20R remains blocked until the exact accepted P3-MP18R head is integrated.

- Branch: `p3/mp20r-route-presentation-residue`
- Commit: `refactor(ui): remove obsolete route presentation residue`
- Lease: `web/src/features/dashboard/marketViewModel.ts`, `marketAdapters.ts`, `marketAdapters.test.ts`
- Result: remove route-only display variants and route-only anomaly formatting only.
- It must not reopen any P3-MP18R path.
- Success: `P3_MP20R_COMPLETE`
- Blocker: `P3_MP20R_BLOCKED_BY_MP18R_OR_SCOPE_CONFLICT`

No implementation worker may start P3-MP20R from `ba31a348…`; its base must be the separately accepted and integrated P3-MP18R head.

## 5. Checkpoint 2R release gate

Semantic bridge work remains blocked until the combined MP18R+MP20R tree passes:

- full frontend gates and exact-head CI;
- Demo/Live × BTC/ETH × 1440/390;
- Dashboard → Symbol Detail;
- Symbol Detail anomaly → exact Anomaly Detail → Back;
- All Markets → Symbol Detail → exact Anomaly Detail → Back;
- All Anomalies → exact Anomaly Detail → Back;
- pointer and keyboard;
- exact visible focus restoration;
- rapid mode/symbol switching;
- no route navigation, stale flash or unexpected console errors.

Checkpoint success: `P3_CHECKPOINT_2R_COMPLETE`.

## 6. Semantic bridge and Wave 4 release schedule

Neither bridge is authorized by this file.

### Bridge 01

- Branch: `p3/w4-bridge01-semantic-health-facts`
- Commit: `feat(api): expose semantic health facts`
- Must publish additive backend authority for Data Age, health thresholds, evaluation time, primary issue, measurement facts and exact identity.
- Must preserve endpoint identity, Demo determinism and Live isolation.

### Bridge 02

- Branch: `p3/w4-bridge02-semantic-adapters`
- Commit: `feat(ui): preserve semantic health facts`
- Follows accepted Bridge01.
- Sequentially reopens MP20R model/adapter files to add surface-neutral semantic facts.
- No JSX-local thresholds or fallback data.

### Safe grouped schedule

- `W4-G2`: P3-MP21, P3-MP22 and P3-MP24 may run together.
- `W4-G3`: P3-MP23, P3-MP25 and P3-MP27 may run together after G2.
- `W4-G4`: P3-MP26 only.
- `W4-G5`: P3-MP28 only.
- `W4-G6`: P3-MP29 only.
- `W4-G7`: P3-MP30 audits the accepted combined tree.

Collision constraints:

- MP21 and MP27 both own `AppShell.tsx` and are separated by groups.
- MP22, MP23 and MP26 own `TimelinePanel.tsx` and are separated by groups.
- MP24, MP25, MP26, MP28 and MP29 touch Dashboard callers and are sequenced.
- MP30 is the only broad caller audit and starts last.

Checkpoint 3 requires product-owner visual review before dialog work.

## 7. Dialog sequence

1. P3-MP31 creates `Dialog.tsx` and its test only; no caller migration.
2. P3-MP31A decomposes `DashboardPage.tsx` into the exact modal modules while retaining the legacy shell.
3. P3-MP32, P3-MP33 and P3-MP34 migrate disjoint modules in parallel.
4. P3-MP35 executes integrated keyboard/focus coverage and deletes `LegacyDashboardTableModal.tsx` after zero-import verification.

The post-MP31A tree, not the current monolith, is the authority for later modal leases.

## 8. Routing, containment and performance sequence

- P3-MP36 adds explicit wildcard 404 and preserves both compatibility redirects.
- P3-MP37B may run in parallel with MP36 only because its lease is modal-local and post-decomposition.
- P3-MP37A follows MP36 because both own router composition.
- P3-MP38 is a measured modal-feature split. Route-page splitting is forbidden.
- P3-MP38 is accepted only when initial JS is lower than the accepted 387,239-byte baseline, a real async edge exists, budgets pass and modal identity remains correct.
- P3-MP39 receives no implementation.
- P3-MP40 exists only after accepted MP38.
- P3-MP41 is a measurement checkpoint and normally has no product write.

## 9. Responsive and final sequence

- P3-MP42 owns complete selector keyboard behavior.
- P3-MP43 owns non-ticker reduced motion only.
- Because both may touch `AppShell.tsx`, their product writes must be serialized even though their broader work group is parallel.
- P3-MP44 and P3-MP45 are test-first. Any production defect creates a separate recovery lease; it is not fixed opportunistically.
- P3-MP46 is final modal-only browser smoke and normally has no production lease.

## 10. Permanent prohibitions

No future worker may:

- restore standalone Symbol Detail or Anomalies pages;
- synchronize modal state to URLs;
- route an All Anomalies row to Symbol Detail;
- change backend `/anomalies` endpoint validity;
- mix Demo and Live or expose public Replay;
- invent frontend thresholds;
- modify ticker text, order, scrolling behavior, CSS selectors or animation ownership;
- raise bundle budgets;
- execute the superseded Phase 4 anomaly-explorer plan;
- authorize a new product Phase 4 before P3-MP46 acceptance.

## 11. Connector publication record

This connector cannot atomically update multiple files through the available contents action, so synthesis uses the minimum sequential commits.

- `MICRO_PHASE_LEDGER.md`: commit `426c971a40630eef3c2a45651eff27d22a14b780`; blob `e251789d58420ddb70401c79fd935f2a9669907a`.
- `IMPLEMENTATION_SEQUENCE.md`: this file's resulting commit and blob are verified after publication and recorded in `STATUS.md`.
- `STATUS.md`: final publication commit; verified by exact read-back.

## 12. Current terminal state

`P3_MP18R_IMPLEMENTATION_AUTHORIZED`
