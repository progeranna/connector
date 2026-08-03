# Phase 4 — Modal anomaly explorer planning and inventory

Status: `P4_PLANNING_INVENTORY_AUTHORIZED`

## 1. Purpose

Produce an exact-source inventory and a reviewed implementation plan for the next SignalGuard RS phase against the integrated Phase 3.6 product state.

This is a planning-only control-plane task. It does not authorize product implementation, product branch creation, product commits, product pushes, pull requests, merges, migrations, package changes, or API changes.

The output must replace the obsolete standalone-page conception of Phase 4 with a Dashboard-owned modal anomaly explorer that preserves the product-owner navigation decision integrated in Phase 3.6.

## 2. Exact authoritative product identity

Product repository:

`progeranna/signalguard-rs`

Integrated phase branch:

`refactor/dashboard-modules`

Exact immutable planning base:

`ba31a348dc5055935c45f6be81073688caedd925`

Exact base tree:

`f629b6ea4339c92d03223c3bd8024cd4cb4571da`

Old closed Phase 3.5 base:

`09e0cbaa8cafd7c0523bb4ed539c01b2f7ad0b27`

Phase 3.6 worker commit:

`41f7f6fa9779e282bfff5714c26965b833f69741`

Phase 3.6 PR:

`#68`

Phase 3.6 control status:

`P3_6_MODAL_ONLY_CORRECTION_INTEGRATED_PHASE_4_NOT_AUTHORIZED`

Before inventory, verify that `refactor/dashboard-modules` still resolves exactly to the immutable planning base and that its tree matches exactly. Any drift is a blocker; do not silently inventory another revision.

## 3. Binding product-owner navigation model

The following rules supersede every historical plan, local control document, architecture note, test strategy, or repository statement that requires standalone visual symbol or anomaly pages:

1. `/` and `/dashboard` are the only user-facing visual console pages.
2. `/symbols/:symbol` is compatibility-only and replacement-redirects to `/dashboard`.
3. `/anomalies` is compatibility-only and replacement-redirects to `/dashboard`.
4. Market activation opens Dashboard-owned Symbol Detail modal.
5. Anomaly activation opens Dashboard-owned Anomaly Detail modal by exact anomaly UUID.
6. `View all anomalies` opens Dashboard-owned All Anomalies modal.
7. Rows/cards in All Anomalies open exact Anomaly Detail and Back restores All Anomalies and row focus.
8. Modal state is ephemeral local UI state. Do not plan URL-synchronized modal state, modal deep links, or a standalone anomaly visual screen.
9. The backend `/anomalies` read API remains a valid product API and may be expanded additively.
10. Phase 4 must not reverse or weaken any Phase 3.6 navigation, UUID identity, focus, Demo/Live isolation, or legacy redirect invariant.

Historical project-control material requiring `/anomalies` or `/symbols/:symbol` as visual pages must be explicitly identified as superseded in the planning report. Do not edit those historical source files during this task.

## 4. Required target concept

Plan a complete read-only anomaly explorer inside the existing All Anomalies modal, not as a page.

The intended end-state concept is:

- Dashboard Recent Anomalies remains a bounded preview from Dashboard summary;
- `View all anomalies` opens an explorer-capable All Anomalies modal;
- the explorer modal owns filter controls, bounded server-backed results, pagination, loading/error/empty states, and exact UUID activation;
- Anomaly Detail remains a Dashboard-owned modal in the same overlay workflow;
- Symbol Detail remains separate and is opened only by market/symbol actions, not automatically by anomaly activation;
- Back from Anomaly Detail preserves explorer filter/page context and restores the exact result-row focus;
- closing the overlay stack returns to the original Dashboard trigger;
- no mutation, acknowledgement, suppression, trading, alert-management, or surveillance workflow is introduced.

Do not assume that export/share actions belong in the first Phase 4 delivery. Inventory and rank them separately; URL-based share state is incompatible with the current no-modal-deep-link invariant unless the product owner later changes that decision.

## 5. Verified current-state facts to confirm and expand

At the exact planning base, independently confirm at least these known facts and inspect all direct tests/contract generators/docs around them:

### Backend API

