# P3-MP15-WEB3 — Atomic Git-object compositor replacement

## Status

`WEB3_REPLACEMENT_AUTHORIZED`

P3-MP15-WEB1 and P3-MP15-WEB2 both stopped before product mutation because their execution environments could not materialize a local checkout. Neither execution produced a product commit, PR, CI run, or delivery report. Their branches are immutable and must not be continued.

## Contract identity

- Connector repository: `progeranna/connector`
- Contract path: `signalguard-rs/phase-3/prompts/P3-MP15-WEB3.md`
- Binding files at the same exact connector commit:
  - `signalguard-rs/phase-3/prompts/P3-MP15-SCOPE.md`
  - `signalguard-rs/phase-3/prompts/P3-MP15-VERIFICATION.md`
  - `signalguard-rs/phase-3/control/WAVE_2_CLOSURE.md`
  - `signalguard-rs/phase-3/control/PRODUCT_MERGE_POLICY.md`

Read this file and every binding file completely before product mutation.

## Product identity

- Product repository: `progeranna/signalguard-rs`
- Authorized branch: `p3/mp15-dashboard-compositor-r2`
- PR base: `refactor/dashboard-modules`
- Exact assigned base and parent: `455a0bf15fbf7df2ecac9dbeb95e2a6dba7f8b73`
- Required product commit message: `refactor(ui): wire dashboard feature components`

Before any write, prove the authorized branch is exactly:

```text
ahead 0
behind 0
commits 0
changed paths 0
```

## Superseded immutable executions

Do not modify, reuse, publish from, reset, rebase, force-push, merge, or open a PR from:

- `p3/mp15-dashboard-compositor` — WEB1, stopped without mutation;
- `p3/mp15-dashboard-compositor-r1` — WEB2, stopped without mutation.

## Exact path lease

Modify only:

- `web/src/pages/DashboardPage.tsx`
- `web/src/pages/DashboardPage.test.tsx`

No other product path may change. Do not add product files.

## Mission

Replace duplicated inline dashboard presentation with the five accepted components:

- `TimelinePanel`
- `MarketHealthDesktopTable`
- `MarketHealthMobileCards`
- `RecentAnomaliesDesktopTable`
- `RecentAnomaliesMobileCards`

Use the accepted preview owners:

- `buildMarketHealthPreview`
- `buildRecentAnomaliesPreview`

Preserve all existing query/controller ownership, selected-symbol persistence, Demo/Live and symbol isolation, routes, labels, messages, classes, tooltips, View-all behavior, dialogs, popup return contexts, full-collection workflows, responsive structure, and the upper ticker.

## Required timeline wiring

Keep `MarketTimelineShell` as query/controller boundary and preserve the existing symbol/mode-scoped query:

```ts
useMarketTimelineQuery(
  selectedMarket?.symbol ?? null,
  selectedUiMode,
  observed,
)
```

Render `TimelinePanel` with the exact selected market, raw timeline points, raw timeline anomalies, summary loading state, timeline loading state, formatted timeline error or `null`, existing refetch callback, and a deterministic finite `emptyAnchorMs` from existing query metadata.

Preferred anchor:

```ts
const emptyAnchorMs = Number.isFinite(timelineQuery.dataUpdatedAt)
  ? timelineQuery.dataUpdatedAt
  : 0;
```

Do not add `Date.now()`, zero-argument `new Date()`, timers, state, effects, randomness, or hidden fallback for this anchor.

## Required Market Health wiring

Build exactly one preview:

```ts
const preview = buildMarketHealthPreview(symbols);
```

Use:

- `preview.rows` for both accepted desktop and mobile components;
- `preview.hasMore` for existing View-all visibility;
- `preview.isEmpty` for existing empty state;
- the same existing symbol callback for both components.

Keep full raw `symbols` for dialogs, selection validation, popup/detail, and all full-collection workflows. Do not sort, slice, limit, remap, or deduplicate the accepted preview in the page.

## Required Recent Anomalies wiring

Build exactly one preview:

```ts
const preview = buildRecentAnomaliesPreview(anomalies);
```

Use:

- `preview.rows` for both accepted desktop and mobile components;
- `preview.hasMore` for existing View-all visibility;
- `preview.isEmpty` for existing empty state;
- the same existing symbol callback for both components.

Keep full raw `anomalies` for dialogs, popup/detail, and all full-collection workflows. Do not independently sort, slice, limit, remap, or deduplicate the preview.

## Dead inline presentation

Remove only code made genuinely dead by accepted components/models:

- direct dashboard Recharts imports and inline chart JSX;
- duplicate timeline normalization/domain/tooltip/marker helpers;
- inline Market Health desktop/mobile preview components;
- inline Recent Anomalies desktop/mobile preview components;
- duplicate preview constants and preview-only formatters no longer referenced.

Preserve every helper still needed by all-markets/all-anomalies dialogs, symbol popup/detail, full-dialog tables/cards, selected-symbol persistence, modal state, popup return contexts, error formatting, or full raw collections.

## Focused compositor tests

Update only `DashboardPage.test.tsx` and prove:

1. all five accepted components are imported and rendered;
2. both accepted preview builders are imported and used exactly once per preview owner;
3. timeline query remains symbol/mode scoped;
4. every `TimelinePanel` prop is wired correctly;
5. empty anchor derives from existing query metadata and no current-time ownership was added;
6. desktop/mobile Market Health receive the same `preview.rows`;
7. desktop/mobile Recent Anomalies receive the same `preview.rows`;
8. View-all uses `preview.hasMore`;
9. empty states use `preview.isEmpty`;
10. equal shrink-safe two-column dashboard grid remains;
11. section titles, subtitles and messages remain;
12. all-markets, all-anomalies and symbol-detail popup entry points remain;
13. full raw collections still feed full modal/detail workflows;
14. direct Recharts and inline dashboard timeline ownership are removed;
15. old inline preview component declarations are removed;
16. accepted implementations are not copied back into the page;
17. ticker, routes, Demo/Live, dialogs and popup behavior remain outside the diff.

