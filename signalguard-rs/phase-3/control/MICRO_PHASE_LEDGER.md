# SignalGuard RS Phase 3 — Authoritative Micro-Phase Ledger

Status: `P3_MICRO_PHASE_LEDGER_RECOVERED`

## 1. Authority and immutable identity

- Product repository: `progeranna/signalguard-rs`
- Phase branch: `refactor/dashboard-modules`
- Accepted product SHA: `ba31a348dc5055935c45f6be81073688caedd925`
- Accepted product tree: `f629b6ea4339c92d03223c3bd8024cd4cb4571da`
- Synthesis authorization commit: `e4e42d04ac603b9040882dbacd1b5ab073b774eb`
- Synthesis contract blob: `f5271965a34a6abe8a17d3d1ce14fde23884071c`
- Consolidated evidence commit: `7585ac59e57e9358584daf05ae8bb670b5001a3a`
- Consolidated evidence blob: `fb45ca39d271b4bfa8ecb044e8c9f3a02cfef31d`

The phase branch was reverified as identical to the accepted product SHA immediately before publication. Because a Git commit immutably identifies its tree, the accepted tree remains `f629b6ea4339c92d03223c3bd8024cd4cb4571da`.

## 2. Binding product-owner overrides

These rules supersede incompatible older roadmap language:

- `/` and `/dashboard` are the only visual console pages.
- `/symbols/:symbol` and `/anomalies` remain replacement redirects to `/dashboard`.
- Market activation opens Dashboard-owned Symbol Detail.
- Anomaly activation opens exact UUID-keyed Anomaly Detail.
- All Anomalies rows never open Symbol Detail.
- Modal state remains ephemeral and local; modal URLs and modal deep links are forbidden.
- Standalone visual Symbol Detail and Anomalies pages are forbidden.
- Backend `/anomalies` remains valid.
- Demo and Live remain strictly isolated; public Replay remains forbidden.
- Ticker ownership is protected.
- Bundle budgets may not be raised.

## 3. Status vocabulary

Only these roadmap states are used:

- `COMPLETE`
- `PARTIALLY_COMPLETE`
- `SUPERSEDED_BY_PRODUCT_OWNER`
- `SUPERSEDED_BY_ACCEPTED_IMPLEMENTATION`
- `NOT_STARTED`
- `REQUIRES_REVALIDATION`

## 4. Original 47-item ledger

| Item | Status | Evidence-backed disposition |
|---|---|---|
| P3-MP00 | COMPLETE | Post-Phase-2 route/component/visual inventory completed. |
| P3-MP01 | COMPLETE | Reusable Demo/Live, BTC/ETH and responsive smoke matrix exists; its route surfaces are now modal-only. |
| P3-MP02 | COMPLETE | Accessible Tooltip primitive exists. |
| P3-MP03 | COMPLETE | Typed System, Market, anomaly, Data Age and tooltip descriptor vocabulary exists. |
| P3-MP04 | COMPLETE | Deterministic semantic fixtures exist. |
| P3-MP05 | COMPLETE | Timeline normalization is integrated. |
| P3-MP06 | COMPLETE | Timeline chart-domain calculation is integrated. |
| P3-MP07 | COMPLETE | Market Health preview model is integrated. |
| P3-MP08 | COMPLETE | Recent Anomalies preview and stable UUID identity are integrated. |
| P3-MP09 | COMPLETE | Dashboard resource-state mapping is present through accepted replacement work. |
| P3-MP10 | COMPLETE | Timeline panel is extracted and integrated. |
| P3-MP11 | COMPLETE | Market Health desktop table is extracted and integrated. |
| P3-MP12 | COMPLETE | Market Health mobile cards are extracted and integrated. |
| P3-MP13 | COMPLETE | Recent Anomalies desktop table is extracted and integrated. |
| P3-MP14 | COMPLETE | Recent Anomalies mobile cards are extracted and integrated. |
| P3-MP15 | COMPLETE | Dashboard compositor wiring is integrated. |
| P3-MP16 | COMPLETE | Shared Symbol Detail header/status section is integrated for modal use. |
| P3-MP17 | COMPLETE | Shared Symbol Detail metrics/state section is integrated for modal use. |
| P3-MP18 | PARTIALLY_COMPLETE | Shared anomaly presentation exists; exact UUID activation, nested return identity and visible responsive focus restoration remain and are assigned to P3-MP18R. |
| P3-MP19 | SUPERSEDED_BY_PRODUCT_OWNER | Standalone Symbol Detail route migration is forbidden; compatibility redirect is the accepted result. |
| P3-MP20 | PARTIALLY_COMPLETE | Shared popup presentation is integrated; pure route-presentation residue remains and is assigned to P3-MP20R. |
| P3-MP21 | PARTIALLY_COMPLETE | System vocabulary exists; rendered header remains ambiguous. |
| P3-MP22 | PARTIALLY_COMPLETE | Timeline shows highest severity but not severity plus detector or `No Active Anomalies`. |
| P3-MP23 | PARTIALLY_COMPLETE | Data-age classifier exists; visible Data Age and authoritative thresholds are not wired. |
| P3-MP24 | PARTIALLY_COMPLETE | Market descriptors exist; tables/cards do not yet render the approved vocabulary truthfully. |
| P3-MP25 | PARTIALLY_COMPLETE | Severity descriptors exist; current anomaly callers do not consistently include concise severity meaning. |
| P3-MP26 | NOT_STARTED | Selected-market semantic status and facts are not integrated. |
| P3-MP27 | PARTIALLY_COMPLETE | Demo/Live explanation exists in the menu but is not implemented through unified tooltip semantics. |
| P3-MP28 | NOT_STARTED | Health-score tooltip is not implemented from authoritative facts. |
| P3-MP29 | NOT_STARTED | Observed/threshold/exceeded-by tooltip is not implemented. |
| P3-MP30 | NOT_STARTED | Unified tooltip copy/format audit has not run on the accepted combined Wave 4 tree. |
| P3-MP31 | PARTIALLY_COMPLETE | Inline modal behavior is substantial, but no shared portal primitive or description contract exists. |
| P3-MP32 | PARTIALLY_COMPLETE | Symbol Detail uses the legacy inline shell; migration remains. |
| P3-MP33 | PARTIALLY_COMPLETE | All Markets uses the legacy inline shell; exact return-focus ownership remains. |
| P3-MP34 | PARTIALLY_COMPLETE | All Anomalies and Anomaly Detail use the legacy inline shell; migration remains. |
| P3-MP35 | REQUIRES_REVALIDATION | Existing keyboard/focus coverage must be rerun after primitive migration and legacy-shell deletion. |
| P3-MP36 | NOT_STARTED | Explicit wildcard 404 is absent. |
| P3-MP37 | NOT_STARTED | Dashboard and modal containment are split into P3-MP37A and P3-MP37B. |
| P3-MP38 | NOT_STARTED | Must be measured modal-feature lazy loading, not route-page splitting. |
| P3-MP39 | SUPERSEDED_BY_ACCEPTED_IMPLEMENTATION | Recharts is removed and accepted native SVG is already integrated; no implementation work is permitted. |
| P3-MP40 | NOT_STARTED | Exists only if P3-MP38 is accepted. |
| P3-MP41 | PARTIALLY_COMPLETE | Phase 3.5 measurements are accepted; final post-Phase-3 measurement remains. |
| P3-MP42 | PARTIALLY_COMPLETE | Basic menu roles/focus/Escape exist; full keyboard model remains. |
| P3-MP43 | NOT_STARTED | Non-ticker reduced-motion support remains. |
| P3-MP44 | REQUIRES_REVALIDATION | Timeline responsive coverage exists but must be rerun after semantic/dialog/performance work. |
| P3-MP45 | REQUIRES_REVALIDATION | Health/anomaly responsive coverage exists but must be rerun after semantic/dialog work. |
| P3-MP46 | NOT_STARTED | Final modal-only browser smoke and Phase 3 acceptance remain. |

