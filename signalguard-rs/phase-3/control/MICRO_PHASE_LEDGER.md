# SignalGuard RS Phase 3 — Micro-Phase Ledger

Status: `P3_MICRO_PHASE_LEDGER_CURRENT`

Authoritative product base: `ba31a348dc5055935c45f6be81073688caedd925`

Authoritative product tree: `f629b6ea4339c92d03223c3bd8024cd4cb4571da`

This ledger records the reconstructed state of the original `P3-MP00` through `P3-MP46` roadmap after Phase 3.5 optimization and the Phase 3.6 modal-only product-owner correction.

Status vocabulary:

- `COMPLETE` — integrated objective remains valid;
- `PARTIALLY_COMPLETE` — useful accepted work exists, but the original user-visible or architectural objective is not closed;
- `SUPERSEDED_BY_PRODUCT_OWNER` — incompatible objective replaced by an explicit user decision;
- `SUPERSEDED_BY_STRONGER_RESULT` — objective achieved or made obsolete by a stronger accepted implementation;
- `REQUIRES_REPLAN` — goal remains, but the old execution shape conflicts with the current architecture;
- `NOT_STARTED` — no accepted completion evidence;
- `REQUIRES_REVALIDATION` — substantial coverage exists but must be rerun after later changes.

## Ledger

| Micro-phase | State | Current disposition |
|---|---|---|
| P3-MP00 | COMPLETE | Post-Phase-2 inventory completed. |
| P3-MP01 | COMPLETE | Smoke matrix exists; modal-only surfaces supersede route surfaces. |
| P3-MP02 | COMPLETE | Accessible Tooltip primitive exists. |
| P3-MP03 | COMPLETE | Typed semantic status descriptors exist. |
| P3-MP04 | COMPLETE | Deterministic semantic fixtures exist. |
| P3-MP05 | COMPLETE | Timeline normalization integrated. |
| P3-MP06 | COMPLETE | Timeline domain calculation integrated. |
| P3-MP07 | COMPLETE | Market Health preview model integrated. |
| P3-MP08 | COMPLETE | Recent Anomalies preview model integrated with UUID identity. |
| P3-MP09 | COMPLETE | Resource-state mapping integrated through accepted replacement work. |
| P3-MP10 | COMPLETE | Timeline panel extracted and integrated. |
| P3-MP11 | COMPLETE | Market Health desktop table extracted and integrated. |
| P3-MP12 | COMPLETE | Market Health mobile cards extracted and integrated. |
| P3-MP13 | COMPLETE | Recent Anomalies desktop table extracted and integrated. |
| P3-MP14 | COMPLETE | Recent Anomalies mobile cards extracted and integrated. |
| P3-MP15 | COMPLETE | Dashboard compositor wiring integrated. |
| P3-MP16 | COMPLETE | Shared Symbol Detail header/status section integrated for modal use. |
| P3-MP17 | COMPLETE | Shared Symbol Detail metrics/state section integrated for modal use. |
| P3-MP18 | PARTIALLY_COMPLETE | Shared anomaly section exists; exact UUID activation from Symbol Detail still requires `P3-MP18R`. |
| P3-MP19 | SUPERSEDED_BY_PRODUCT_OWNER | Standalone Symbol Detail route removed; compatibility redirect is binding. |
| P3-MP20 | PARTIALLY_COMPLETE | Shared Symbol Detail modal is integrated; route residue and anomaly-to-symbol behavior require `P3-MP20R`. |
| P3-MP21 | PARTIALLY_COMPLETE | Pure System vocabulary exists; header still uses ambiguous Data status presentation. |
| P3-MP22 | PARTIALLY_COMPLETE | Timeline shows highest severity, but not severity plus detector and not `No Active Anomalies`. |
| P3-MP23 | PARTIALLY_COMPLETE | Data-age classifier exists; visible `Data Age` presentation and authoritative thresholds are not wired. |
| P3-MP24 | PARTIALLY_COMPLETE | Market descriptors exist; tables/cards still use generic health labels and lack truthful stale distinction. |
| P3-MP25 | PARTIALLY_COMPLETE | Severity descriptors and combined active label exist; current tables largely show severity alone. |
| P3-MP26 | NOT_STARTED | Selected-market semantic status/facts presentation not completed. |
| P3-MP27 | PARTIALLY_COMPLETE | Demo/Live explanation exists in header menu, but not through unified tooltip semantics. |
| P3-MP28 | NOT_STARTED | Composite health-score tooltip not completed. |
| P3-MP29 | NOT_STARTED | Observed/threshold/exceeded-by tooltip not completed. |
| P3-MP30 | NOT_STARTED | Unified tooltip copy and format audit not completed. |
| P3-MP31 | PARTIALLY_COMPLETE | Inline modal boundary has focus trap, initial/return focus, Escape, backdrop and scroll lock; shared portal primitive and description contract remain. |
| P3-MP32 | PARTIALLY_COMPLETE | Symbol Detail uses inline Dashboard modal boundary; migration to accepted shared primitive remains. |
| P3-MP33 | PARTIALLY_COMPLETE | All Markets uses inline Dashboard modal boundary; migration remains. |
| P3-MP34 | PARTIALLY_COMPLETE | All Anomalies and Anomaly Detail use inline boundary; migration and decomposition remain. |
| P3-MP35 | REQUIRES_REVALIDATION | Significant modal keyboard/focus tests and smoke matrix exist; rerun after shared primitive migration. |
| P3-MP36 | NOT_STARTED | Explicit 404 still required while preserving legacy redirects. |
| P3-MP37 | NOT_STARTED | Recoverable Dashboard/modal error boundaries still required. |
| P3-MP38 | REQUIRES_REPLAN | Standalone page splitting is obsolete; evaluate measured feature-level modal lazy loading after extraction. |
| P3-MP39 | SUPERSEDED_BY_STRONGER_RESULT | Recharts was removed; accepted native SVG timeline and bundle result are stronger. |
| P3-MP40 | REQUIRES_REPLAN | Suspense/failure fallback depends on actual lazy boundaries selected in re-planned MP38. |
| P3-MP41 | PARTIALLY_COMPLETE | Phase 3.5 bundle measurement is accepted; final measurement must be repeated after remaining Phase 3 work. |
| P3-MP42 | PARTIALLY_COMPLETE | Selector roles, focus and Escape exist; complete arrow-key menu semantics remain. |
| P3-MP43 | NOT_STARTED | Reduced-motion support remains; ticker ownership stays forbidden. |
| P3-MP44 | REQUIRES_REVALIDATION | Strong Timeline responsive tests exist; final regression follows Wave 4 and dialog work. |
| P3-MP45 | REQUIRES_REVALIDATION | Health/anomaly responsive coverage exists; final regression follows Wave 4 and dialog work. |
| P3-MP46 | NOT_STARTED | Final modal-only desktop/mobile smoke and user Phase 3 acceptance remain. |

