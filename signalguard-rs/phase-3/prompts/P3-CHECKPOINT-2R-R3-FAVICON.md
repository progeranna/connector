# P3-CHECKPOINT-2R-R3 — Prevent missing favicon browser request

Status: `P3_CHECKPOINT_2R_R3_FAVICON_IMPLEMENTATION_AUTHORIZED`

## Mode

Dedicated local Codex implementation worker.

Use the `$rust-development` skill.

This is a narrow recovery implementation for the independently accepted Checkpoint 2R browser-console blocker.

Do not perform unrelated cleanup or continue to Bridge 01/02, Wave 4, or later work.

## Exact product base

Product repository:

`progeranna/signalguard-rs`

Target branch:

`refactor/dashboard-modules`

Immutable implementation base commit:

`cbf5c543ada8752c273fbb2e91be029c9febc3d3`

Expected base tree:

`495d14862b0996766b5376358b99382124df9916`

Before editing, fetch the authenticated remote and prove `origin/refactor/dashboard-modules` still resolves exactly to this commit and tree. Any drift is a hard blocker.

## Required authority

Read completely before implementation:

- `signalguard-rs/phase-3/control/CURRENT_EXECUTION.md`
- `signalguard-rs/phase-3/control/STATUS.md`
- `signalguard-rs/phase-3/prompts/P3-CHECKPOINT-2R-RERUN-AFTER-R2-LOCAL.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-AFTER-R2-BLOCKER/cbf5c543ada8752c273fbb2e91be029c9febc3d3.md`
- `signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-RERUN-AFTER-R2-BLOCKER-REVIEW/cbf5c543ada8752c273fbb2e91be029c9febc3d3.md`

Accepted blocker report publication:

- connector commit: `974512cb1b9e934c25d5ccfc2c3874767dbf631d`
- blocker report blob: `ce613b9d93d5062088d26d735af3fc7919498dbd`

Independent blocker review publication:

- connector commit: `688678a91806db7dc3bc3e588d25a4e0d3999f3b`
- status: `P3_CHECKPOINT_2R_RERUN_AFTER_R2_BLOCKER_ACCEPTED_R3_REQUIRED`

## Local repository and branch

Local repository:

`/Users/anion/Desktop/work/git-signalguard-rs/signalguard-rs`

Assigned branch:

`p3/checkpoint2r-favicon-console`

Use a fresh dedicated worktree from the exact immutable base. Suggested path:

`/Users/anion/Desktop/work/git-signalguard-rs/worktrees/p3-checkpoint2r-r3-favicon`

Required single product commit message:

`fix(ui): prevent missing favicon request`

## Exact writable lease

Exactly one tracked product file may change:

`web/index.html`

No other tracked product or test path is writable.

The final base-to-worker diff must contain exactly this one modified file and no added, deleted, or renamed file.

## Required implementation

At the immutable base, `web/index.html` has blob:

`f9cbef13a7d91bcdd998a5f8082d954a136b8348`

It has no favicon declaration, and no repository favicon asset exists at `web/public/favicon.ico` or root `favicon.ico`.

Make the smallest possible document-only change:

Insert exactly this line inside `<head>`, after the existing description metadata and before `<title>`:

```html
    <link rel="icon" href="data:image/svg+xml,%3Csvg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 1 1%22%3E%3C/svg%3E" />
```

Do not alter any other byte in `web/index.html` except the newline positioning required for this exact inserted line.

Required semantics:

- favicon identity is embedded as a data URL;
- the browser must not need any network request for `/favicon.ico`;
- no new static asset is added;
- no product copy, title, metadata, script identity, page structure, or application behavior changes;
- the favicon may be visually transparent; this recovery is about deterministic browser request/error behavior, not branding.

## Strictly forbidden scope

Do not modify:

- any Dashboard or modal file;
- any R1/R2 implementation or test file;
- routes/router/navigation;
- API/resource/query/schema code;
- CSS or presentation components;
- ticker ownership;
- package manifests or lockfiles;
- bundle-size budgets or scripts;
- Vite config;
- any `web/public/*` path;
- any new favicon/static asset;
- Rust/backend/OpenAPI/contracts/migrations/Docker/scripts;
- connector control files from the implementation worker;
- Bridge 01/02, Wave 4, or later-phase code.

Do not reformat the whole HTML file.

## Focused blocker validation

After the edit and before the full gates:

