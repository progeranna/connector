# P3-CHECKPOINT-2R-R3 — Integration contract

Status: `P3_CHECKPOINT_2R_R3_INTEGRATION_AUTHORIZED`

## Worker mode

Dedicated GitHub web integration worker using connected GitHub tools only.

Do not use a local checkout, shell, Codex CLI, GitHub CLI, filesystem repository copy, or unconnected repository data.

This contract authorizes only exact-ref PR CI and integration of the independently accepted one-file R3 favicon recovery.

Do not execute the next full Checkpoint 2R rerun inside this worker.

## Required authority

Read completely before any write:

- `signalguard-rs/phase-3/control/CURRENT_EXECUTION.md`
- `signalguard-rs/phase-3/control/STATUS.md`
- `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-R3-FAVICON.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-AFTER-R2-BLOCKER/cbf5c543ada8752c273fbb2e91be029c9febc3d3.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R3-FAVICON/778b23b6a9dbb4e1b652e7a31349a35b707f3373.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R3-FAVICON-REVIEW/778b23b6a9dbb4e1b652e7a31349a35b707f3373.md`

Independent review identity:

- connector commit: `d58a9af0ec2fd78724011b6095828bd754909d5d`
- blob: `8a48f027a1e8632541d853c12641d9a303c59267`
- required status: `P3_CHECKPOINT_2R_R3_FAVICON_ACCEPTED_FOR_INTEGRATION`

Implementation report identity:

- connector commit: `b82c112c28eb81f1abe82750b39ebf6e808ec9a8`
- report path: `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R3-FAVICON/778b23b6a9dbb4e1b652e7a31349a35b707f3373.md`
- required status: `P3_CHECKPOINT_2R_R3_FAVICON_COMPLETE`

## Exact product identity

Product repository:

`progeranna/signalguard-rs`

Target branch:

`refactor/dashboard-modules`

Exact target base:

`cbf5c543ada8752c273fbb2e91be029c9febc3d3`

Expected target base tree:

`495d14862b0996766b5376358b99382124df9916`

Worker branch:

`p3/checkpoint2r-favicon-console`

Exact worker commit:

`778b23b6a9dbb4e1b652e7a31349a35b707f3373`

Expected worker tree:

`d5ca241f173f2733d6699283084bf7435c0e9259`

Required worker message:

`fix(ui): prevent missing favicon request`

Before creating a PR, independently prove:

- target branch still resolves exactly to the target base and expected tree;
- worker branch still resolves exactly to the worker commit and expected tree;
- worker is exactly one commit ahead and zero behind target base;
- merge base is exactly the target base;
- the sole worker commit therefore directly descends from the exact target base;
- no existing PR already owns this exact head/base pair.

Stop on any identity drift.

## Exact accepted diff

Target base → worker must contain exactly one modified file:

`web/index.html`

Expected aggregate diff:

- 1 modified file;
- 1 addition;
- 0 deletions;
- 0 added files;
- 0 deleted files;
- 0 renamed files.

The sole patch must be exactly the embedded favicon declaration:

```html
    <link rel="icon" href="data:image/svg+xml,%3Csvg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 1 1%22%3E%3C/svg%3E" />
```

No additional product change is accepted.

## Pull request

Create exactly one non-draft pull request:

- base: `refactor/dashboard-modules`
- head: `p3/checkpoint2r-favicon-console`
- title: `fix(ui): prevent missing favicon request`

Do not modify either branch before CI.

Do not create any second PR for the same head/base pair.

## Synthetic merge identity

After PR creation, identify the exact GitHub synthetic merge ref/commit.

Require ordered parents:

1. `cbf5c543ada8752c273fbb2e91be029c9febc3d3`
2. `778b23b6a9dbb4e1b652e7a31349a35b707f3373`

Expected synthetic merge tree:

`d5ca241f173f2733d6699283084bf7435c0e9259`

Because the worker directly descends from the exact target base and no unrelated target change is allowed, the synthetic tree must equal the accepted worker tree.

Verify:

- base → synthetic effective diff is exactly `web/index.html`, +1 / -0;
- worker → synthetic file diff is empty;
- no merge-only content drift exists.

Stop before merge if any synthetic identity differs.

## Exact-ref PR CI

Require a fresh PR-triggered CI run for the exact synthetic merge ref.

Do not merge until both required jobs complete successfully:

- `frontend`
- `rust`

Verify job metadata, steps and decoded logs. Both jobs must have checked out the exact synthetic merge SHA, not merely the worker head SHA.