## 5. Reusable validation profiles

### `V-FRONTEND`

1. Run every focused Vitest file named by the item.
2. From `web/`: `npm run test:run`.
3. `npm run typecheck`.
4. `npm run lint`.
5. `npm run build`.
6. `npm run bundle:check` with unchanged budgets.
7. Repository-root `git diff --check`.
8. Verify one product commit, exact base, exact changed-path allowlist, no untracked/generated residue, and no dependency or lockfile drift unless explicitly leased.

### `V-BACKEND-CONTRACT`

1. Focused Rust tests for changed config/scoring/API/contract modules.
2. `cargo fmt --all -- --check`.
3. `cargo clippy --workspace --all-targets --all-features -- -D warnings`.
4. `cargo test --workspace --all-targets --all-features`.
5. OpenAPI/DTO contract consistency checks.
6. Full `V-FRONTEND`, including schema and isolation tests.
7. Demo determinism, Live isolation and no endpoint-identity regression.

### `V-TEST-FIRST`

1. Focused test files only in the declared test lease.
2. Full `V-FRONTEND`.
3. Confirm zero production-path changes. Any discovered product defect blocks the item and requires a new narrow recovery lease.

### `V-MEASUREMENT`

1. Clean production build from the accepted base/head.
2. `npm run test:run`, `typecheck`, `lint`, `build`, `bundle:check`.
3. Record initial JS, total JS, largest asset and async-edge topology.
4. Compare against the accepted 387,239-byte initial-JS baseline where applicable.
5. Budgets remain unchanged; measurement does not authorize a budget increase.

## 6. Browser evidence profiles

- Desktop viewport: `1440×900`.
- Mobile viewport: `390×844` or the nearest stable browser viewport with width exactly 390.
- Visible work requires Demo and Live, BTCUSDT and ETHUSDT, pointer and keyboard flows, zero unexpected console errors and screenshots named by item/mode/market/viewport.
- Modal work additionally requires Tab/Shift+Tab containment, Escape, Close, backdrop, body lock, Back and exact visible focus restoration.
- Screenshots must capture the changed state, not merely the page shell.

## 7. Detailed non-complete and superseded records

### P3-MP18 → P3-MP18R — exact anomaly detail from Symbol Detail

- Current evidence: desktop Symbol Detail anomaly rows are inert; mobile cards activate Symbol Detail; controller state cannot represent an anomaly nested under a Symbol Detail resource; responsive focus lookup may select a hidden duplicate.
- Exact remaining result: store `{ anomalyId, parent SymbolPopupIdentity }`; resolve by UUID from the current mode/symbol resource; never store a full stale anomaly object; desktop/mobile activation opens exact Anomaly Detail; Back restores the same Symbol Detail and exact visible row/card focus; mode/symbol replacement clears stale detail; remove unreachable return context `"anomalies"`; remove ignored single-literal `variant="popup"` and `surface="popup"` props.
- Exact writable lease: `web/src/pages/DashboardPage.tsx`; `web/src/features/dashboard/SymbolDetailAnomalies.tsx`; `SymbolDetailHeader.tsx`; `SymbolDetailMetrics.tsx`; `symbolPopup.ts`; and the matching `DashboardPage.popup.test.tsx`, `SymbolDetailAnomalies.test.tsx`, `SymbolDetailHeader.test.tsx`, `SymbolDetailMetrics.test.tsx`, `symbolPopup.test.ts`.
- Forbidden adjacent paths: routes/router; `marketViewModel.ts`; `marketAdapters.ts`; API/query/schema/resource identity; shared Dialog architecture; Wave 4 vocabulary; CSS; ticker; package/lockfiles.
- Dependencies: exact base `ba31a348dc5055935c45f6be81073688caedd925`.
- Safe group: `W3-R1`, exclusive.
- Branch: `p3/mp18r-exact-symbol-anomaly-detail`.
- Commit: `fix(ui): open exact anomaly detail from symbol detail`.
- Focused tests: all five leased test files; exact UUID desktop/mobile activation; nested Back; visible focus restoration; Demo/Live and symbol stale-state clearing; no anomaly-to-symbol activation.
- Validation: `V-FRONTEND`.
- Browser/screenshots: full Checkpoint 2R subset for Dashboard → Symbol Detail → Anomaly Detail → Back in Demo/Live, BTC/ETH, 1440/390; pointer and keyboard; at least eight changed-state screenshots; zero console errors.
- Success marker: `P3_MP18R_COMPLETE`.
- Blocker marker: `P3_MP18R_BLOCKED_BY_SCOPE_OR_IDENTITY`.
- Authorization: `AUTHORIZED` by this synthesis. This is the only product implementation authorized.

### P3-MP19 — standalone route objective

