# P3-MP11-WEB4 — Market Health Desktop Type-Safe Replacement

Status: `IMMUTABLE_WEB_WORKER_EXECUTION_CONTRACT`

## Identity

- Product repository: `progeranna/signalguard-rs`
- Connector repository: `progeranna/connector`
- Replacement branch: `p3/mp11-market-health-desktop-r3`
- PR base: `refactor/dashboard-modules`
- Exact assigned base SHA: `025921919fa923abff1366bea01e9a502c088d22`
- Required product commit: `feat(ui): add market health desktop table`
- Required draft PR title: `feat(ui): add market health desktop table`

## Immutable rejected executions

### WEB1

- branch: `p3/mp11-market-health-desktop`
- head: `3b5e3e0b5efd1ca5291c08cb0d7f9e3ab36ea596`
- PR: `#33`, closed and unmerged
- failure: overbroad source guard rejected harmless `value.slice(1)`

### WEB2

- branch: `p3/mp11-market-health-desktop-r1`
- head: `e3230713fcc5256dd1d92651f9ba54bdb4ec1c8a`
- PR: none
- failure: remote test blob contained malformed `[#']` quote classes and differed from hardened local bytes

### WEB3

- branch: `p3/mp11-market-health-desktop-r2`
- head: `a10cc096d31dabe525dec321de9cd250951de47b`
- PR: `#43`, closed and unmerged
- CI: `30372902126` (`#212`)
- merge ref: `d48e7e12171aaa3eb89fa9eb505fe34c3d63046a`
- frontend tests: success
- frontend typecheck: failure
- lint/build/bundle: skipped
- Rust/global: success
- exact defect: typed test case passes `healthStatus: "custom"`, which is outside accepted `healthy | degraded | unhealthy | null`
- review: `signalguard-rs/phase-3/reviews/P3-MP11/a10cc096d31dabe525dec321de9cd250951de47b.md`

Do not modify, reopen, amend, reset, rebase, merge, force-push, or add commits to any rejected branch. Accidental administrative PRs `#44` and `#45` are closed unmerged and are not execution sources.

## Goal

Create the standalone desktop Market Health table component over accepted readonly `MarketHealthPreviewRow` values, preserving the binding inline dashboard presentation without wiring `DashboardPage.tsx`.

## Authorized product paths

Add only:

1. `web/src/features/dashboard/MarketHealthDesktopTable.tsx`
2. `web/src/features/dashboard/MarketHealthDesktopTable.test.tsx`

No existing product file may change.

## Required API

Export:

```ts
export type MarketHealthDesktopTableProps = Readonly<{
  rows: readonly MarketHealthPreviewRow[];
  onOpenSymbolDetail: (symbol: string) => void;
}>;

export function MarketHealthDesktopTable(...)
```

Consume accepted `MarketHealthPreviewRow` through a type-only import. Do not accept raw dashboard summaries.

## Binding presentation and behavior

Preserve exactly:

- desktop-only wrapper hidden below `lg`;
- horizontal overflow and overscroll containment;
- `aria-label="Market health"`;
- fixed six-column table;
- widths: Market 18%, Health Score 22%, Last Price 16%, Spread 11%, Trades/min 14%, Status 19%;
- supplied row order and cardinality;
- React identity exactly `row.key`;
- focusable `role="button"` rows;
- exact accessible label `Open <SYMBOL> market detail`;
- click, Enter and Space callback behavior, with `preventDefault()` for keyboard activation;
- current symbol/View typography, classes, separators, hover and focus treatment;
- Health Score number, compact bar, minimum 4% width for non-null zero, and binding score-first tone precedence;
- current Price, Spread and Trades/min formatting, including zero and missing values;
- current observed status wording and configured/awaiting/unavailable wording;
- visually empty non-observed metric cells.

Do not sort, slice, limit, reverse, mutate, deduplicate, inspect preview metadata, synthesize metrics, coerce source/availability, or introduce Demo/Live fallback.

## Required regression hardening

### WEB1 collection guard

Target transformations of the `rows` collection specifically:

```ts
const rowTransformation =
  /\brows\s*\.\s*(?:sort|toSorted|slice|splice|reverse)\s*\(/;

expect(componentSource).not.toMatch(rowTransformation);
expect(rowTransformation.test("rows.slice(0, 7)")).toBe(true);
expect(rowTransformation.test("rows.toSorted(compareRows)")).toBe(true);
expect(rowTransformation.test("value.slice(1)")).toBe(false);
```

### WEB2 quote integrity

All quote classes must use:

```ts
["']
```

Never use:

```ts
[#']
```

The type-only import source assertion must match the actual double-quoted import.

### WEB3 type-safety regression

Every typed `healthStatus` fixture must be one of:

```text
healthy
degraded
unhealthy
null
```

Never use as `healthStatus`:

```text
custom
info
warning
critical
unknown
```

Test visible neutral/Unknown presentation using `healthStatus: null`.

Do not bypass typing through `as any`, `as unknown as`, `@ts-ignore`, `@ts-expect-error`, widened string casts, or untyped fixture helpers.

The complete focused test source must pass repository TypeScript typecheck.

## Score-tone precedence

Preserve:

1. healthy status or score >= 80 -> healthy/green;
2. otherwise degraded status or score >= 50 -> degraded/amber;
3. otherwise unhealthy status or score < 50 -> unhealthy/rose;
4. otherwise neutral.

Include the edge cases already required for the mobile counterpart, including degraded + 95 and unhealthy + 90 producing healthy score tone while status wording remains accepted.

## Verification and publication

1. Verify the replacement branch is exactly `0 0` from assigned base.
2. Work only on `p3/mp11-market-health-desktop-r3`.
3. Run focused tests and strict repository TypeScript validation before publication when available.
4. Create exactly one normal product commit.
5. Push normally without history rewriting.
6. Fetch both committed files from GitHub by exact final SHA.
7. Require exact equality with pre-publication Git blob identities.
8. Verify complete UTF-8/TSX content.
9. Verify valid `["']` classes and absence of `[#']`.
10. Verify no invalid health-status fixture or type bypass exists remotely.
11. Verify exact diff is one commit and only the two authorized additions.
12. Open one draft PR from `p3/mp11-market-health-desktop-r3` to `refactor/dashboard-modules`.
13. Require complete green current-phase GitHub Actions:
   - frontend tests;
   - typecheck;
   - lint;
   - build;
   - bundle budget;
   - Rust/global job.
14. If any gate is red or skipped, stop without further product mutation.
15. After complete green CI, publish:

`signalguard-rs/phase-3/reports/P3-MP11/<FINAL_PRODUCT_HEAD_SHA>.md`

## Forbidden scope

Do not modify or wire `DashboardPage.tsx`; do not modify integrated MP12/MP13/MP14 files, models, CSS, routes, API/query/resource files, package/configuration, backend, OpenAPI, CI, Docker, scripts, or upper ticker. Do not start P3-MP15. Do not merge.
