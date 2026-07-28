# P3-MP12-WEB2 Recovery Control

## Rejected WEB2

- Branch: `p3/mp12-market-health-mobile-r1`
- Head: `ae19b372943f890c9f0ec18bc85143e366dadef1`
- PR: `#39` — closed, unmerged
- CI: `30369207184` — failure
- Frontend tests: passed
- Frontend typecheck: failed
- Lint/build/bundle gates: skipped
- Review: `signalguard-rs/phase-3/reviews/P3-MP12/ae19b372943f890c9f0ec18bc85143e366dadef1.md`
- Report: `signalguard-rs/phase-3/reports/P3-MP12/ae19b372943f890c9f0ec18bc85143e366dadef1.md`

## Confirmed cause

The committed focused test supplies `healthStatus: "info"`. The accepted market-health status type permits only `healthy`, `degraded`, `unhealthy`, or `null`. This is a test-fixture type error, not an authorized runtime state.

## Quarantine rules

1. Leave WEB2 branch and head immutable.
2. Do not amend, reset, rebase, force-push, reopen PR #39, merge, or add another product commit.
3. Do not copy the invalid `healthStatus: "info"` fixture.
4. Preserve the corrected score-first tone precedence from WEB2.

## Authorized recovery

- Replacement contract: `P3-MP12-WEB3`
- Replacement branch: `p3/mp12-market-health-mobile-r2`
- Exact assigned base: `93a870010730c458417ccfff392cb97aff23d6c9`
- Initial divergence: `0 0`
- Required product commit: `feat(ui): add market health mobile cards`

WEB3 is the only authorized P3-MP12 execution source after this record.
