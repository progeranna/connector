# SignalGuard RS product merge policy

Status: `USER_OVERRIDE_BINDING`

Effective from 2026-07-29.

## Product repository

Repository: `progeranna/signalguard-rs`

Accepted worker commits must remain visible in the product repository history.

For future product integrations:

- do not use squash merge;
- do not use rebase merge;
- do not amend, recreate, or rewrite accepted worker commits;
- use a normal merge commit with an exact expected worker head SHA;
- preserve every accepted worker commit in the ancestry of the target branch;
- force-push and history rewriting remain forbidden.

The connector repository may consolidate its own administrative documentation history when explicitly requested by the user, provided the final tree is preserved and the previous history is retained on a non-default archival branch.
