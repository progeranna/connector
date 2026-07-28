# P3-MP11 Integration Record

- Verdict: `ACCEPT`
- Accepted worker head: `f92e8978a5b19346acc447e9e0426a26a1e8043b`
- Worker branch: `p3/mp11-market-health-desktop-r4`
- PR: `#47`
- PR merge-ref CI: `30383418741`
- Tested merge ref: `a82a882d207a7e20578b05d6049b9741a186719f`
- Resulting Phase SHA: `455a0bf15fbf7df2ecac9dbeb95e2a6dba7f8b73`
- Merge method: guarded squash with expected head SHA

## Final Wave 2 tree proof

Both the tested PR merge ref and the resulting Phase commit use the same parent Phase tree `ae0759079d0845753c2bbcbd30fb13d24af85ad8` as their comparison base and differ from it only by the same two additions:

- `web/src/features/dashboard/MarketHealthDesktopTable.tsx`
- `web/src/features/dashboard/MarketHealthDesktopTable.test.tsx`

The component blob is `e57f8562f3b23a2a1f364f7709c49bf3f140b589` at both refs.
The test blob is `5a11aabc14bdcf1806b865348aa96a59609dc504` at both refs.

Therefore the integrated Wave 2 product tree is byte-equivalent to the fully green tested merge-ref tree, despite different commit ancestry caused by squash integration.

`DashboardPage.tsx`, the upper ticker, integrated MP10/MP12/MP13/MP14 files, routes, APIs, packages, backend, CI, Docker and scripts were not changed by P3-MP11.