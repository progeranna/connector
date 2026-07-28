# P3-MP15-WEB1 Recovery Control

Status: `WEB2_AUTHORIZED`

## Superseded execution

- Execution: `P3-MP15-WEB1`
- Branch: `p3/mp15-dashboard-compositor`
- State: stopped before product mutation
- Final branch divergence: `0 0`
- Product commits: `0`
- PR: none
- Review: `signalguard-rs/phase-3/reviews/P3-MP15/WEB1-BLOCKED-REQUIRED-GATES-UNAVAILABLE.md`

Do not continue or publish from the WEB1 branch. Preserve it as immutable evidence of the blocked execution.

## Replacement execution

- Execution: `P3-MP15-WEB2`
- Branch: `p3/mp15-dashboard-compositor-r1`
- Exact assigned base: `455a0bf15fbf7df2ecac9dbeb95e2a6dba7f8b73`
- Initial divergence: `0 0`
- PR base: `refactor/dashboard-modules`
- Required product commit: `refactor(ui): wire dashboard feature components`

## Procedure correction

The replacement keeps the exact same product scope and acceptance criteria but corrects the unavailable-gate deadlock.

Before the product commit, the worker must execute every locally available check and complete deterministic source, type-shape, path-scope, UTF-8, whitespace, conflict-marker, blob, and ownership preflight. Dependency-backed commands that are genuinely unavailable in the isolated environment must be listed precisely and may not be claimed as passed.

A commit and draft PR may be published only if no available check failed and remote read-back/path integrity succeeds. Completion then requires the authoritative exact current-phase PR merge-ref GitHub Actions run to pass every frontend and Rust/global gate with no required red, cancelled, or skipped step.

Any actual failed check, remote-integrity failure, scope violation, or incomplete PR CI remains a hard immutable stop with no second product commit or history rewrite.
