# P3-MP11 Recovery Control

- WEB1 branch: `p3/mp11-market-health-desktop`
- WEB1 head: `3b5e3e0b5efd1ca5291c08cb0d7f9e3ab36ea596`
- WEB1 PR: `#33`
- WEB1 status: `REJECTED_AND_QUARANTINED`
- Reason: frontend CI failed because the authored focused source guard falsely matched status-capitalization `value.slice(1)`.

The production component behavior reviewed as aligned with the binding assigned-base presentation, but the execution head cannot be accepted with red frontend CI and skipped typecheck/lint/build/bundle gates.

Recovery policy:

1. Do not mutate, amend, rebase, reset, force-push, or add commits to the WEB1 branch.
2. Do not merge or reopen PR #33 as an acceptance candidate.
3. Use a new replacement branch and immutable WEB2 contract.
4. Recreate both authorized files from a clean accepted Phase 3 base.
5. Correct the focused ownership guard so it targets row transformations, not unrelated string operations.
6. Require full green frontend and global CI before draft PR publication is considered complete.
