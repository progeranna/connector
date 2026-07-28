# P3-MP10-WEB2 Recovery

Status: `WEB3_REPLACEMENT_AUTHORIZED`

## Rejected WEB2

- Branch: `p3/mp10-timeline-panel-r1`
- Head: `0ad34843578670d8b313af4f7f53853195c305a9`
- Assigned base: `93a870010730c458417ccfff392cb97aff23d6c9`
- Orchestrator-opened draft PR: `#41`, closed and unmerged
- Combined-tree CI: `30372209086`
- Rust/global: success
- Frontend tests: failure
- Typecheck, lint, build, and bundle budget: skipped
- Review: `signalguard-rs/phase-3/reviews/P3-MP10/0ad34843578670d8b313af4f7f53853195c305a9.md`

The WEB2 branch, head, PR, files, and report remain immutable evidence. They must not be modified, reopened, rebased, reset, amended, force-pushed, merged, or extended by another product commit.

## Authorized WEB3

- Product repository: `progeranna/signalguard-rs`
- Replacement branch: `p3/mp10-timeline-panel-r2`
- PR base: `refactor/dashboard-modules`
- Exact assigned base: `144ca95ae0338cfcf5ae00bd1cccd8317dbbc0b0`
- Required commit message: `feat(ui): add timeline panel component`
- Authorized paths:
  - `web/src/features/dashboard/TimelinePanel.tsx`
  - `web/src/features/dashboard/TimelinePanel.test.tsx`

## Diagnostic-first requirement

Before any product write, WEB3 must identify the exact failing test/assertion from:

- PR `#41`
- workflow run `30372209086`
- frontend job `90318715688`
- merge ref `cc19e0cf6c5179e25e2d35970694808c43331c1f`

Acceptable evidence includes complete Actions logs, GitHub UI check annotations, or faithful local reproduction against the exact merge tree.

WEB3 must not guess the failure from partial logs or silently assume the production component is correct. If the exact failure cannot be identified or reproduced, it must stop without product mutation and publish a connector diagnostic report.

After exact diagnosis, WEB3 may recreate the component/tests cleanly on the replacement branch, run all required gates, publish one normal product commit, open one draft PR, and publish one immutable delivery report only after complete green current-tree CI.
