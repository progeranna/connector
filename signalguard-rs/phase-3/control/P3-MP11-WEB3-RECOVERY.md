# P3-MP11-WEB3 Recovery

Status: `WEB4_REQUIRED`

## Rejected execution

- Branch: `p3/mp11-market-health-desktop-r2`
- Head: `a10cc096d31dabe525dec321de9cd250951de47b`
- PR: `#43`, closed and unmerged
- CI: `30372902126` (`#212`)
- Frontend tests: success
- Frontend typecheck: failure
- Lint/build/bundle: skipped
- Rust/global: success
- Review: `signalguard-rs/phase-3/reviews/P3-MP11/a10cc096d31dabe525dec321de9cd250951de47b.md`

The rejected branch and head are immutable evidence. Do not modify, reopen, amend, reset, rebase, force-push, merge, or add a corrective commit.

## Root cause

The typed focused-test table includes `healthStatus: "custom"` through `Partial<MarketHealthPreviewRow>`. The accepted health-status union is only `healthy | degraded | unhealthy | null`. Runtime tests pass, but repository typecheck rejects the invalid fixture.

## Recovery identity

- New branch: `p3/mp11-market-health-desktop-r3`
- Exact base: current accepted Phase SHA `025921919fa923abff1366bea01e9a502c088d22`
- Required commit: `feat(ui): add market health desktop table`
- Required PR base: `refactor/dashboard-modules`
- Allowed product paths: the two P3-MP11 component/test additions only

WEB4 must preserve the accepted production presentation and all prior regression hardening while replacing the impossible custom-status fixture with accepted typed cases. Neutral/Unknown presentation must be tested with `healthStatus: null`.
