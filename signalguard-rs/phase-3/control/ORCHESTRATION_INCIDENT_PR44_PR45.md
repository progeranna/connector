# Orchestration Incident — Accidental PR #44 and #45

Date: 2026-07-28

During P3-MP11-WEB4 branch preparation, the orchestrator twice invoked the pull-request creation action instead of the branch-creation action.

Accidental PRs:

- `#44` — created from quarantined branch `p3/mp11-market-health-desktop-r2`, then immediately closed unmerged.
- `#45` — created from the same quarantined branch, then immediately closed unmerged.

Both PRs point to existing rejected head `a10cc096d31dabe525dec321de9cd250951de47b`. Neither operation created a product commit, moved a branch ref, changed the phase branch, or merged code. Both PR titles and bodies were updated to identify them explicitly as closed orchestration errors.

The correct replacement branch was subsequently created using the explicit `create_branch` action:

- branch: `p3/mp11-market-health-desktop-r3`
- exact base: `025921919fa923abff1366bea01e9a502c088d22`

No product-tree remediation is required. The incident is retained for auditability.