- Current evidence: `/symbols/:symbol` is an accepted replacement redirect and `/` plus `/dashboard` are the only visual pages.
- Exact remaining result: none; preserve the redirect and modal-only ownership.
- Exact writable lease: `NONE`.
- Forbidden adjacent paths: all product paths for the purpose of restoring a standalone page or URL-backed modal state.
- Dependencies/safe group: permanent product-owner override.
- Branch/commit: `NONE`.
- Focused tests/validation: router compatibility-redirect tests remain green under `V-FRONTEND` whenever router work occurs.
- Browser/screenshots: `/symbols/BTCUSDT` must replace-navigate to `/dashboard` without rendering a standalone detail page.
- Success marker: `P3_MP19_SUPERSEDED_BY_PRODUCT_OWNER`.
- Blocker marker: `P3_MP19_BLOCKED_BY_STANDALONE_ROUTE_REGRESSION`.

### P3-MP20 → P3-MP20R — pure route-presentation residue cleanup

- Current evidence: `MarketDisplayVariants` retains route/popup values and adapters still calculate route-only anomaly formatting.
- Exact remaining result: remove route-only display variants and dead route/popup parity formatting without changing modal interaction, resources or presentation.
- Exact writable lease: `web/src/features/dashboard/marketViewModel.ts`; `marketAdapters.ts`; `marketAdapters.test.ts`.
- Forbidden adjacent paths: every MP18R path; Dashboard controller; routes; schemas; resources; visible copy/CSS; ticker.
- Dependencies: accepted integrated P3-MP18R head.
- Safe group: `W3-R2`, exclusive and sequential.
- Branch: `p3/mp20r-route-presentation-residue`.
- Commit: `refactor(ui): remove obsolete route presentation residue`.
- Focused tests: `marketAdapters.test.ts`; compile-time absence of route variants; unchanged popup output fixtures.
- Validation: `V-FRONTEND`; no browser screenshot required because result is pure and presentation-neutral, but Checkpoint 2R follows.
- Success marker: `P3_MP20R_COMPLETE`.
- Blocker marker: `P3_MP20R_BLOCKED_BY_MP18R_OR_SCOPE_CONFLICT`.
- Authorization: `BLOCKED` until P3-MP18R is integrated and accepted.

### Checkpoint 2R

- Current evidence: modal-only flows exist but Symbol Detail nested anomaly flow is incomplete.
- Exact remaining result: combined-tree acceptance of MP18R and MP20R.
- Writable lease/branch/commit: `NONE`; verification checkpoint.
- Dependencies: accepted MP18R and MP20R.
- Safe group: `W3-CHECKPOINT`.
- Tests/validation: full `V-FRONTEND` on combined tree.
- Browser/screenshots: Demo/Live × BTC/ETH × 1440/390 for Dashboard → Symbol Detail; Symbol Detail anomaly → exact Anomaly Detail → Back; All Markets → Symbol Detail → Anomaly Detail → Back; All Anomalies → Anomaly Detail → Back; pointer/keyboard; rapid mode/symbol switching; no route navigation, stale flash or console errors.
- Success marker: `P3_CHECKPOINT_2R_COMPLETE`.
- Blocker marker: `P3_CHECKPOINT_2R_BLOCKED`.

### P3-W4-BRIDGE01 — backend semantic facts

- Current evidence: backend owns health/detector thresholds, penalties and evaluation data, but delayed threshold, evaluated time, rich health facts, primary issue and measurement semantics are not fully public.
- Exact remaining result: additive validated `delayed_after_ms` with `0 <= delayed_after_ms <= stale_after_ms`; expose evaluated time, degraded/unhealthy thresholds, deterministic primary issue, penalty/observed/threshold/unit/comparison/exceeded-by facts and exact source/mode/symbol identity; align Demo with runtime configuration; preserve endpoints and Demo/Live isolation.
- Exact writable lease: `src/config.rs`; `src/health/scoring.rs`; `src/api/dto.rs`; `src/api/handlers.rs`; `src/api/demo_data.rs`; `src/api/contract.rs`; `contracts/web-console.openapi.json`; directly matching Rust tests within those modules only.
- Forbidden adjacent paths: frontend; endpoint paths; detector algorithms unrelated to fact exposure; database/migrations; ticker; public Replay.
- Dependencies: Checkpoint 2R.
- Safe group: `W4-B1`, exclusive.
- Branch: `p3/w4-bridge01-semantic-health-facts`.
- Commit: `feat(api): expose semantic health facts`.
- Focused tests: config validation boundaries; DTO/OpenAPI serialization; Demo determinism; Live identity; primary-issue determinism; observed/threshold arithmetic.
- Validation: `V-BACKEND-CONTRACT`.
- Browser/screenshots: none; contract-only.
- Success marker: `P3_W4_BRIDGE01_COMPLETE`.
- Blocker marker: `P3_W4_BRIDGE01_BLOCKED_BY_MISSING_BACKEND_AUTHORITY`.
- Authorization: `BLOCKED`.

### P3-W4-BRIDGE02 — frontend preservation and pure semantic adapters

- Current evidence: frontend schemas drop rich health fields and JSX lacks one pure semantic ownership layer.
- Exact remaining result: preserve all Bridge01 facts in Zod/types; verify source/mode/symbol identity; create pure System/Market/Data Age/tooltip adapters; prohibit JSX-local threshold classification and fallback data.
- Exact writable lease: `web/src/features/dashboard/types.ts`; `types.test.ts`; `api-contract.test.ts`; `marketViewModel.ts`; `marketAdapters.ts`; `marketAdapters.test.ts`; `symbolMarketResource.ts`; `marketDataIsolation.test.tsx`; `web/src/test/marketFixtures.ts`; new `semanticAdapters.ts`; `semanticAdapters.test.ts`; new `semanticTooltipFacts.ts`; `semanticTooltipFacts.test.ts`.
- Forbidden adjacent paths: JSX callers; routes; CSS; ticker; backend; package/lockfiles.
- Dependencies: accepted Bridge01 contract and accepted MP20R result. Sequential reopening of MP20R model/adapter paths is intentional.
- Safe group: `W4-B2`, exclusive.
- Branch: `p3/w4-bridge02-semantic-adapters`.
- Commit: `feat(ui): preserve semantic health facts`.
- Focused tests: every leased test; unknown/missing fields fail safely; no Demo fallback in Live; threshold boundaries; identity mismatch rejection.
- Validation: `V-FRONTEND` plus OpenAPI/schema parity.
- Browser/screenshots: none; pure data layer.
- Success marker: `P3_W4_BRIDGE02_COMPLETE`.
- Blocker marker: `P3_W4_BRIDGE02_BLOCKED_BY_BRIDGE01_OR_IDENTITY`.
- Authorization: `BLOCKED`.