- `src/api/handlers.rs` defines `AnomaliesQuery` with only optional string `symbol` and `limit` fields.
- `/anomalies` parses canonical symbol and a bounded positive limit.
- the endpoint currently returns `AnomaliesResponse { source: Live, anomalies }` and has no public Demo-mode path.
- there are no severity, anomaly-type, time-range, cursor, direction, or page metadata fields.

### Backend DTO and storage

- `AnomaliesResponse` is currently a source plus a flat anomaly array.
- anomaly fields currently include UUID, symbol, anomaly type, severity, message, observed/threshold values, event time, and created time.
- `src/storage/anomalies.rs` supports only optional symbol and limit.
- the current query orders only by `created_at DESC` and has no deterministic UUID tie-breaker or cursor.
- the current maximum recent-anomaly limit is 500.

### Frontend data ownership

- `web/src/features/dashboard/api.ts` has a symbol-specific `/anomalies` query used only in Live mode.
- the existing market-anomalies query identity includes mode, symbol, and limit but not explorer filters/cursor.
- current All Anomalies and Anomaly Detail are owned inside `DashboardPage.tsx` and resolve from the active Dashboard summary array.
- current modal identity is exact anomaly UUID and current-mode summary ownership.
- legacy anomaly and symbol routes are redirects, not pages.

These are planning anchors, not an exhaustive inventory.

## 6. Mandatory inventory scope

Read the exact base and produce an evidence-backed inventory of all active files that would be directly or transitively affected by a modal explorer implementation.

At minimum inspect and report:

### Backend

- API router registration for `/anomalies`;
- request query parsing/validation;
- DTOs and generated OpenAPI contract;
- API error mapping;
- demo-data ownership and whether deterministic anomaly history exists or must be designed;
- anomaly domain enums and canonical parse functions;
- PostgreSQL anomaly read/storage implementation;
- schema, migrations, indexes, and same-timestamp behavior;
- existing unit, API, contract, PostgreSQL, replay, and smoke tests;
- product-facing API/README/operations docs affected by an additive contract.

### Frontend

- current Dashboard modal state/controller and dialog boundary;
- Recent Anomalies preview model and desktop/mobile components;
- All Anomalies and Anomaly Detail implementation/tests;
- current query-key factories, API clients, schemas, adapters, formatters, and resource ownership;
- Demo/Live mode ownership and deterministic Demo data path;
- focus/back/close behavior and same-symbol/different-UUID tests;
- UI smoke matrix, browser harness, bundle budget, CI workflow, and route tests;
- component decomposition implications, especially avoiding further growth of `DashboardPage.tsx`.

### Control-plane conflicts

Identify every current project-control statement that conflicts with the integrated modal-only invariant, including the old Phase 4 page/URL-filter plan. Classify each as:

- superseded by explicit product-owner decision and Phase 3.6 integration;
- still applicable after wording adjustment;
- unrelated historical context.

Do not modify historical files in this planning task.

## 7. Required contract decisions

The planning report must make explicit, justified recommendations for each item below. Do not leave them as vague implementation-time questions.

### 7.1 Public API resource identity

Define the semantic identity for an anomaly explorer page resource, including at minimum:

- public data mode;
- canonical optional symbol;
- optional severity;
- optional anomaly type;
- bounded time-range semantics;
- cursor;
- limit.

Specify whether the time range applies to `event_time` or `created_at`, and why. Treat those timestamps as distinct.

### 7.2 Demo and Live behavior

Recommend an additive `/anomalies?mode=demo|live...` contract or another equally explicit server boundary.

Requirements:

- Demo is deterministic and read-only;
- Live never falls back to Demo;
- response source must exactly match requested mode;
- query keys must include mode;
- absent Live history is explicit empty data, not synthetic Demo data.

### 7.3 Stable pagination

Recommend a deterministic keyset/cursor order and exact tie-breaker. Assess at minimum a tuple such as `(created_at, id)` and alternatives based on the current schema and user-visible chronology.

The recommendation must prove how concurrent inserts avoid duplicates/skips within documented cursor semantics.

Specify:

- cursor payload fields;
- opaque encoding/validation expectations;
- sort direction;
- next-cursor response semantics;
- malformed/stale cursor behavior;
- whether a database index or migration is required;
- fresh-database and upgraded-database migration test requirements when applicable.

