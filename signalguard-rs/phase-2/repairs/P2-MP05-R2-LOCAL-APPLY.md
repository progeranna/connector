# P2-MP05-R2 Local Apply Contract — Verified Candidate Integration

## Role

You are the local Codex executor for the already generated and fully verified P2-MP05 candidate.

Do not redesign or reimplement the Redis change. Do not start P2-MP06.

## Product repository

Primary local repository:

`/Users/anion/Desktop/work/git-signalguard-rs/signalguard-rs`

Dedicated worktree path:

`/Users/anion/Desktop/work/git-signalguard-rs/worktrees/p2-mp05-r2`

Remote repository:

`progeranna/signalguard-rs`

Assigned branch:

`p2/mp05-atomic-redis-state-r2`

Exact expected branch base:

`ce2ee582a370cce8bf8198d1fbb82fcb961867c3`

Required product commit message:

`fix(cache): write market state atomically`

## Verified candidate source

Connector file:

`https://raw.githubusercontent.com/progeranna/connector/main/signalguard-rs/phase-2/candidate-results/P2-MP05/03fa30b-ci2/src/storage/redis.rs`

Required SHA-256:

`f8ed711ae4421efadb1d9c6ad520862b58f44ae67ee49130bafb60e82f6777be`

Candidate-builder evidence:

- request id: `03fa30b-ci2`;
- source product SHA: `03fa30b938b6d3d8f351581ee92785dcfdf3e207`;
- workflow run: `30203694273`;
- workflow URL: `https://github.com/progeranna/connector/actions/runs/30203694273`;
- result: `success`;
- canonical rustfmt applied;
- `cargo fmt --all --check` passed;
- `cargo check --all-targets --all-features` passed;
- `cargo clippy --all-targets --all-features -- -D warnings` passed;
- `cargo test --all-targets --all-features` passed;
- existing ignored Redis integration suite passed against Redis 7;
- ignored `atomic_market_state_write` proof tests passed against Redis 7.

Result record:

`signalguard-rs/phase-2/candidate-results/P2-MP05/03fa30b-ci2/result.json`

Checksums:

`signalguard-rs/phase-2/candidate-results/P2-MP05/03fa30b-ci2/checksums.sha256`

## Start conditions

1. Show `pwd`, current branch, `git status --short`, and current HEAD in the primary repository.
2. Run `git fetch origin --prune`.
3. Confirm `origin/p2/mp05-atomic-redis-state-r2` exists and points exactly to `ce2ee582a370cce8bf8198d1fbb82fcb961867c3`.
4. Create or reuse the dedicated worktree for `p2/mp05-atomic-redis-state-r2`.
5. Stop if that worktree is dirty, on another branch, ahead, behind, or not at the exact expected SHA.
6. Confirm `cargo`, `rustfmt`, `clippy`, Git, and Docker are executable locally before changing files.

Do not modify the primary checkout, the superseded branch `p2/mp05-atomic-redis-state`, PR #16, the frontend MP02 worktree, or any connector control file.

## Exact apply procedure

1. Download the verified candidate to a temporary path outside every Git worktree.
2. Compute SHA-256 and require exact equality with:

   `f8ed711ae4421efadb1d9c6ad520862b58f44ae67ee49130bafb60e82f6777be`

3. Copy that exact file to:

   `src/storage/redis.rs`

   in the dedicated R2 worktree.

4. Confirm the only changed product path is:

   `src/storage/redis.rs`

5. Show:

   - `git diff --check`;
   - `git diff --stat`;
   - `git diff -- src/storage/redis.rs`.

6. Confirm the diff contains:

   - one Lua script that checks both Redis key types before mutation;
   - allowed state-key types `none|string`;
   - allowed symbols-key types `none|set`;
   - `SET` and `SADD` only after both checks;
   - real-Redis success, replacement, wrong-symbol-index-type, and wrong-state-key-type tests.

7. Stop if any unrelated semantic or formatting change appears.

## Required local gates

Run in this order:

1. `cargo fmt --all --check`
2. `cargo check --all-targets --all-features`
3. `cargo clippy --all-targets --all-features -- -D warnings`
4. `cargo test --all-targets --all-features`
5. start an isolated Redis 7 container on an unused local port;
6. set `REDIS_URL` to that container;
7. `cargo test --test redis_cache -- --ignored --test-threads=1`
8. `cargo test --lib atomic_market_state_write -- --ignored --test-threads=1`
9. stop and remove the isolated Redis container;
10. `git diff --check`;
11. repository hygiene scan;
12. final `git status --short`.

No commit or push is allowed after any failed required gate.

## Commit and push

After all gates pass:

1. stage only `src/storage/redis.rs`;
2. show `git diff --cached --check` and `git diff --cached --stat`;
3. create exactly one commit:

   `fix(cache): write market state atomically`

4. push only:

   `p2/mp05-atomic-redis-state-r2`

5. do not force-push;
6. do not open or merge a PR unless `gh` is already configured and the operation is straightforward; absence of `gh` is not a blocker after successful push because the Orchestrator will open the PR.

## Final response

Return only:

- repository path;
- worktree path;
- branch;
- base SHA;
- resulting product commit SHA;
- exact changed paths;
- local Rust gate summary;
- local real-Redis gate summary;
- push result;
- PR URL if one was opened;
- blocker, if any.