### P3-MP21 — System status indicator

- Evidence/result: descriptors exist; replace ambiguous header copy with entity-qualified System state and authoritative facts.
- Lease: `web/src/app/AppShell.tsx`; `AppShell.test.tsx`.
- Forbidden: `GlobalMarketTicker.tsx`; ticker CSS/keyframes; selector keyboard behavior; mode labels; DashboardPage; semantic adapters except imports.
- Dependencies/group: Bridge02; `W4-G2` parallel with MP22 and MP24.
- Branch/commit: `p3/mp21-system-status-indicator`; `feat(ui): qualify system status indicator`.
- Focused tests: System Healthy/Degraded/Critical/Offline/Unknown; facts and accessible tooltip; Live never uses Demo facts.
- Validation: `V-FRONTEND`.
- Browser/screenshots: Demo/Live header at 1440 and 390, including keyboard tooltip; four screenshots.
- Success/blocker: `P3_MP21_COMPLETE`; `P3_MP21_BLOCKED_BY_SEMANTIC_FACTS`.

### P3-MP22 — chart anomaly indicator

- Evidence/result: highest severity exists; render `Severity · Detector` or `No Active Anomalies` from semantic adapters.
- Lease: `web/src/features/dashboard/TimelinePanel.tsx`; `TimelinePanel.test.tsx`.
- Forbidden: Data Age block; selected-market status facts; chart renderer; DashboardPage; CSS/ticker.
- Dependencies/group: Bridge02; `W4-G2` parallel with MP21 and MP24.
- Branch/commit: `p3/mp22-chart-anomaly-indicator`; `feat(ui): show anomaly severity and detector`.
- Focused tests: each severity, detector formatting, none state, mode/symbol isolation.
- Validation/browser: `V-FRONTEND`; Demo/Live BTC/ETH 1440/390, four representative screenshots.
- Success/blocker: `P3_MP22_COMPLETE`; `P3_MP22_BLOCKED_BY_TIMELINE_IDENTITY`.

### P3-MP23 — Data Age

- Evidence/result: classifier exists; replace `Freshness` with `Data Age`, state, age, delayed/stale thresholds and last event using backend values only.
- Lease: `web/src/features/dashboard/TimelinePanel.tsx`; `TimelinePanel.test.tsx`.
- Forbidden: anomaly indicator; selected-market status; hardcoded thresholds; DashboardPage; CSS/ticker.
- Dependencies/group: Bridge02 and accepted G2; `W4-G3` parallel with MP25 and MP27.
- Branch/commit: `p3/mp23-data-age-indicator`; `feat(ui): add authoritative data age indicator`.
- Focused tests: Fresh/Delayed/Stale/No Data exact boundaries and tooltip facts.
- Validation/browser: `V-FRONTEND`; all four Data Age states at 1440 and 390; screenshots for each state.
- Success/blocker: `P3_MP23_COMPLETE`; `P3_MP23_BLOCKED_BY_THRESHOLD_AUTHORITY`.

### P3-MP24 — Market Health vocabulary

- Evidence/result: descriptors exist; render Market Healthy/Degraded/Critical/Stale/No Data consistently in preview and All Markets, desktop/mobile, with concise explanation.
- Lease: `web/src/features/dashboard/MarketHealthDesktopTable.tsx`; `MarketHealthDesktopTable.test.tsx`; `MarketHealthMobileCards.tsx`; `MarketHealthMobileCards.test.tsx`; `web/src/pages/DashboardPage.tsx`; `DashboardPage.test.tsx`.
- Forbidden: anomaly callers; HealthScore tooltip; modal architecture; routes; CSS/ticker.
- Dependencies/group: Bridge02; `W4-G2` parallel with MP21 and MP22.
- Branch/commit: `p3/mp24-market-health-vocabulary`; `feat(ui): qualify market health states`.
- Focused tests: all five states, desktop/mobile parity, All Markets parity, stale truth from backend threshold.
- Validation/browser: `V-FRONTEND`; preview and All Markets in Demo/Live at 1440/390; eight screenshots.
- Success/blocker: `P3_MP24_COMPLETE`; `P3_MP24_BLOCKED_BY_MARKET_STATE_AUTHORITY`.

### P3-MP25 — Recent Anomalies severity semantics

- Evidence/result: descriptors exist; expose concise meaning for Critical/Warning/Info in preview and All Anomalies without changing UUID ownership.
- Lease: `web/src/features/dashboard/RecentAnomaliesDesktopTable.tsx`; `RecentAnomaliesDesktopTable.test.tsx`; `RecentAnomaliesMobileCards.tsx`; `RecentAnomaliesMobileCards.test.tsx`; `web/src/pages/DashboardPage.tsx`; `DashboardPage.test.tsx`.
- Forbidden: anomaly controller identity; observed/threshold tooltip; modal shell; routes; CSS/ticker.
- Dependencies/group: Bridge02 and accepted G2; `W4-G3` parallel with MP23 and MP27.
- Branch/commit: `p3/mp25-anomaly-severity-semantics`; `feat(ui): explain anomaly severity semantics`.
- Focused tests: all severities, desktop/mobile/modal parity, UUID activation unchanged.
- Validation/browser: `V-FRONTEND`; preview and All Anomalies 1440/390; six screenshots.
- Success/blocker: `P3_MP25_COMPLETE`; `P3_MP25_BLOCKED_BY_ANOMALY_IDENTITY`.

### P3-MP26 — selected-market status and facts

- Evidence/result: no integrated selected-market semantic presentation; render entity-qualified Market state with score, primary issue, last event and last evaluation.
- Lease: `web/src/features/dashboard/TimelinePanel.tsx`; `TimelinePanel.test.tsx`; `web/src/pages/DashboardPage.tsx`; `DashboardPage.test.tsx`.
- Forbidden: System indicator; Market Health table vocabulary; threshold invention; Symbol Detail interaction; CSS/ticker.
- Dependencies/group: accepted G3; `W4-G4`, exclusive.
- Branch/commit: `p3/mp26-selected-market-status`; `feat(ui): add selected market status facts`.
- Focused tests: all market states, exact selected mode/symbol identity, fact omission rules, loading/error/no-data.
- Validation/browser: `V-FRONTEND`; Demo/Live BTC/ETH 1440/390; eight screenshots.
- Success/blocker: `P3_MP26_COMPLETE`; `P3_MP26_BLOCKED_BY_SELECTED_MARKET_FACTS`.