Use narrow source/behavior assertions. Do not reject legitimate full-dialog or symbol-detail code that must remain.

## Mandatory transport method

Do not attempt `git clone`, `git fetch`, archive download, DNS repair, proxy discovery, GitHub CLI installation, or repeated Base64 transport experiments.

A local repository checkout is not required for this execution.

Use the connected GitHub Git Data operations atomically:

1. Read the complete immutable base bytes for both leased files with `GitHub.fetch_file`, using deterministic line windows if necessary.
2. Reassemble each file exactly once and verify its Git blob identity against the base blobs:
   - `DashboardPage.tsx`: `deb2eee919938d3b1807e353d309c046b08ba6f5`
   - `DashboardPage.test.tsx`: `a5db497f99fc2ebfdf08b46cb070176a95f22067`
3. Read accepted component/model signatures from the exact assigned base and verify their remote blob identities before use.
4. Construct both complete candidate UTF-8 files in local temporary memory/files.
5. Validate syntax/source contracts and compute pre-publication Git blob SHAs for both complete candidate files.
6. Obtain the exact assigned base commit tree SHA from commit metadata.
7. Call `GitHub.create_tree` once with that base tree and exactly two replacement blob entries:
   - mode `100644`;
   - type `blob`;
   - exact leased path;
   - complete candidate UTF-8 content.
8. Call `GitHub.create_commit` once:
   - tree: the new tree SHA;
   - sole parent: `455a0bf15fbf7df2ecac9dbeb95e2a6dba7f8b73`;
   - message: `refactor(ui): wire dashboard feature components`.
9. Before moving the branch, inspect the created commit and prove it has exactly one parent and exactly the two leased paths.
10. Call `GitHub.update_ref` once with `force: false` to fast-forward only `p3/mp15-dashboard-compositor-r2` to the created commit.

Forbidden publication methods:

- sequential Contents API file updates;
- two product commits;
- amend, reset, rebase, squash, force-push;
- partial/truncated file reconstruction;
- manual branch ref movement before exact commit inspection.

If the Git Data operations are unavailable or the complete base bytes cannot be reconstructed and blob-verified, stop without product mutation and report the exact missing operation. Do not repeat clone/network investigation.

## Pre-publication validation

Run every check available in the execution environment. At minimum, before creating the commit, prove:

- exact branch/base/divergence;
- exact two-path lease;
- complete UTF-8 content;
- TSX syntax/transpilation where available;
- accepted import/export and prop compatibility;
- all wiring/source contracts above;
- no conflict markers or trailing whitespace;
- no type bypasses;
- no direct Recharts ownership remains in the page;
- no duplicate inline accepted preview implementation remains;
- all modal/popup/controller entry points remain;
- before/after line counts;
- pre-publication Git blob SHA for both candidate files.

Dependency-backed local commands that genuinely require an unavailable checkout/dependency installation may be recorded as unavailable. Their absence alone does not block the single atomic candidate commit. Any failed available check is a hard stop.

## Remote integrity and PR publication

After the one atomic branch update:

1. Compare exact base to exact head and require:
   - ahead `1`;
   - behind `0`;
   - one commit;
   - exactly the two leased paths.
2. Fetch both files back by exact final product SHA.
3. Require exact pre-publication/remote Git blob equality and complete UTF-8 decoding.
4. Repeat all source/integrity checks against remote bytes.
5. Verify all accepted component/model/ticker blobs remain unchanged.
6. Open one draft PR:
   - head: `p3/mp15-dashboard-compositor-r2`;
   - base: `refactor/dashboard-modules`.

## Authoritative CI

Require the exact current-phase PR merge ref to pass every repository gate:

- frontend tests;
- TypeScript typecheck;
- frontend lint;
- production build;
- bundle budget;
- Rust formatting;
- generated API contract;
- OpenAPI validation;
- `cargo check`;
- clippy with warnings denied;
- Rust tests;
- replay target discovery;
- both Docker Compose validations;
- demo and smoke script syntax.

No required step may be red, cancelled, unavailable, or skipped.

If remote integrity or CI fails, stop without another product commit or history rewrite.

Only after complete green current-phase CI publish:

`signalguard-rs/phase-3/reports/P3-MP15/<FINAL_PRODUCT_HEAD_SHA>.md`

## Final response

Return:

- final product SHA and sole parent;
- draft PR number and URL;
- exact changed paths;
- pre-publication and remote blob equality;
- before/after page and test line counts;
- complete component wiring matrix;
- timeline query and empty-anchor proof;
- preview-builder/same-row wiring proof;
- View-all, empty, modal and popup preservation;
- dead inline presentation removed;
- all available pre-commit checks;
- precisely unavailable local commands;
- complete GitHub Actions run, jobs and tested merge-ref SHA;
- accepted component/model/ticker preservation;
- divergence;
- connector report path and commit;
- blockers and unavailable checks;
- exact status: `CODE_COMPLETE_AWAITING_INTEGRATION_AND_USER_UI_CHECK`.

Do not merge. Do not start P3-MP16. Do not claim `USER_UI_ACCEPTED`.