### Frontend required result

Must pass on the exact synthetic merge ref:

- full Vitest suite;
- no fewer than 44 test files;
- no fewer than 614 tests;
- zero test failures;
- TypeScript typecheck;
- ESLint with zero warnings;
- production build;
- bundle-policy tests;
- bundle-budget check.

Configured bundle limits must remain unchanged:

- initial JS max: 409600 bytes;
- largest JS max: 409600 bytes;
- total JS max: 414720 bytes.

Because the accepted change is HTML-only, expected JS measurements are the accepted values:

- initial JS: 389599 bytes;
- largest JS: 389599 bytes;
- total JS: 389599 bytes.

Any unexplained bundle drift is a blocker.

### Rust/global required result

Must pass the configured workflow gates for:

- formatting;
- generated API-contract check;
- OpenAPI validation;
- cargo check;
- Clippy with warnings denied;
- Cargo tests;
- replay E2E target discovery;
- Docker Compose config;
- Docker Compose app-profile config;
- demo script syntax;
- smoke script syntax.

Declared service-dependent ignored tests may remain ignored exactly as designed.

Do not use a rerun to conceal a deterministic first failure. A deterministic first-attempt failure blocks integration and requires separate diagnosis/recovery authority.

## Merge

Only after exact synthetic identity and successful exact-ref PR CI, merge by normal merge commit.

Expected worker/head SHA:

`778b23b6a9dbb4e1b652e7a31349a35b707f3373`

Do not squash, rebase, amend, force-push, or rewrite the accepted worker commit.

After merge independently verify:

- PR is closed and merged;
- final merge commit has exactly two ordered parents;
- parent 1 is `cbf5c543ada8752c273fbb2e91be029c9febc3d3`;
- parent 2 is `778b23b6a9dbb4e1b652e7a31349a35b707f3373`;
- final tree is exactly `d5ca241f173f2733d6699283084bf7435c0e9259`;
- old target base → final target is exactly two commits ahead and zero behind;
- effective file diff remains exactly `web/index.html`, +1 / -0;
- worker → final merge has empty file diff;
- tested synthetic tree equals final merge tree;
- worker branch remains unchanged at the accepted worker commit.

## Connector publication

Publish the integration report exactly to:

`signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R3-INTEGRATION/<FINAL_MERGE_SHA>.md`

Connector report commit message:

`docs(phase-3): publish Checkpoint 2R R3 integration`

The report must record:

- integration contract identity;
- independent review identity;
- exact pre-PR target and worker identities;
- exact one-file +1/-0 accepted diff;
- PR number/title/base/head;
- synthetic merge SHA/tree/ordered parents;
- exact synthetic effective diff and empty worker→synthetic diff;
- workflow run ID/attempt/conclusion;
- frontend and rust job IDs/conclusions;
- exact synthetic checkout SHA proved from decoded logs for both jobs;
- frontend test counts and bundle measurements/limits;
- Rust/global gate disposition;
- final merge SHA/tree/ordered parents;
- final target/worker branch read-back;
- final exact effective diff and synthetic/final tree equality;
- confirmation that no full Checkpoint 2R rerun, Bridge 01/02, Wave 4 or later work began.

Then update:

- `signalguard-rs/phase-3/control/CURRENT_EXECUTION.md`
- `signalguard-rs/phase-3/control/STATUS.md`

Final control state must be exactly:

`P3_CHECKPOINT_2R_R3_INTEGRATED_CHECKPOINT_RERUN_NOT_AUTHORIZED`

The control files must pin the new final product merge SHA/tree and state that a separate orchestrator step must publish a new full Checkpoint 2R rerun contract before any validation rerun begins.

## Strict continuation boundary

Do not execute or authorize within this worker:

- a full Checkpoint 2R rerun;
- `P3-W4-BRIDGE01`;
- `P3-W4-BRIDGE02`;
- P3-MP21…P3-MP30 / semantic Wave 4;
- dialogs/accessibility, routing/loading/performance, responsive/final or Phase 4 work;
- any favicon branding/static-asset enhancement beyond the accepted embedded declaration.

## Terminal status

Return exactly:

`P3_CHECKPOINT_2R_R3_INTEGRATION_COMPLETE`

only after exact-ref CI success, normal merge, final identity verification and connector publication/control update all succeed.

Otherwise return exactly:

`P3_CHECKPOINT_2R_R3_INTEGRATION_BLOCKED_BY_IDENTITY_SCOPE_OR_CI`