### P3-MP27 — Demo/Live explanation

- Evidence/result: explanatory copy exists; migrate to unified accessible tooltip while preserving visible labels and strict isolation.
- Lease: `web/src/app/AppShell.tsx`; `AppShell.test.tsx`.
- Forbidden: System indicator; selector keyboard model; mode labels/order; URL behavior; ticker/CSS.
- Dependencies/group: accepted G2; `W4-G3` parallel with MP23 and MP25.
- Branch/commit: `p3/mp27-mode-tooltip`; `feat(ui): unify demo and live explanation`.
- Focused tests: visible labels unchanged, tooltip accessible by hover/focus, exact source/isolation copy, no Replay.
- Validation/browser: `V-FRONTEND`; Demo and Live at 1440/390 with keyboard focus; four screenshots.
- Success/blocker: `P3_MP27_COMPLETE`; `P3_MP27_BLOCKED_BY_MODE_COPY_OR_ISOLATION`.

### P3-MP28 — Health-score tooltip

- Evidence/result: tooltip absent and frontend duplicates score thresholds; explain composite score using backend facts only.
- Lease: `web/src/features/dashboard/HealthScore.tsx`; `HealthScore.test.tsx`; `MarketHealthDesktopTable.tsx`; `MarketHealthDesktopTable.test.tsx`; `MarketHealthMobileCards.tsx`; `MarketHealthMobileCards.test.tsx`; `web/src/pages/DashboardPage.tsx`; `DashboardPage.test.tsx`.
- Forbidden: scoring behavior/thresholds; backend; anomaly callers; modal architecture; ticker/CSS.
- Dependencies/group: MP24 and MP26; `W4-G5`, exclusive.
- Branch/commit: `p3/mp28-health-score-tooltip`; `feat(ui): explain authoritative health score`.
- Focused tests: score/penalty facts, absent facts, desktop/mobile/modal parity, no hardcoded threshold.
- Validation/browser: `V-FRONTEND`; Market Health preview, All Markets and Symbol Detail at 1440/390; six screenshots.
- Success/blocker: `P3_MP28_COMPLETE`; `P3_MP28_BLOCKED_BY_SCORE_FACTS`.

### P3-MP29 — observed/threshold tooltip

- Evidence/result: presentation absent; explain observed value, threshold, comparison, unit and exceeded-by where authoritative facts exist.
- Lease: `web/src/features/dashboard/RecentAnomaliesDesktopTable.tsx`; `RecentAnomaliesDesktopTable.test.tsx`; `RecentAnomaliesMobileCards.tsx`; `RecentAnomaliesMobileCards.test.tsx`; `web/src/pages/DashboardPage.tsx`; `DashboardPage.test.tsx`; `web/src/features/dashboard/SymbolDetailAnomalies.tsx`; `SymbolDetailAnomalies.test.tsx`.
- Forbidden: detector thresholds in JSX; anomaly UUID/controller changes; backend; CSS/ticker.
- Dependencies/group: MP25 and MP28; `W4-G6`, exclusive.
- Branch/commit: `p3/mp29-observed-threshold-tooltip`; `feat(ui): explain anomaly threshold facts`.
- Focused tests: units/comparisons/exceeded-by, missing facts, preview/modal/Symbol Detail parity, UUID unchanged.
- Validation/browser: `V-FRONTEND`; representative detector facts across all anomaly surfaces at 1440/390; eight screenshots.
- Success/blocker: `P3_MP29_COMPLETE`; `P3_MP29_BLOCKED_BY_THRESHOLD_FACTS`.

### P3-MP30 — unified tooltip audit

- Evidence/result: infrastructure exists; audit the accepted combined Wave 4 tree to entity title + one short explanation + one-to-three facts + proper time fact, approximately four-to-six lines.
- Lease: `web/src/shared/components/Tooltip.tsx`; `Tooltip.test.tsx`; `web/src/features/dashboard/semanticTooltipFacts.ts`; `semanticTooltipFacts.test.ts`; `web/src/app/AppShell.tsx`; `AppShell.test.tsx`; `web/src/features/dashboard/TimelinePanel.tsx`; `TimelinePanel.test.tsx`; `HealthScore.tsx`; `HealthScore.test.tsx`; `MarketHealthDesktopTable.tsx`; `MarketHealthDesktopTable.test.tsx`; `MarketHealthMobileCards.tsx`; `MarketHealthMobileCards.test.tsx`; `RecentAnomaliesDesktopTable.tsx`; `RecentAnomaliesDesktopTable.test.tsx`; `RecentAnomaliesMobileCards.tsx`; `RecentAnomaliesMobileCards.test.tsx`; `SymbolDetailAnomalies.tsx`; `SymbolDetailAnomalies.test.tsx`; `web/src/pages/DashboardPage.tsx`; `DashboardPage.test.tsx`.
- Forbidden: new semantics, thresholds, layout redesign, dependencies, ticker/CSS.
- Dependencies/group: MP21–MP29; `W4-G7`, exclusive final audit.
- Branch/commit: `p3/mp30-tooltip-format-audit`; `refactor(ui): unify semantic tooltip format`.
- Focused tests: every leased tooltip test plus keyboard/focus accessibility and line/fact constraints.
- Validation/browser: `V-FRONTEND`; representative tooltip screenshots for System, mode, chart anomaly, Data Age, Market state, health score and detector facts at both widths.
- Success/blocker: `P3_MP30_COMPLETE`; `P3_MP30_BLOCKED_BY_WAVE4_INCONSISTENCY`.

### Checkpoint 3

- Result: product-owner visual review of each accepted Wave 4 item on the combined tree.
- Lease/branch/commit: `NONE`.
- Dependencies: MP21–MP30.
- Validation: full `V-FRONTEND`; screenshots from each item; zero console errors.
- Success/blocker: `P3_CHECKPOINT_3_COMPLETE`; `P3_CHECKPOINT_3_BLOCKED`.

### P3-MP31 — shared Dialog primitive