## Recovery additions

These additions do not erase or renumber the original 47 micro-phases. They are narrow recovery/bridge contracts required by the current accepted architecture.

| Recovery unit | State | Purpose |
|---|---|---|
| P3-MP18R | AWAITING_CONTRACT | Exact UUID Anomaly Detail activation and Back/focus from Symbol Detail. |
| P3-MP20R | AWAITING_CONTRACT | Remove route-only display residue and obsolete anomaly-to-symbol semantics. |
| Checkpoint 2R | BLOCKED | Manual modal-only Wave 3 closure after MP18R/MP20R integration. |
| P3-W4-BRIDGE01 | AWAITING_INVENTORY | Minimal authoritative backend/API semantic facts; no scoring changes. |
| P3-W4-BRIDGE02 | BLOCKED | Frontend schemas/adapters after BRIDGE01 acceptance. |

## Required continuation

```text
P3-MP18R + P3-MP20R
→ Checkpoint 2R
→ P3-W4-BRIDGE01
→ P3-W4-BRIDGE02
→ P3-MP21–P3-MP25
→ P3-MP26–P3-MP30
→ Checkpoint 3
→ P3-MP31–P3-MP35
→ P3-MP36–P3-MP41
→ P3-MP42–P3-MP46
→ next product Phase 4 only after final Phase 3 acceptance
```

## Current authorization

Only parallel read-only inventories and connector-only synthesis are authorized. Product implementation requires separate reviewed contracts.
