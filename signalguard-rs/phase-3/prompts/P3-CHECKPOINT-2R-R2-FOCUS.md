# P3-CHECKPOINT-2R-R2 — All Markets Back focus recovery

Status: `P3_CHECKPOINT_2R_R2_FOCUS_IMPLEMENTATION_AUTHORIZED`

## Mode

Dedicated local Codex implementation worker.

Use the `$rust-development` skill.

This is a narrowly scoped product recovery micro-phase for the independently verified Checkpoint 2R rerun blocker. It is not a checkpoint rerun, integration worker, Bridge 01/02 worker, or Wave 4 worker.

## Authoritative blocker

Read completely before implementation:

`signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-BLOCKER/9cedbeb9c9e5e59ad634123a3b2d6217555a5c96.md`

Verified blocker publication:

- connector commit: `6c4b2e6858b7ce2d8a348f3129e0e1aab3413e4b`
- report blob: `8ee6e7441339d484c56afa9616f18b3463f2f659`
- terminal status: `P3_CHECKPOINT_2R_RERUN_BLOCKED`

The independently confirmed blocking behavior is:

```text
All Markets
→ Symbol Detail
→ exact Anomaly Detail
→ Back to Symbol Detail
→ Back to All Markets
```

The first Back correctly restores the exact visible anomaly trigger. The second Back restores the All Markets modal but focuses `Close` instead of the exact visible originating market row/card.

The defect is deterministic at both required viewports:

- desktop `1440×900`;
- mobile `390×844`.

Classification: MP18R focus-restoration regression.

## Independent source verification

At the accepted product head:

- `All Anomalies` already stores `focusAnomalyId`, passes an `initialFocusSelector`, and restores exact visible focus through the existing `findVisibleInitialFocus` browser-visible selection logic;
- `All Markets` currently stores only `{ type: "symbols" }` and provides no initial focus identity on remount;
- `DashboardTableModal` already accepts `initialFocusSelector` and otherwise focuses `Close`;
- both All Markets desktop rows and mobile cards already expose the same exact accessible identity: `aria-label="Open <SYMBOL> market detail"`.

Therefore no shared Dialog change, popup identity change, route change, resource change, CSS change, or added production helper file is authorized.

## Exact product base

Product repository:

`progeranna/signalguard-rs`

Target phase branch:

`refactor/dashboard-modules`

Immutable base commit:

`9cedbeb9c9e5e59ad634123a3b2d6217555a5c96`

Expected base tree:

`9bdfdcf331ef08cdeaf8f21a8ab66adee3092fe8`

Before any write, fetch over authenticated HTTPS and prove that `origin/refactor/dashboard-modules` still resolves exactly to the immutable base commit and tree. Any drift is a hard blocker.

## Local repository and assigned worktree

Local repository:

`/Users/anion/Desktop/work/git-signalguard-rs/signalguard-rs`

Create a NEW isolated worktree from the exact immutable base:

`/Users/anion/Desktop/work/git-signalguard-rs/worktrees/p3-checkpoint2r-r2-focus`

Assigned branch:

`p3/checkpoint2r-all-markets-back-focus`

The assigned branch must be created from exactly `9cedbeb9c9e5e59ad634123a3b2d6217555a5c96` and have no other product commits before implementation.

Do not reuse the detached Checkpoint 2R rerun validation worktree or any MP18R, MP20R, R1, or `p35-manual-qa` worktree.

## Exact writable lease

Exactly these two files are writable:

Production:

- `web/src/pages/DashboardPage.tsx`

Tests:

- `web/src/pages/DashboardPage.popup.test.tsx`

Every other product path is read-only.

Any discovered need to modify another product path is a hard blocker. Do not expand the lease yourself.

## Required implementation

Implement the smallest controller-local restoration of the exact All Markets trigger identity.

Required semantics:

