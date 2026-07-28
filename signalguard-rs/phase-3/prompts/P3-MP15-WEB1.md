# P3-MP15-WEB1 — Dashboard compositor wiring

This is the immutable execution contract for SignalGuard RS Phase 3 microphase P3-MP15.

## Product identity

- Repository: `progeranna/signalguard-rs`
- Worker branch: `p3/mp15-dashboard-compositor`
- PR base: `refactor/dashboard-modules`
- Exact assigned base: `455a0bf15fbf7df2ecac9dbeb95e2a6dba7f8b73`
- Required commit: `refactor(ui): wire dashboard feature components`

## Binding companion files

Read and execute both files completely. They are part of this contract:

- `signalguard-rs/phase-3/prompts/P3-MP15-SCOPE.md`
- `signalguard-rs/phase-3/prompts/P3-MP15-VERIFICATION.md`

The Wave 2 closure record is also binding context:

- `signalguard-rs/phase-3/control/WAVE_2_CLOSURE.md`

## Mission

Replace the duplicated inline dashboard timeline, Market Health preview and Recent Anomalies preview presentation in `DashboardPage.tsx` with the five accepted integrated components.

This is compositor wiring only. Preserve all existing data/query ownership, selected-symbol behavior, modals, popup return contexts, routes, labels, tooltips, CSS semantics, responsive layout, preview behavior and user-visible output.

## Exact product lease

Modify only:

- `web/src/pages/DashboardPage.tsx`
- `web/src/pages/DashboardPage.test.tsx`

No other product path may change. Do not modify any accepted component or model.

## Mandatory execution

1. Confirm the branch equals the assigned base with divergence `0 0` before any write.
2. Read the current page, test and all accepted component/model APIs from the exact assigned base.
3. Implement the binding scope without visual or data-semantic changes.
4. Update focused compositor tests according to the binding verification file.
5. Run all required frontend and Rust/global gates.
6. Create exactly one normal product commit with the required message.
7. Push normally without history rewrite.
8. Fetch both committed files by exact final SHA and require exact remote blob equality.
9. Verify exact one-commit/two-path scope and preservation of accepted component/model/ticker blobs.
10. Open one draft PR to `refactor/dashboard-modules` only after remote integrity succeeds.
11. Require complete green current-phase PR merge-ref CI.
12. Publish the connector delivery report only after complete green CI.
13. Stop on any failed, skipped, cancelled or unavailable required gate without another product mutation.

## Prohibitions

- Do not merge.
- Do not modify or recreate the upper ticker.
- Do not change Demo/Live or symbol isolation.
- Do not remove a route, page, section, dialog, View-all action or symbol popup.
- Do not change visible copy, tooltips, classes or CSS semantics.
- Do not modify packages, config, API/query/resource modules, backend, OpenAPI, CI, Docker, deployment or scripts.
- Do not start P3-MP16.
- Do not claim `USER_UI_ACCEPTED`.

## Final response

Return the complete evidence required by `P3-MP15-VERIFICATION.md`, including final SHA, PR, exact diff, remote blobs, wiring matrix, tests, CI identity, preservation proof, blockers and the status `CODE_COMPLETE_AWAITING_INTEGRATION_AND_USER_UI_CHECK`.