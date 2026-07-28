# P3-MP11-WEB4 Recovery

Rejected execution:

- Branch: `p3/mp11-market-health-desktop-r3`
- Head: `76ab834f65d2f792bdb24ae39f2f726c49e556fe`
- Assigned base: `025921919fa923abff1366bea01e9a502c088d22`
- PR: none
- CI: none
- Verdict: `REJECT`

Mandatory remote read-back found a malformed negated quote class in the committed forbidden-import test expression. The class incorrectly excluded a hash character instead of a double quote. The rejected branch must remain immutable.

Authorize P3-MP11-WEB5:

- Branch: `p3/mp11-market-health-desktop-r4`
- Exact base: `025921919fa923abff1366bea01e9a502c088d22`
- Required commit: `feat(ui): add market health desktop table`
- Exact lease:
  - `web/src/features/dashboard/MarketHealthDesktopTable.tsx`
  - `web/src/features/dashboard/MarketHealthDesktopTable.test.tsx`

WEB5 must preserve all prior semantic and type-safety corrections and add executable regression checks proving that the forbidden-import expression handles both single- and double-quoted imports and contains no malformed hash-based character class.