Offset pagination is not acceptable without strong evidence that it meets concurrent-insert stability requirements.

### 7.4 Filter validation

Define canonical accepted values and validation boundaries for:

- symbol;
- severity;
- anomaly type;
- from/to timestamps;
- maximum time span, if required;
- limit;
- cursor/filter identity consistency.

Do not propose free-form detector or severity values when domain enums already exist.

### 7.5 Response shape

Recommend an additive response DTO that preserves existing anomaly fields and adds bounded-page metadata without fabricating evidence fields.

Assess backward compatibility for existing `/anomalies` consumers and whether the existing flat `anomalies` field can remain while adding `next_cursor` and normalized filter metadata.

### 7.6 Frontend architecture

Recommend exact feature ownership and file boundaries for the explorer. Prefer a dedicated feature module rather than expanding the Dashboard page monolith.

The recommendation must define:

- filter value model and canonical defaults;
- local ephemeral modal filter state;
- query-key factory including every identity dimension;
- AbortSignal/cancellation behavior;
- Zod DTO validation and source/filter identity checks;
- page accumulation or single-page navigation strategy;
- loading/error/empty/refetch behavior;
- desktop/mobile result presentation reuse;
- exact UUID activation;
- preservation of filter/cursor context through Anomaly Detail Back;
- focus restoration to the exact row/card;
- stale mode/filter/cursor response rejection;
- no URL navigation or modal deep-link state.

### 7.7 Detail and symbol interaction

Preserve Anomaly Detail as the primary anomaly activation result.

Inventory whether a deliberate secondary `Open market detail` action inside Anomaly Detail is product-appropriate. If recommended, it must be explicit and must not replace anomaly detail or lose explorer context. If evidence is insufficient, defer it.

Do not restore the obsolete behavior where anomaly rows directly open Symbol Detail.

### 7.8 Export/share

Classify bounded export and share actions as one of:

- required in initial Phase 4;
- optional later mini-phase;
- deferred beyond Phase 4.

A share URL must not be recommended while URL-synchronized modal state remains forbidden. A bounded export must specify strict row limits and exact active-filter ownership.

## 8. Required mini-phase plan

Propose a cohesive Phase 4 branch and ordered mini-phases from the exact planning base.

The plan must:

- recommend an exact branch name but not create it;
- keep one logical purpose per commit;
- identify dependencies and split conditions;
- give each mini-phase a concrete result;
- list an exact initial writable lease or exact inventory-derived path set;
- list forbidden adjacent paths;
- provide a Conventional Commit message;
- provide focused and full verification commands;
- identify required real PostgreSQL integration and migration gates;
- identify browser/component/E2E evidence;
- define each mini-phase terminal status;
- include a final integration/checkpoint sequence.

The plan should normally separate:

1. validated additive API/query DTO contract;
2. stable storage pagination and any proven index migration;
3. frontend explorer resource/query/adapters;
4. modal controller/filter/results presentation;
5. detail/back/focus integration and accessibility hardening;
6. deterministic browser/E2E and final checkpoint.

Combine or split only when the exact-source inventory gives a stronger atomic boundary. Explain every deviation.

Do not authorize all mini-phases at once. The planning output is reviewed first; subsequent implementation contracts will be published separately, one controlled unit at a time.

## 9. Test and evidence matrix

The planning report must define a minimum regression matrix including:

### Backend

- symbol BTC and ETH;
- severity/type combinations;
- event-time or created-time range boundary cases;
- invalid range and limit;
- same timestamp with different UUIDs;
- cursor round trip;
- cursor reused with different filters/mode;
- concurrent insert between pages;
- Demo/Live source isolation;
- empty history;
- mapping/SQL errors;
- OpenAPI drift.

### Frontend

- Demo and Live;
- BTC and ETH;
- two anomalies with same symbol and different UUIDs;
- every filter dimension in query-key identity;
- out-of-order filter/page responses;
- AbortSignal cancellation;
- loading/error/empty/success;
- page navigation or accumulation without duplicates;
- filter reset;
- All Anomalies -> exact Anomaly Detail -> Back with filter/page/focus preserved;
- mode switch closes or replaces stale detail/results correctly;
- desktop and approximately 390px mobile;
- keyboard activation, Escape, backdrop, focus trap, initial focus, and return focus;
- legacy `/anomalies` and `/symbols/:symbol` redirects remain unchanged;
- no standalone visual page content;
- zero unexpected console/page/unhandled errors.

