# P3-MP09 Recovery Control

Current state: `WEB2_REPLACEMENT_AUTHORIZED`

## Rejected execution

- Contract: `P3-MP09-WEB1`
- Branch: `p3/mp09-dashboard-resource-state`
- Head: `b7dfebd10a8ec90b0e4f9a957b8368f6a4f06ee9`
- Status: `REJECTED_AND_QUARANTINED`
- Reason: corrupted committed remote test blob
- PR: none
- Merge authorization: none

The rejected branch/head must remain immutable and must not be reset, rewritten, reused, opened as a PR, or merged.

## Replacement execution

- Contract: `signalguard-rs/phase-3/prompts/P3-MP09-WEB2.md`
- Contract commit: `0cbbcaf2d292690fa0f7754c8b12fc847d1fc39a`
- Replacement branch: `p3/mp09-dashboard-resource-state-r1`
- Required PR base: `refactor/dashboard-modules`
- Exact assigned base: `3587ec9b70b677121aa796467d5bb359ffb4d174`
- Required commit: `feat(ui): extract dashboard resource states`
- Status: `WEB_WORKER_EXECUTION_AUTHORIZED`

The replacement worker must validate both remote committed blobs after publication and require exact-head full CI before opening a draft PR.