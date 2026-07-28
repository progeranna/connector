# P3-MP10 Recovery Authorization

## Rejected immutable execution

- Contract: `P3-MP10-WEB1`
- Branch: `p3/mp10-timeline-panel`
- Head: `9bddc301d32c51bbb54dc5058d8d33320c144ff7`
- PR: `#36`
- Status: `REJECTED_AND_QUARANTINED`
- CI: `30367741374` — frontend failure; Rust/global success.
- Delivery report: absent.

The production component delegates to the accepted domain owner, but its focused test expects an incorrect price domain. For prices 100 and 102, the accepted formula yields `[99.796, 102.204]`; WEB1 expects `[99.84, 102.16]`.

Do not modify, amend, rebase, reset, force-push, merge, or add a corrective commit to the rejected branch.

## Authorized replacement

- Contract: `P3-MP10-WEB2`
- Replacement branch: `p3/mp10-timeline-panel-r1`
- Exact assigned base: `93a870010730c458417ccfff392cb97aff23d6c9`
- Required commit: `feat(ui): add timeline panel component`
- PR base: `refactor/dashboard-modules`

WEB2 must recreate the two-file extraction on the clean replacement branch, correct the domain expectation, fetch both committed files back from GitHub after publication, and require complete green frontend and Rust/global CI before opening the draft PR.