## 10. Bundle and dependency constraints

Current integrated bundle evidence:

- one initial JavaScript asset;
- zero async JavaScript assets;
- raw initial/largest/total: `387239` bytes;
- direct gzip: `110799` bytes;
- current strict limits: raw `395700`, gzip `113042`;
- fixed budgets: `409600 / 409600 / 414720`.

The planning report must account for the very small remaining strict headroom.

Prefer no new frontend dependency. Any dependency recommendation must include measured bundle cost and a concrete need that cannot be met by existing React, TanStack Query, React Router, Zod, Tailwind, and platform APIs.

Do not recommend weakening bundle budgets.

## 11. Planning workspace and permitted actions

Preferred local product inventory worktree:

`/Users/anion/Desktop/work/git-signalguard-rs/worktrees/p4-planning-inventory`

It must be detached at the exact planning base and remain clean.

Preferred isolated connector checkout/worktree:

`/Users/anion/Desktop/work/connector-p4-planning`

Permitted:

- fetch/read exact product and connector refs;
- create a detached clean inventory worktree;
- inspect source, tests, migrations, generated contract, history, and CI configuration;
- run read-only discovery commands and targeted no-change verification when useful;
- publish the required connector planning report and status.

Forbidden:

- editing product files;
- formatting product files;
- installing or updating dependencies in a way that changes tracked files;
- creating a product branch;
- creating any product commit or push;
- opening a product PR;
- running migrations against a non-disposable database;
- starting Phase 4 implementation;
- touching the existing `p35-manual-qa` worktree or environment;
- force-pushing or rewriting either repository.

If any command changes the product worktree, stop, restore only changes proven to have been caused by that command, and report the incident. Do not publish an implementation authorization.

## 12. Required connector outputs

Publish exactly these two paths in one connector commit:

1. Planning report:

`signalguard-rs/phase-4/reports/P4-PLANNING-INVENTORY/ba31a348dc5055935c45f6be81073688caedd925.md`

2. Phase 4 status:

`signalguard-rs/phase-4/control/STATUS.md`

Required connector commit message:

`docs(phase-4): publish modal explorer plan`

The planning report must include:

- exact source and contract identities;
- exact product branch/SHA/tree verification;
- current backend/frontend/test/migration/file inventory;
- verified current limitations;
- historical conflict/supersession table;
- all decisions from Section 7;
- recommended branch and ordered mini-phase plan;
- per-mini-phase initial leases, commit messages, tests, risks, and gates;
- migration/index recommendation;
- API backward-compatibility recommendation;
- frontend architecture diagram in text or Mermaid;
- test/evidence matrix;
- bundle/dependency analysis;
- deferred items;
- open questions that truly require product-owner input, ideally none;
- proof that no product branch, file, commit, push, PR, or merge was created;
- cleanup state.

`STATUS.md` must record:

- state: `P4_PLANNING_COMPLETE_IMPLEMENTATION_NOT_AUTHORIZED`;
- exact planning base and tree;
- planning report commit/blob;
- selected recommended branch name;
- ordered proposed mini-phases;
- modal-only product invariants;
- explicit statement that implementation remains unauthorized;
- next action: orchestrator review and a separate P4-MP01 implementation contract.

The connector commit must modify only those two paths.

Read back both files from connector `main` and verify exact blobs and commit.

## 13. Terminal statuses

Return:

`P4_PLANNING_INVENTORY_COMPLETE`

only after exact-base inventory, complete planning report, status publication, read-back verification, clean product inventory worktree, and cleanup succeed.

Return:

- `P4_PLANNING_BLOCKED_BY_IDENTITY_DRIFT` when the product base/branch/tree moved;
- `P4_PLANNING_BLOCKED_BY_INCOMPLETE_INVENTORY` when material source ownership cannot be established;
- `P4_PLANNING_BLOCKED_BY_PUBLICATION` when connector publication or read-back fails.

Do not return an implementation-complete status. This contract authorizes planning only.
