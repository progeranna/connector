# P3-MP20R — Blocker diagnostic continuation

Status: `P3_MP20R_DIAGNOSTIC_AUTHORIZED`

## Purpose

This is a diagnostic-only continuation for the same local Codex worker that returned:

`P3_MP20R_BLOCKED_BY_MP18R_OR_SCOPE_CONFLICT`

It does not authorize implementation continuation, lease expansion, requirement revision, commit, push, PR, merge, cleanup, reset, rebase, worktree recreation, or destruction of current evidence.

## Immutable identities

Product repository:

`/Users/anion/Desktop/work/git-signalguard-rs/signalguard-rs`

Product remote:

`progeranna/signalguard-rs`

Expected target branch:

`refactor/dashboard-modules`

Expected immutable integrated base:

`6142ec7004b75cda077a49ab37bcfdca01f7f8e8`

Expected base tree:

`65c816c76a5f9e31858cdcb29acd523e8a92c122`

Assigned branch:

`p3/mp20r-route-presentation-residue`

Assigned worktree:

`/Users/anion/Desktop/work/git-signalguard-rs/worktrees/p3-mp20r`

Original implementation contract:

`signalguard-rs/phase-3/prompts/P3-MP20R.md`

Original contract commit:

`cd7f4daa6a1b8e0a0f71e78a6e0d4af743e588e8`

Original contract blob:

`110352b0d96c315ecf0e8deb1743362d66356901`

Preflight report:

`signalguard-rs/phase-3/reports/P3-MP20R-PREFLIGHT/6142ec7004b75cda077a49ab37bcfdca01f7f8e8.md`

## Current remote evidence

At diagnostic authorization time:

- no remote branch named `p3/mp20r-route-presentation-residue` was found;
- no connector report containing `P3_MP20R_BLOCKED_BY_MP18R_OR_SCOPE_CONFLICT` was found;
- therefore the blocker occurred before product/connector delivery and any useful evidence may exist only in the local worktree and Codex conversation.

## Preservation rules

Use the same Codex conversation and the existing worktree.

Do not:

- reset, restore, checkout, clean, stash, stash-drop, rebase, amend, cherry-pick, recreate or remove the worktree;
- delete local changes or untracked diagnostic artifacts;
- modify product code while diagnosing;
- create a product commit;
- push any branch;
- open a PR;
- write connector files;
- rerun destructive setup commands;
- touch the existing `p35-manual-qa` environment.

Read-only commands and non-mutating test/log inspection are authorized.

## Required diagnostic output

Return a complete structured report directly in the Codex chat.

### 1. Primary blocker class

Choose exactly one:

- `IDENTITY_DRIFT`
- `WORKTREE_PRECONDITION`
- `OUT_OF_LEASE_DEPENDENCY`
- `CONTRACT_REQUIREMENT_CONFLICT`
- `FOCUSED_TEST_FAILURE`
- `FULL_TEST_FAILURE`
- `TYPECHECK_OR_LINT_FAILURE`
- `BUILD_OR_BUNDLE_FAILURE`
- `RUST_OR_GLOBAL_GATE_FAILURE`
- `RESIDUAL_AUDIT_FAILURE`
- `DELIVERY_OR_CONNECTOR_FAILURE`
- `OTHER`

### 2. First proving command

Provide:

- exact command that first proved the blocker;
- working directory;
- exit code;
- minimal complete relevant stdout/stderr;
- first failing file, test, assertion, symbol, path, identity, or residual match;
- whether the failure reproduces from immutable base without the MP20R diff.

Do not substitute a later corroborating failure for the first blocker.

### 3. Repository state

Report without mutation:

```bash
cd /Users/anion/Desktop/work/git-signalguard-rs/worktrees/p3-mp20r
pwd
git status --short
git branch --show-current
git rev-parse HEAD
git show -s --format=%T HEAD
git rev-parse origin/refactor/dashboard-modules
git show -s --format=%T origin/refactor/dashboard-modules
git rev-list --count 6142ec7004b75cda077a49ab37bcfdca01f7f8e8..HEAD
git rev-list --count HEAD..6142ec7004b75cda077a49ab37bcfdca01f7f8e8
git diff --name-status 6142ec7004b75cda077a49ab37bcfdca01f7f8e8
git diff --stat 6142ec7004b75cda077a49ab37bcfdca01f7f8e8
```

State explicitly:

- whether implementation changes exist;
- whether they are committed, staged, unstaged, or untracked;
- every changed/untracked path;
- whether each path is inside the authorized five-file lease;
- whether any product commit, remote branch, PR, connector report, or connector draft exists.

### 4. Consumer and lease audit

Search the existing integrated tree and current diff for every active dependency on the removed shape, including:

- `MarketDisplayVariants`;
- `formatRouteAnomalyValue`;
- `anomalyDisplayVariants`;
- `formatPopupAnomalyValue`;
- `observed.route`;
- `threshold.route`;
- `observed.popup`;
- `threshold.popup`;
- object fixtures containing `route` and `popup` for `MarketAnomalyViewModel`;
- source-string tests or snapshots requiring those concepts;
- TypeScript structural assignments that still expect object-valued `observed` or `threshold`.

List every match by path and classify it as:

- authorized lease and intentionally changed;
- authorized lease and unexpectedly unchanged;
- outside lease but requires change;
- unrelated legitimate occurrence;
- generated/cache/build artifact that must not enter the product diff.

Do not modify matches during diagnosis.

### 5. Contract-conflict analysis

If the blocker is an out-of-lease dependency, identify:

- every exact outside path required;
- exact symbol/test/assertion that requires it;
- why the five leased files cannot satisfy the contract alone;
- smallest possible additional path set;
- whether each path is production or test-only;
- whether the cause is stale test ownership, hidden consumer ownership, generated output, or an overbroad requirement;
- whether any proposed added production path would change visible behavior or MP18R controller/focus logic.

If the blocker is a requirement conflict, identify the two exact incompatible requirements and the narrowest wording revision that preserves product intent.

If the blocker is a validation failure, state:

- whether caused by MP20R;
- whether present on immutable base;
- deterministic reproduction count;
- narrowest valid recovery action.

### 6. Work-preservation recommendation

Return exactly one:

- `PRESERVE_AND_EXPAND_TEST_LEASE`
- `PRESERVE_AND_EXPAND_PRODUCTION_LEASE`
- `PRESERVE_AND_REVISE_REQUIREMENT`
- `PRESERVE_AND_FIX_WITHIN_EXISTING_LEASE`
- `PRESERVE_AND_RETRY_DELIVERY`
- `DISCARD_NOT_AUTHORIZED`
- `BLOCKED_BY_REAL_IDENTITY_DRIFT`

Do not perform the recommendation.

## Terminal result

Return:

`P3_MP20R_DIAGNOSTIC_COMPLETE`

only after printing the complete evidence report.

Return:

`P3_MP20R_DIAGNOSTIC_BLOCKED`

only when the existing worktree or prior execution evidence is unavailable, and identify exactly what is missing.