- Evidence/result: inline shell has partial lifecycle; create portal, robust focus trap, initial/return focus, Escape, backdrop, body lock, `aria-labelledby` and `aria-describedby`; no caller migration.
- Lease: new `web/src/shared/components/Dialog.tsx`; new `Dialog.test.tsx`.
- Forbidden: DashboardPage; modal callers; visible styling redesign; routes; CSS/ticker.
- Dependencies/group: Checkpoint 3; `D0`, exclusive before MP31A.
- Branch/commit: `p3/mp31-dialog-primitive`; `feat(ui): add accessible dialog primitive`.
- Focused tests: portal, tab cycle, hidden/disabled filtering, initial/return focus, Escape, backdrop, body lock nesting, labels/descriptions.
- Validation: `V-FRONTEND`; no screenshots because no callers migrate.
- Success/blocker: `P3_MP31_COMPLETE`; `P3_MP31_BLOCKED_BY_DIALOG_CONTRACT`.

### P3-MP31A — structural modal decomposition

- Evidence/result: DashboardPage concentrates controller and four modal surfaces; move code only without adopting Dialog.
- Lease: `web/src/pages/DashboardPage.tsx`; `DashboardPage.test.tsx`; new `web/src/features/dashboard/modals/LegacyDashboardTableModal.tsx`; `SymbolDetailModal.tsx`; `AllMarketsModal.tsx`; `AnomalyModals.tsx`.
- Forbidden: behavior/copy/style changes; Dialog adoption; route/resource/semantic changes; CSS/ticker.
- Dependencies/group: MP31; `D0A`, exclusive.
- Branch/commit: `p3/mp31a-modal-decomposition`; `refactor(ui): decompose dashboard modal surfaces`.
- Focused tests: existing Dashboard and popup tests prove byte-for-behavior interaction parity and imports.
- Validation/browser: `V-FRONTEND`; before/after screenshots for all four modal surfaces at 1440/390.
- Success/blocker: `P3_MP31A_COMPLETE`; `P3_MP31A_BLOCKED_BY_BEHAVIOR_DRIFT`.

### P3-MP32 — Symbol Detail migration

- Evidence/result: migrate post-decomposition Symbol Detail modal to Dialog without changing identity, nested anomaly or presentation.
- Lease: `web/src/features/dashboard/modals/SymbolDetailModal.tsx`; new `SymbolDetailModal.test.tsx`.
- Forbidden: Dashboard controller; other modal modules; semantic copy; routes/CSS/ticker.
- Dependencies/group: MP31 and MP31A; `D1` parallel with MP33 and MP34.
- Branch/commit: `p3/mp32-symbol-dialog-migration`; `refactor(ui): migrate symbol detail to dialog`.
- Focused tests: lifecycle, exact focus return, nested anomaly entry compatibility.
- Validation/browser: `V-FRONTEND`; Symbol Detail 1440/390 keyboard/pointer screenshots.
- Success/blocker: `P3_MP32_COMPLETE`; `P3_MP32_BLOCKED_BY_SYMBOL_DIALOG_REGRESSION`.

### P3-MP33 — All Markets migration

- Evidence/result: migrate All Markets and implement exact market trigger return focus.
- Lease: `web/src/features/dashboard/modals/AllMarketsModal.tsx`; new `AllMarketsModal.test.tsx`; `web/src/pages/DashboardPage.tsx`; `DashboardPage.test.tsx` only for exact controller focus identity.
- Forbidden: Symbol/Anomaly modal modules; semantic vocabulary; routes/CSS/ticker.
- Dependencies/group: MP31 and MP31A; `D1` parallel with MP32 and MP34.
- Branch/commit: `p3/mp33-all-markets-dialog`; `refactor(ui): migrate all markets to dialog`.
- Focused tests: exact trigger return, selected market activation, desktop/mobile focus visibility.
- Validation/browser: `V-FRONTEND`; All Markets 1440/390 pointer/keyboard screenshots.
- Success/blocker: `P3_MP33_COMPLETE`; `P3_MP33_BLOCKED_BY_RETURN_FOCUS`.

### P3-MP34 — All Anomalies and Anomaly Detail migration

- Evidence/result: migrate both anomaly overlays while preserving UUID identity, Back and exact row/card focus.
- Lease: `web/src/features/dashboard/modals/AnomalyModals.tsx`; new `AnomalyModals.test.tsx`.
- Forbidden: Dashboard controller except existing props; Symbol/All Markets modules; semantics; routes/CSS/ticker.
- Dependencies/group: MP31 and MP31A; `D1` parallel with MP32 and MP33.
- Branch/commit: `p3/mp34-anomaly-dialogs`; `refactor(ui): migrate anomaly dialogs`.
- Focused tests: All Anomalies → exact detail → Back, UUID replacement, visible responsive focus, stale close.
- Validation/browser: `V-FRONTEND`; Demo/Live, BTC/ETH, 1440/390 anomaly flows; eight screenshots.
- Success/blocker: `P3_MP34_COMPLETE`; `P3_MP34_BLOCKED_BY_UUID_OR_BACK_REGRESSION`.

### P3-MP35 — integrated dialog validation and legacy-shell removal

- Evidence/result: execute complete keyboard/focus matrix, add All Markets to smoke matrix, delete legacy shell after zero-import proof.
- Lease: `web/src/pages/DashboardPage.tsx`; `DashboardPage.test.tsx`; `DashboardPage.popup.test.tsx`; `web/src/test/uiSmokeMatrix.ts`; `uiSmokeMatrix.test.ts`; all post-decomposition modal test files; delete `web/src/features/dashboard/modals/LegacyDashboardTableModal.tsx`.
- Forbidden: semantic/routing/performance changes; production visual redesign; CSS/ticker.
- Dependencies/group: MP32–MP34; `D2`, exclusive integration.
- Branch/commit: `p3/mp35-dialog-integration`; `test(ui): validate integrated dialog behavior`.
- Focused tests: full declarative and executed dialog matrix, zero legacy imports.
- Validation/browser: `V-FRONTEND`; complete modal lifecycle at 1440/390, Demo/Live, BTC/ETH; screenshots for every modal and return path.
- Success/blocker: `P3_MP35_COMPLETE`; `P3_MP35_BLOCKED_BY_DIALOG_MATRIX`.

### P3-MP36 — explicit 404

- Evidence/result: add wildcard user-facing 404 while preserving `/symbols/:symbol` and `/anomalies` redirects.
- Lease: `web/src/app/router.tsx`; `router.test.tsx`; new `web/src/pages/NotFoundPage.tsx`; new `NotFoundPage.test.tsx`.
- Forbidden: compatibility redirect targets; modal state; Dashboard presentation; backend; CSS/ticker.
- Dependencies/group: MP35; `R1`, may run in parallel with MP37B only.
- Branch/commit: `p3/mp36-not-found-route`; `feat(ui): add explicit not found route`.
- Focused tests: wildcard, `/`, `/dashboard`, both compatibility redirects, query strings, replacement navigation.
- Validation/browser: `V-FRONTEND`; unknown desktop/mobile screenshots plus redirect verification.
- Success/blocker: `P3_MP36_COMPLETE`; `P3_MP36_BLOCKED_BY_ROUTE_COMPATIBILITY`.