1. Extend the local `DashboardModalState` `symbols` state only as much as needed to optionally preserve the originating symbol used for return focus.
2. When Symbol Detail has `returnContext === "symbols"`, `Back to all markets` must remount All Markets with the exact current `activePopupIdentity.symbol` as the requested return-focus identity.
3. `AllSymbolHealthModal` must accept that optional symbol focus identity and pass an `initialFocusSelector` into the existing `DashboardTableModal` mechanism.
4. Reuse the existing browser-visible `findVisibleInitialFocus` behavior. Do not duplicate or replace its visibility algorithm.
5. The selector must resolve the existing exact accessible market trigger identity shared by desktop row and mobile card. Do not add a second controller/resource identity system.
6. In a real browser, the visible responsive variant must receive focus. The hidden duplicate must never receive focus.
7. In jsdom, the existing deterministic no-layout fallback remains valid.
8. Opening All Markets directly from Dashboard must continue to have no requested market focus identity; its existing initial-focus behavior must remain unchanged.
9. The exact Symbol Detail identity remains `SymbolPopupIdentity`; do not add return-focus state to `SymbolPopupIdentity` or change `SymbolPopupReturnContext`.
10. The exact anomaly UUID controller remains unchanged.

The intended state shape may be equivalent to:

```ts
{ type: "symbols"; focusSymbol?: string }
```

but exact local naming is implementation-owned. Do not broaden beyond this behavior.

## Required tests

Add deterministic regression coverage in `DashboardPage.popup.test.tsx` for the complete failing nested flow:

```text
All Markets
→ exact market trigger
→ Symbol Detail
→ exact Anomaly Detail
→ Back to exact anomaly trigger in Symbol Detail
→ Back to exact originating market trigger in All Markets
```

Required assertions:

- desktop row variant receives focus when it is the visible variant;
- mobile card variant receives focus when it is the visible variant;
- the hidden responsive duplicate does not receive focus;
- another market row/card does not receive focus;
- nested anomaly Back still restores the exact visible UUID trigger before the second Back;
- the restored parent modal is still exactly `All markets`;
- `returnContext` remains `symbols`;
- pathname/modal routing semantics are not introduced or changed.

Use deterministic `getClientRects()` visibility stubbing consistent with the existing exact-anomaly focus tests. Do not weaken visibility assertions to DOM-order-only behavior.

Preserve all existing tests, including R1 reachability tests at Demo cardinalities 7 markets / 3 anomalies.

## KEEP_EXACT / forbidden changes

Do not change:

- `web/src/features/dashboard/symbolPopup.ts`;
- `SymbolPopupIdentity` fields or key semantics;
- `SymbolPopupReturnContext` values;
- exact anomaly UUID lookup semantics;
- Dashboard direct-symbol return behavior;
- All Anomalies → exact detail → Back behavior;
- exact visible anomaly focus restoration;
- Close/Escape/backdrop behavior: these close the entire workflow, not Back;
- body scroll-lock semantics;
- `/` and `/dashboard` visual route ownership;
- `/symbols/:symbol` and `/anomalies` replacement redirects;
- URL/modal-state synchronization prohibition;
- Demo/Live data isolation;
- preview limits or accepted Demo cardinality;
- R1 `View all` reachability behavior;
- market/anomaly resource identity, query keys, API or schemas;
- market adapters or presentation vocabulary;
- shared Dialog architecture;
- global CSS;
- ticker ownership/selectors/keyframes;
- package manifests or lockfiles;
- bundle budgets;
- backend/Rust source, migrations, or API artifacts.

Do not touch `web/index.html`, `web/public`, or add a favicon/static-asset change in this micro-phase. The browser-generated `/favicon.ico` 404 recorded by the blocker report is a separate pre-existing observation and is not causal to this MP18R focus recovery. It will be re-audited by the next full checkpoint and must not be opportunistically mixed into this product commit.

Do not begin Bridge 01, Bridge 02, P3-MP21…P3-MP30, or any later phase work.

## Required validation before commit

Before creating the product commit, run from `web/`:

