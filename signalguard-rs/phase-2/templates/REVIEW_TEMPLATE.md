# <MP-ID> Orchestrator Review

## Reviewed identity

- Mini-phase: `<MP-ID>`
- Contract connector commit: `<CONNECTOR-CONTRACT-SHA>`
- Product repository: `progeranna/signalguard-rs`
- Expected product base SHA: `<EXPECTED-BASE-SHA>`
- Product branch: `<PRODUCT-BRANCH>`
- Reviewed product head SHA: `<PRODUCT-HEAD-SHA>`
- Product PR: `<PR-URL>`
- Worker report: `<CONNECTOR-REPORT-PATH>`
- Worker report commit: `<CONNECTOR-REPORT-SHA>`

## Decision

Choose exactly one:

- `ACCEPT`
- `ACCEPT_WITH_NOTES`
- `REJECT`

Decision rationale:

`<concise but complete rationale>`

## Identity and Git validation

| Check | Result | Evidence |
|---|---|---|
| Contract commit is exact and immutable | `<PASS/FAIL>` | `<evidence>` |
| Product base SHA is exact | `<PASS/FAIL>` | `<evidence>` |
| Task branch is correct | `<PASS/FAIL>` | `<evidence>` |
| PR base is `refactor/data-boundaries` | `<PASS/FAIL>` | `<evidence>` |
| PR head equals reviewed SHA | `<PASS/FAIL>` | `<evidence>` |
| No unreported later commit | `<PASS/FAIL>` | `<evidence>` |

## Changed-path validation

- Expected paths: `<list>`
- Actual paths: `<list>`
- Unexpected paths: `<NONE or list>`
- Scope verdict: `<PASS/FAIL>`

## Patch review

Summarize the full reviewed patch and the key implementation choices.

## Contract invariant matrix

| Required invariant | Result | Independent evidence |
|---|---|---|
| `<invariant>` | `<PASS/FAIL/NOT_PROVEN>` | `<evidence>` |

## Test and gate validation

| Gate | Worker claim | Independent validation | Result |
|---|---|---|---|
| `<gate>` | `<claim>` | `<CI/log/inspection>` | `<PASS/FAIL/PENDING/NOT_RUN>` |

## Compatibility and regression review

Record effects on:

- public API/contracts;
- routes and popup behavior;
- Demo/Live isolation;
- symbol isolation;
- query/fetch policy;
- Redis key and serialization compatibility;
- startup/reset semantics;
- dependencies and lockfiles;
- repository hygiene.

Use `Not applicable` where appropriate.

## Defects and notes

### Blocking defects

- `<NONE or defect>`

### Non-blocking notes

- `<NONE or note>`

`ACCEPT_WITH_NOTES` must not contain an unresolved correctness, isolation, atomicity, security, or data-integrity defect.

## Integration authorization

- Authorized for integration: `<YES/NO>`
- Exact authorized product head SHA: `<SHA or NONE>`
- Required integration method: `<squash merge / other>`
- Required integration order: `<position>`
- Recheck PR head before integration: `YES`

## Repair instructions

Complete only for `REJECT`:

- Repair contract path: `<path>`
- Required fixes: `<list>`
- Branch to continue: `<branch>`
- New scope restrictions: `<list or NONE>`

## Final declaration

This review applies only to the exact product head SHA listed above. Any later product commit requires a new review.