### P3-MP37 → P3-MP37A — Dashboard/render containment

- Evidence/result: add recoverable Dashboard/render boundary distinct from 404 and query errors.
- Lease: post-MP36 `web/src/app/router.tsx`; `router.test.tsx`; `web/src/app/ConsoleLayout.tsx`; `ConsoleLayout.test.tsx`; new `web/src/shared/components/DashboardErrorBoundary.tsx`; new `DashboardErrorBoundary.test.tsx`.
- Forbidden: modal-local boundary; query-state copy; compatibility redirects; modal modules; CSS/ticker.
- Dependencies/group: MP36; `R2`, exclusive router owner.
- Branch/commit: `p3/mp37a-dashboard-error-boundary`; `feat(ui): contain dashboard render failures`.
- Focused tests: thrown render error, reset/retry, 404 distinction, query-error distinction, route preservation.
- Validation/browser: `V-FRONTEND`; desktop/mobile failure and recovery screenshots.
- Success/blocker: `P3_MP37A_COMPLETE`; `P3_MP37A_BLOCKED_BY_ROUTER_CONFLICT`.

### P3-MP37 → P3-MP37B — modal-local containment

- Evidence/result: boundary resets by modal type, mode, symbol and UUID without closing or corrupting unrelated Dashboard state.
- Lease against accepted post-MP35 tree: new `web/src/features/dashboard/modals/ModalErrorBoundary.tsx`; new `ModalErrorBoundary.test.tsx`; `SymbolDetailModal.tsx`; `SymbolDetailModal.test.tsx`; `AllMarketsModal.tsx`; `AllMarketsModal.test.tsx`; `AnomalyModals.tsx`; `AnomalyModals.test.tsx`; `web/src/pages/DashboardPage.tsx`; `DashboardPage.test.tsx` only for reset keys.
- Forbidden: router; 404; shared query errors; semantic copy; CSS/ticker.
- Dependencies/group: MP35; `R1`, may run in parallel with MP36 because leases are disjoint.
- Branch/commit: `p3/mp37b-modal-error-boundary`; `feat(ui): contain modal render failures`.
- Focused tests: each modal failure, identity-key reset, Back/Close/focus return, no stale error across mode/symbol/UUID.
- Validation/browser: `V-FRONTEND`; representative Symbol and Anomaly modal failure/recovery at both widths.
- Success/blocker: `P3_MP37B_COMPLETE`; `P3_MP37B_BLOCKED_BY_MODAL_IDENTITY`.

### P3-MP38 — measured modal-feature lazy loading

- Evidence/result: controlled experiment only; create a real async edge for accepted post-MP35 modal features, never route-page split.
- Lease: post-MP35 `web/src/pages/DashboardPage.tsx`; `DashboardPage.test.tsx`; new `web/src/features/dashboard/modals/lazyDashboardModals.tsx`; new `lazyDashboardModals.test.tsx`; existing modal modules only for default/named export compatibility, not extraction.
- Forbidden: router page splitting; package/lockfiles; budget changes; feature extraction; semantic changes; ticker.
- Dependencies/group: MP37A and MP37B; `R3`, exclusive measurement experiment.
- Branch/commit: `p3/mp38-lazy-modal-features`; `perf(ui): lazy load dashboard modal features`.
- Focused tests: real dynamic import edge, cold open identity, no eager modal import, mode/symbol/UUID correctness.
- Validation: `V-MEASUREMENT` plus `V-FRONTEND`.
- Browser/screenshots: cold first-open spinner/success for Symbol Detail and Anomaly Detail at 1440/390; no stale content or console errors.
- Acceptance threshold: initial JS below 387,239 bytes, total/largest budgets pass, real async edge emitted.
- Success/blocker: `P3_MP38_COMPLETE`; `P3_MP38_BLOCKED_BY_NO_MEASURED_BENEFIT`.

### P3-MP39 — Recharts-heavy chunk extraction

- Evidence/result: Recharts is already removed and native SVG accepted.
- Lease/branch/commit: `NONE`; implementation forbidden.
- Forbidden: adding Recharts or recreating a chart-library split.
- Dependencies/group: permanent accepted implementation.
- Tests/validation: Timeline native-SVG tests and bundle check remain green.
- Browser/screenshots: no new evidence required.
- Success/blocker: `P3_MP39_SUPERSEDED_BY_ACCEPTED_IMPLEMENTATION`; `P3_MP39_BLOCKED_BY_RECHARTS_REGRESSION`.

### P3-MP40 — lazy fallback, conditional

- Evidence/result: exists only after accepted MP38; provide accessible loading and import-failure presentation for actual lazy modal boundary.
- Lease: new `web/src/shared/components/LazyFeatureBoundary.tsx`; new `LazyFeatureBoundary.test.tsx`; `web/src/features/dashboard/modals/lazyDashboardModals.tsx`; `lazyDashboardModals.test.tsx`; `web/src/pages/DashboardPage.test.tsx`.
- Forbidden: new lazy boundaries; router split; modal identity changes; budget changes; CSS/ticker.
- Dependencies/group: accepted MP38 only; `R4`, exclusive.
- Branch/commit: `p3/mp40-lazy-modal-fallback`; `feat(ui): add accessible modal loading fallback`.
- Focused tests: loading announcement, import rejection, retry, focus behavior, successful recovery.
- Validation/browser: `V-FRONTEND` and `V-MEASUREMENT`; cold loading/failure/retry screenshots at 1440/390.
- Success/blocker: `P3_MP40_COMPLETE`; `P3_MP40_BLOCKED_BY_UNACCEPTED_MP38`.

### P3-MP41 — final bundle measurement

- Evidence/result: repeat measurement after accepted MP38/MP40 decision and all preceding work; no product write by default.
- Lease/branch/commit: `NONE` for normal completion; any corrective product change requires a separate narrow lease.
- Forbidden: budget increase; opportunistic splitting; dependency changes; ticker.
- Dependencies/group: MP40 if MP38 accepted, otherwise MP38 rejection record; `R5` checkpoint.
- Tests/validation: `V-MEASUREMENT` and full exact-head CI.
- Browser/screenshots: only if lazy behavior exists; otherwise none.
- Success/blocker: `P3_MP41_COMPLETE`; `P3_MP41_BLOCKED_BY_BUNDLE_BUDGET`.

