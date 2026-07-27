# P2-MP07 Independent Review

## Verdict

`REJECT — NARROW REPAIR REQUIRED`

Do not create or merge a product PR from this head.

## Reviewed identity

- Product repository: `progeranna/signalguard-rs`
- Product branch: `p2/mp07-market-availability`
- Assigned base: `856b58177d30772bc691ec870fe537c05aab3dba`
- Reviewed head: `9ed0d1e12fc385b19aabe0cbf32b0d4b726dd8fb`
- Commit message: `feat(api): expose market data availability`
- Commit count from assigned base: `1`
- Branch comparison: ahead `1`, behind `0`
- Product PR: not created
- Exact-head GitHub status: no checks were published for this SHA at review time

## Accepted implementation foundations

The candidate establishes several correct foundations:

- additive public `source = demo|live` fields;
- typed `availability = observed|configured|awaiting|unavailable`;
- backend-owned Live configured+registered catalog union;
- canonical deduplication and lexicographic ordering;
- one bulk `get_market_states` call for the complete Live catalog;
- no per-symbol Redis state read in the dashboard path;
- typed backend OpenAPI component schemas;
- source literals on successful Live state, health, symbols, and anomalies responses;
- explicit dashboard-symbol source and availability fields.

These foundations may be repaired in place. The candidate is not superseded.

## Blocking findings

### 1. Exact path lease was violated

The candidate changed two paths that were not authorized by the immutable P2-MP07 contract:

- `web/src/pages/DashboardPage.popup.test.tsx`;
- `web/src/test/marketFixtures.ts`.

The original test lease allowed dashboard-feature tests, AppShell header tests, and `web/src/pages/SymbolDetailPage.test.tsx`. It explicitly required the executor to stop before modifying any other path. This is a blocking process-integrity defect.

A repair contract may explicitly authorize these two already-used test-support paths; the first commit must not be rewritten.

### 2. Frontend OpenAPI compatibility gate does not cover the new contract

`web/src/features/dashboard/api-contract.test.ts` is unchanged from the assigned base.

Consequently, the reusable frontend contract validator does not verify:

- required `source` fields on every specified response;
- required `availability` fields on dashboard symbol, state, and health responses;
- exact `PublicDataMode` and `MarketAvailability` enum values;
- non-null/non-optional semantics;
- rejection of the previous `catalogAvailability` representation;
- mutation failures when any of those fields or enum values drift.

Backend artifact tests alone do not satisfy the cross-language compatibility requirement.

### 3. Header can still claim healthy observed data when no symbol is observed

`web/src/app/AppShell.tsx` was not changed.

Its header status still maps a healthy pipeline directly to `Data Healthy`, even when every dashboard symbol is `configured`, `awaiting`, or `unavailable`. This directly violates the required neutral header behavior for a catalog with zero observed symbols.

### 4. Dashboard still fetches and can render timeline data for non-observed symbols

`MarketTimelineShell` enables `useMarketTimelineQuery` solely from symbol/mode identity. It does not require `selectedSymbol.availability === "observed"`.

For a Live `configured`, `awaiting`, or `unavailable` symbol, historical PostgreSQL trades/anomalies may therefore render as a chart even though the authoritative current availability is non-observed. The contract explicitly forbids chart points and anomaly presentation for non-observed symbols.

The selected-market snapshot also continues to render metric rows for non-observed symbols, and its freshness value falls back to pipeline age. Pipeline age is not current market-state freshness for that symbol.

### 5. Route surface still renders metric/anomaly placeholders for non-observed symbols

A non-observed symbol is represented as a successful resource with empty anomalies and null state/health. `SymbolDetailPage` then still renders:

- the metric strip with placeholder values;
- `Recent anomalies` as `0`;
- generic `No recent anomalies for this market` copy.

The adapter also computes `anomalyCount` from the empty array, producing `0` for non-observed resources. The contract requires no fabricated price, rate, health score, chart point, or anomaly count for non-observed symbols; it requires the exact availability-specific empty-state copy instead.

The route source badge also evaluates missing view-model source as Demo (`undefined === "live" ? "Live" : "Demo"`), which can mislabel a Live unavailable/unknown state.

## Test and evidence assessment

The executor reported:

- Rust: `379 passed`, `3 ignored`;
- frontend: `281 passed`;
- OpenAPI write/check/validate success;
- fmt/check/clippy/typecheck/lint/build/bundle success;
- manual Docker smoke unavailable.

These are executor-reported local results. No exact-head PR CI exists yet, and the missing required assertions above explain why the green local suite did not establish contract completion.

## Repair authorization

Continue the same branch and worktree from immutable head:

`9ed0d1e12fc385b19aabe0cbf32b0d4b726dd8fb`

Apply exactly one additional normal repair commit under `P2-MP07-R1`. Do not amend, reset, rebase, squash, replace the branch, force-push, open a PR, or merge.