```bash
npx vitest run --threads src/pages/DashboardPage.popup.test.tsx
npm run test:run
npm run typecheck
npm run lint
npm run build
npm run bundle:check
```

The full frontend suite must not silently lose test coverage. The accepted base currently has 44 test files and 612 tests; the recovery should increase, not reduce, the relevant regression coverage.

From repository root run:

```bash
cargo fmt --check
cargo check
cargo clippy --all-targets --all-features -- -D warnings
cargo test
```

All commands must pass.

Bundle budgets must remain exactly:

- initial max: `409600` bytes;
- largest max: `409600` bytes;
- total max: `414720` bytes.

Do not edit those budgets.

## Required targeted real-browser validation

Before commit, run the accepted production build in an isolated local preview using real backend Demo data. Do not mock or inject frontend data.

Reproduce and prove the corrected flow at both:

- desktop `1440×900`;
- mobile `390×844`.

At each viewport verify:

1. Demo contains the real accepted market/anomaly collections.
2. Market Health `View all` remains reachable.
3. All Markets opens.
4. Activate BTCUSDT from the visible All Markets row/card.
5. Open an exact BTCUSDT anomaly UUID from Symbol Detail.
6. `Back to symbol detail` restores the exact visible UUID row/card.
7. `Back to all markets` restores the exact visible `Open BTCUSDT market detail` row/card.
8. The hidden responsive market duplicate does not receive focus.
9. pathname remains `/` or `/dashboard` throughout.
10. Close/Escape/backdrop still close the complete workflow rather than acting as Back.
11. zero page errors and zero unhandled promise rejections occur.

The implementation worker is not authorized to reinterpret or weaken the focus requirement if the browser disagrees with the unit test.

Capture at least four deterministic screenshots outside the product repository, including desktop and mobile post-second-Back focus states. Record SHA-256 hashes in the implementation report.

## Product commit and push

After all required validation passes, create exactly one product commit on the assigned branch.

Required commit message:

`fix(ui): restore all-markets back focus`

The commit must have exactly one parent:

`9cedbeb9c9e5e59ad634123a3b2d6217555a5c96`

The effective product diff must contain exactly the two leased files and no others.

Push only:

`p3/checkpoint2r-all-markets-back-focus`

Do not push or rewrite `refactor/dashboard-modules`.

Do not open a pull request.

Do not merge.

## Connector implementation report

After the product branch is pushed and read back successfully, publish:

`signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R2-FOCUS/<PRODUCT_COMMIT_SHA>.md`

Required report contents:

- this contract path, connector commit and blob;
- immutable product base commit/tree;
- assigned branch and worktree;
- final product commit/tree/message/sole parent;
- exact changed paths and per-file stats;
- focused test result;
- full frontend suite file/test counts;
- typecheck/lint/build/bundle results and actual bundle byte counts;
- Rust/global gate results;
- exact desktop and mobile browser flow evidence;
- exact originating symbol and exact anomaly UUID used;
- focus target before and after each Back;
- hidden responsive duplicate non-focus evidence;
- screenshot filenames and SHA-256 hashes;
- final clean worktree status;
- confirmation that target phase branch remained unchanged;
- confirmation that no PR/merge was created;
- confirmation that Bridge 01/02 and Wave 4 did not begin.

Commit message:

`docs(phase-3): publish Checkpoint 2R R2 focus recovery report`

Do not modify `signalguard-rs/phase-3/control/CURRENT_EXECUTION.md` or `signalguard-rs/phase-3/control/STATUS.md` from the implementation worker.

A separate GitHub web review/integration step must verify the product commit before any merge is authorized.

## Terminal status

Return exactly:

`P3_CHECKPOINT_2R_R2_FOCUS_COMPLETE`

only after the product commit, push, read-back, all validation, and connector report publication succeed.

If any identity, scope, test, browser, evidence, or write-boundary requirement cannot be satisfied, make no out-of-scope repair and return:

`P3_CHECKPOINT_2R_R2_FOCUS_BLOCKED`

Do not begin any later work.