### P3-MP42 — selector keyboard behavior

- Evidence/result: implement ArrowUp/Down, Home/End, filtered symbol navigation, activation and Escape return focus for mode and symbol selectors.
- Lease: `web/src/app/AppShell.tsx`; `AppShell.test.tsx`.
- Forbidden: System/mode semantic copy; ticker; routes; DashboardPage; CSS except existing selector classes.
- Dependencies/group: MP41; `H1` parallel with MP43.
- Branch/commit: `p3/mp42-selector-keyboard`; `feat(ui): complete selector keyboard navigation`.
- Focused tests: full keyboard model, disabled/empty/filter states, active descendant/focus, Escape return.
- Validation/browser: `V-FRONTEND`; keyboard-only Demo/Live and BTC/ETH selection at 1440/390; four screenshots.
- Success/blocker: `P3_MP42_COMPLETE`; `P3_MP42_BLOCKED_BY_SELECTOR_FOCUS`.

### P3-MP43 — reduced motion, non-ticker only

- Evidence/result: reduce chart/dialog/selector nonessential motion under user preference without altering ticker.
- Lease: `web/src/features/dashboard/TimelineChartRenderer.tsx`; `TimelineChartRenderer.test.tsx`; `web/src/shared/components/Dialog.tsx`; `Dialog.test.tsx`; `web/src/app/AppShell.tsx`; `AppShell.test.tsx`; `web/src/index.css` only for a named `prefers-reduced-motion` block that excludes all ticker selectors/keyframes.
- Forbidden: `web/src/app/GlobalMarketTicker.tsx`; `.sg-ticker-track`; ticker animation/keyframes/duration/order; route behavior; semantic copy.
- Dependencies/group: MP41 and MP31; `H1` parallel with MP42, with AppShell ownership serialized if both require the same accepted head.
- Branch/commit: `p3/mp43-reduced-motion`; `feat(ui): reduce non-ticker motion`.
- Focused tests: media-query behavior, dialog/chart/selector transitions, explicit ticker source unchanged.
- Validation/browser: `V-FRONTEND`; normal and reduced-motion recordings/screenshots at both widths; ticker equivalence proof.
- Success/blocker: `P3_MP43_COMPLETE`; `P3_MP43_BLOCKED_BY_TICKER_OWNERSHIP`.

### P3-MP44 — Timeline responsive regression

- Evidence/result: test-first verification after Wave 4/dialog/performance; no production fixes in this phase.
- Lease: `web/src/features/dashboard/TimelinePanel.test.tsx`; `TimelineChartRenderer.test.tsx`; new `TimelinePanel.responsive.test.tsx`; `web/src/test/uiSmokeMatrix.ts`; `uiSmokeMatrix.test.ts` only for Timeline scenarios.
- Forbidden: all production files.
- Dependencies/group: MP42 and MP43; `H2` parallel with MP45.
- Branch/commit: `p3/mp44-timeline-responsive-tests`; `test(ui): harden timeline responsive regression`.
- Focused tests: 1440/390 overflow, labels, chart bounds, Data Age/anomaly indicator, loading/error/empty/success.
- Validation/browser: `V-TEST-FIRST`; Demo/Live BTC/ETH screenshots for timeline states at both widths.
- Success/blocker: `P3_MP44_COMPLETE`; `P3_MP44_BLOCKED_BY_RESPONSIVE_DEFECT`.

### P3-MP45 — Health/anomaly responsive regression

- Evidence/result: test-first verification of preview and modal tables/cards; production fixes require separate recovery leases.
- Lease: `MarketHealthDesktopTable.test.tsx`; `MarketHealthMobileCards.test.tsx`; `RecentAnomaliesDesktopTable.test.tsx`; `RecentAnomaliesMobileCards.test.tsx`; new `web/src/features/dashboard/DashboardTables.responsive.test.tsx`; `web/src/test/uiSmokeMatrix.ts`; `uiSmokeMatrix.test.ts` only for health/anomaly scenarios.
- Forbidden: all production files.
- Dependencies/group: MP42 and MP43; `H2` parallel with MP44.
- Branch/commit: `p3/mp45-dashboard-responsive-tests`; `test(ui): harden health and anomaly responsiveness`.
- Focused tests: 1440/390 table/card visibility, overflow, semantic tooltips, modal rows, exact activation/focus.
- Validation/browser: `V-TEST-FIRST`; Demo/Live preview and modal screenshots at both widths.
- Success/blocker: `P3_MP45_COMPLETE`; `P3_MP45_BLOCKED_BY_RESPONSIVE_DEFECT`.

### P3-MP46 — final modal-only smoke

- Evidence/result: execute final combined matrix and document Phase 3 acceptance; normally no production lease.
- Lease: `web/src/test/uiSmokeMatrix.ts`; `uiSmokeMatrix.test.ts`; `web/src/pages/DashboardPage.popup.test.tsx`; `web/src/app/router.test.tsx`; test-only additions required to represent accepted 404, error-boundary, lazy and reduced-motion scenarios.
- Forbidden: production files; budget changes; ticker; new features.
- Dependencies/group: MP44 and MP45; `H3`, final exclusive checkpoint.
- Branch/commit: `p3/mp46-final-modal-smoke`; `test(ui): finalize modal-only browser smoke`.
- Focused tests: all smoke-matrix and route/modal integration tests.
- Validation: `V-TEST-FIRST`, full exact-head CI and final bundle measurement.
- Browser/screenshots: Demo/Live × BTC/ETH × 1440/390; Dashboard, Symbol Detail, All Markets, All Anomalies, Anomaly Detail, exact nested Back/focus, loading/error/empty/unavailable/success, rapid mode/symbol switches, explicit 404, Dashboard/modal boundaries, cold lazy success/failure if accepted, selector keyboard, normal/reduced motion, zero console errors. Preserve final screenshot set for every surface and viewport.
- Success/blocker: `P3_MP46_COMPLETE`; `P3_MP46_BLOCKED_BY_FINAL_SMOKE`.

## 8. Authorization state

Only `P3-MP18R` is authorized for product implementation.

P3-MP20R, both semantic bridges, P3-MP21–P3-MP46 and any new product Phase 4 remain blocked until their explicit dependencies and a separate immutable implementation contract are satisfied.