1. Build the production frontend.
2. Run a fresh isolated production preview/browser setup using a real fresh Chrome context.
3. Navigate at minimum to `/dashboard` with the real accepted Demo backend behavior available, matching the blocker surface.
4. Also validate `/` in a separate fresh page/context or equivalent clean navigation.
5. Record all browser requests and browser console/page errors.

Required focused acceptance:

- no request whose URL pathname is `/favicon.ico`;
- browser console errors: `0`;
- page errors: `0`;
- unhandled promise rejections: `0`;
- Dashboard application resources and real Demo API calls continue to load normally;
- no Demo/Live behavior is modified;
- `dist/index.html` contains the embedded favicon declaration;
- no external favicon/static asset exists or is emitted solely for this change.

Do not mock or intercept `/favicon.ico` to make the check pass. The absence of the request must come from the document declaration itself.

Capture focused evidence outside both repositories, including request log and at least one screenshot of the successfully rendered Dashboard. Record SHA-256 hashes in the implementation report.

## Full frontend gates

From `web/` run:

```bash
node --test scripts/check-bundle-size.test.mjs
npm run test:run
npm run typecheck
npm run lint
npm run build
npm run bundle:check
```

Required expectations:

- 25/25 bundle-policy tests;
- no fewer than 44 frontend test files;
- no fewer than 614 frontend tests;
- zero frontend test failures;
- typecheck pass;
- ESLint pass with zero warnings;
- build pass;
- bundle-budget pass.

Because JavaScript/CSS sources are outside the lease, the expected JS bundle remains exactly the accepted measurement unless tooling nondeterminism is concretely demonstrated:

- initial JS: `389599` bytes;
- largest JS: `389599` bytes;
- total JS: `389599` bytes;
- limits remain `409600 / 409600 / 414720` bytes.

No budget change is permitted.

## Full root/global gates

From repository root run:

```bash
cargo fmt --check
cargo run --quiet --bin export-api-contract -- --check
cargo run --quiet --bin export-api-contract -- --validate
cargo check
cargo clippy --all-targets --all-features -- -D warnings
cargo test
cargo test --test replay_e2e
docker compose config
docker compose --profile app config
bash -n scripts/demo-replay.sh
bash -n scripts/smoke.sh
git diff --check
```

All commands must pass. Declared service-dependent ignored tests remain ignored exactly as designed.

## Exact diff and residual audit

Before commit prove:

- only `web/index.html` differs from the immutable base;
- the diff is only the exact embedded favicon line;
- `web/public/favicon.ico` is still absent;
- root `favicon.ico` is still absent;
- no other static asset was added;
- package/lock/budget files are unchanged;
- no application source/test file changed;
- `git diff --check` passes.

After commit prove:

- exactly one product commit ahead of `cbf5c543ada8752c273fbb2e91be029c9febc3d3`;
- zero commits behind;
- merge base is exactly the immutable base;
- direct parent is exactly the immutable base;
- commit message is exactly `fix(ui): prevent missing favicon request`;
- effective diff is exactly one modified path: `web/index.html`.

## Delivery

Push only:

`p3/checkpoint2r-favicon-console`

Do not open a pull request.

Do not merge anything.

Do not modify `refactor/dashboard-modules`.

Publish the implementation report to:

`signalguard-rs/phase-3/reports/P3-CHECKPOINT-2R-R3-FAVICON/<PRODUCT_COMMIT_SHA>.md`

Connector report commit message:

`docs(phase-3): publish Checkpoint 2R R3 favicon implementation`

The report must include:

- contract identity;
- exact immutable base SHA/tree;
- worker branch/commit/tree/message/parent;
- exact one-file diff and line-level description;
- focused fresh-browser request/error evidence for `/dashboard` and `/`;
- confirmation that `/favicon.ico` was not requested and was not intercepted/mocked;
- screenshot/request-log evidence hashes;
- every frontend/root gate and test count;
- bundle measurements and unchanged limits;
- final branch relation and cleanliness;
- confirmation that no PR/merge was created;
- confirmation that Bridge 01/02, Wave 4 and later work did not begin.

Do not update `CURRENT_EXECUTION.md` or `STATUS.md` from the implementation worker.

## Terminal status

Return exactly:

`P3_CHECKPOINT_2R_R3_FAVICON_COMPLETE`

only if the exact one-file implementation, focused browser proof, all prescribed gates, exact commit/branch identity, push, and connector report publication succeed.

Otherwise return exactly:

`P3_CHECKPOINT_2R_R3_FAVICON_BLOCKED`

Do not expand the lease or fix any additional defect without a new orchestrator contract.
