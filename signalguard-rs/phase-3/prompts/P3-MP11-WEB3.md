# P3-MP11-WEB3 — Market Health Desktop Table Replacement

Status: `IMMUTABLE_WEB_WORKER_REPLACEMENT_CONTRACT`

## Identity

- Product repository: `progeranna/signalguard-rs`
- Connector repository: `progeranna/connector`
- Replacement branch: `p3/mp11-market-health-desktop-r2`
- PR base: `refactor/dashboard-modules`
- Exact assigned base SHA: `144ca95ae0338cfcf5ae00bd1cccd8317dbbc0b0`
- Required product commit message: `feat(ui): add market health desktop table`
- Required draft PR title: `feat(ui): add market health desktop table`

## Quarantined executions

### WEB1

- Branch: `p3/mp11-market-health-desktop`
- Head: `3b5e3e0b5efd1ca5291c08cb0d7f9e3ab36ea596`
- Closed PR: `#33`
- Failure: overbroad source guard falsely rejected harmless `value.slice(1)`.

### WEB2

- Branch: `p3/mp11-market-health-desktop-r1`
- Head: `e3230713fcc5256dd1d92651f9ba54bdb4ec1c8a`
- PR: none
- Failure: remote test blob differed from the locally hardened candidate and contained malformed `[#']` quote classes in source-guard regular expressions.

Do not modify, reopen, repair, amend, reset, rebase, force-push, merge, or add commits to either quarantined branch.

## Goal and authorized paths

Create the desktop-only Market Health preview table and focused tests. Add only:

1. `web/src/features/dashboard/MarketHealthDesktopTable.tsx`
2. `web/src/features/dashboard/MarketHealthDesktopTable.test.tsx`

No existing product file may change.

Export:

```ts
export type MarketHealthDesktopTableProps = Readonly<{
  rows: readonly MarketHealthPreviewRow[];
  onOpenSymbolDetail: (symbol: string) => void;
}>;

export function MarketHealthDesktopTable(...)
```

Consume accepted `MarketHealthPreviewRow` values through a type-only import. Do not accept raw summaries.

## Binding presentation

Use the existing desktop Market Health preview table in `DashboardPage.tsx` at the exact assigned base as the source of truth. Preserve exactly:

- desktop-only wrapper hidden below `lg` and shown at `lg`;
- horizontal overflow, overscroll containment, and border structure;
- `aria-label="Market health"`;
- fixed six-column table with current widths and order: Market, Health Score, Last Price, Spread, Trades/min, Status;
- supplied row order and accepted `row.key` React identity;
- focusable button-role rows;
- exact accessible label `Open <SYMBOL> market detail`;
- click, Enter, and Space activation with `preventDefault()` for keyboard activation;
- current symbol typography and conditional `View` copy;
- current Health Score number, bar, minimum non-null width, and score/status tone precedence;
- current price, spread, compact trades/min, and numeric-zero formatting;
- current observed/configured/awaiting/unavailable wording, empty metric cells, classes, hover, focus, and separators.

Do not sort, reorder, slice, limit, mutate, deduplicate, synthesize metrics, inspect preview metadata, coerce source/availability, or introduce Demo/Live fallback.

Do not add a section header, mobile markup, loading/empty shell, view-all control, modal, tooltip, icon, source badge, Wave 4 vocabulary, query/API/router ownership, or caller wiring.

## Required tests

Use explicit DOM assertions covering:

1. desktop wrapper, table label, columns, widths, and classes;
2. supplied order and accepted `row.key` identity;
3. click, Enter, Space, exact labels, callback symbols, and default prevention;
4. observed score/status presentation and exact tone precedence;
5. price, spread, trades/min, null, missing, zero, and negative formatting;
6. configured, awaiting, unavailable, and observed-fallback states;
7. no ordering, limiting, mutation, fallback, shell, modal, mobile, tooltip, Wave 4, query, router, or network ownership.

## WEB1 regression prevention

Ownership guards must target transformations of the `rows` collection specifically:

```ts
const rowTransformation =
  /\brows\s*\.\s*(?:sort|toSorted|slice|splice|reverse)\s*\(/;

expect(componentSource).not.toMatch(rowTransformation);
expect(rowTransformation.test("rows.slice(0, 7)")).toBe(true);
expect(rowTransformation.test("rows.toSorted(compareRows)")).toBe(true);
expect(rowTransformation.test("value.slice(1)")).toBe(false);
```

Do not use a whole-source expression that rejects unrelated string operations such as `value.slice(1)`.

## WEB2 byte-integrity regression prevention

Every quote-character class in source-guard regular expressions must support both double and single quotes using an exact valid form such as:

```ts
["']
```

Never use:

```ts
[#']
```

The import assertion must match the actual double-quoted type-only import. For example:

```ts
expect(componentSource).toMatch(
  /import\s+type\s+\{\s*MarketHealthPreviewRow\s*\}\s+from\s+["']\.\/marketHealthPreviewModel["'];/,
);
```

After publication, fetch both files back from GitHub using the exact final SHA and verify:

- remote blob SHAs equal the pre-publication Git object hashes;
- both files decode completely as UTF-8/TSX;
- the remote test contains `["']` and contains no `[#']`;
- the remote import assertion matches the actual component import;
- the collection-specific regression cases are present exactly.

## Forbidden scope

Do not modify `DashboardPage.tsx`, integrated MP13/MP14 files, accepted models/order owners, mobile Market Health lease, modals, CSS, routes/pages, API/query/resource/adapter/identity files, fixtures, Tooltip, packages/configuration, backend, OpenAPI, CI, Docker, scripts, deployment, or the upper ticker. Do not start P3-MP15.

## Execution and hardening

1. Verify `p3/mp11-market-health-desktop-r2` equals exact assigned base `144ca95ae0338cfcf5ae00bd1cccd8317dbbc0b0` with divergence `0 0`.
2. Work only on the replacement branch.
3. Run focused tests and strict TypeScript/TSX validation for both new files before commit when available.
4. Create exactly one normal product commit and push normally.
5. Fetch both committed files back from GitHub by exact final SHA and perform the byte-integrity checks above.
6. Verify exact base-to-head diff contains only the two authorized additions.
7. Open one draft PR only after remote read-back succeeds:
   - head: `p3/mp11-market-health-desktop-r2`
   - base: `refactor/dashboard-modules`
8. Require complete green exact-current merge-tree GitHub Actions:
   - frontend tests;
   - typecheck;
   - lint;
   - build;
   - bundle budget;
   - Rust/global job.
9. On corruption or any red/skipped required gate, stop without further product-branch mutation and do not claim completion.
10. After complete green CI, publish:

`signalguard-rs/phase-3/reports/P3-MP11/<FINAL_PRODUCT_HEAD_SHA>.md`

The report must include quarantined WEB1/WEB2 evidence, exact API/presentation matrix, collection-specific guards, quote-class integrity evidence, remote blob SHAs/equality, complete gates, exact paths, integrated MP13/MP14 preservation, ticker proof, unavailable checks, and divergence.

Do not merge, amend, reset, rebase, squash, or force-push.