# P3-MP11-WEB2 Recovery Control

## Rejected WEB2

- Branch: `p3/mp11-market-health-desktop-r1`
- Head: `e3230713fcc5256dd1d92651f9ba54bdb4ec1c8a`
- Exact assigned base: `93a870010730c458417ccfff392cb97aff23d6c9`
- PR: none
- Status: `REJECTED_AND_QUARANTINED`
- Reason: required remote read-back found a malformed committed test blob that differs from the locally hardened candidate. No complete green CI exists.

## Immutable recovery

1. Leave WEB1 and WEB2 branches and heads unchanged.
2. Do not add corrective commits, amend, reset, rebase, force-push, merge, or open a PR from either rejected branch.
3. Use replacement branch `p3/mp11-market-health-desktop-r2`.
4. Exact WEB3 assigned base: `144ca95ae0338cfcf5ae00bd1cccd8317dbbc0b0`.
5. Use immutable contract `signalguard-rs/phase-3/prompts/P3-MP11-WEB3.md`.
6. Require one normal product commit, exact two-path scope, remote blob equality, valid source-guard regular expressions, and complete green current-tree CI before a draft PR and delivery report.