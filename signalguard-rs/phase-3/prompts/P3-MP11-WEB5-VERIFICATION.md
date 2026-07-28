# P3-MP11-WEB5 — Binding Verification

Preserve the rows-specific transformation guard: it detects transformations of `rows` and permits `value.slice(1)`.

Preserve the valid type-only `MarketHealthPreviewRow` import assertion.

WEB4 failed because the remote forbidden-import expression used a hash character where the second quote delimiter class needed a double quote.

Before commit and again after fetching the committed test by exact final SHA, prove that the expression:

- detects a forbidden double-quoted module import;
- detects a forbidden single-quoted module import;
- ignores the allowed model import;
- contains no hash-based quote class.

Verification order:

1. Initial branch divergence is `0 0`.
2. Focused tests and repository TypeScript typecheck pass.
3. Full frontend tests, lint, build, and bundle budget pass.
4. Required Rust/global gates pass.
5. Exact diff contains only the two leased additions.
6. Exactly one normal commit is created and pushed without history rewrite.
7. Both files are fetched by final SHA as complete UTF-8 TSX.
8. Pre-publication and remote Git blob SHAs are equal.
9. Remote fixture and quote-integrity checks pass.
10. One draft PR targets `refactor/dashboard-modules`.
11. Current-phase PR CI is completely green for frontend and Rust/global jobs.
12. The connector delivery report is published only after complete green CI.

A red, unavailable, cancelled, or skipped required gate ends execution without another product mutation. The worker does not merge.
