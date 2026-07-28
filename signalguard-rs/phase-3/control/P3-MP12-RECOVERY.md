# P3-MP12 Recovery Control

- WEB1 branch: `p3/mp12-market-health-mobile`
- WEB1 head: `e2b13831be4bda00c4d6a554e583abfc877b82c9`
- WEB1 PR: `#35`
- WEB1 status: `REJECTED_AND_QUARANTINED`
- Reason: frontend CI failed because an authored focused test expected amber for `healthStatus: degraded` with `healthScore: 95`, contrary to the binding score-first tone precedence.

The production component behavior reviewed as aligned with the assigned-base presentation, but the execution head cannot be accepted with red frontend CI and skipped typecheck/lint/build/bundle gates.

Recovery policy:

1. Do not mutate, amend, rebase, reset, force-push, or add commits to the WEB1 branch.
2. Do not merge or reopen PR #35 as an acceptance candidate.
3. Use a new replacement branch and immutable WEB2 contract.
4. Recreate both authorized files from a clean accepted Phase 3 base.
5. Test the exact binding precedence: score `>= 80` wins before degraded-status handling.
6. Require full green frontend and global CI before draft PR publication is considered complete.
