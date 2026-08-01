# P3.5-MP09 validation blocker

## Identity

- Product repository: `progeranna/signalguard-rs`
- Exact implementation base and current integrated phase head: `38a1cc440a264d9e04fad3c699386fd45778797f`
- Assigned branch: `p35/mp09-bundle-policy-refinement`
- Original contract: `signalguard-rs/phase-3.5/prompts/P3.5-MP09.md`
- Worker terminal status: `P3_5_MP09_BLOCKED_BY_VALIDATION`

No product commit, push, pull request, merge, or connector implementation report was created.

## Exact blocker

The original MP09 contract required a Node built-in policy suite at:

`web/scripts/check-bundle-size.test.mjs`

The repository's unchanged Vitest discovery also matches `*.test.mjs`. Therefore the protected command:

`vitest run --threads`

discovered the Node `node:test` file as a 46th Vitest suite. The application suites still produced `45` passing files and `653` passing tests, but Vitest failed the Node policy file with:

`No test suite found`

The failure is a runner-discovery conflict, not a bundle-policy, application, or production-build failure.

## Evidence completed before the blocker

- Node built-in policy suite: `25` tests passed when executed by Node.
- Candidate production build: `395700` raw JS bytes.
- Candidate direct gzip: `113042` bytes.
- Initial budget `409600`: pass with `13900` bytes headroom.
- Largest budget `409600`: pass with `13900` bytes headroom.
- Total budget `414720`: pass with `19020` bytes headroom.
- Emitted graph: one initial JS asset and no async JS assets.
- No application-source or package-lock change.
- Generated `dist` output removed.
- Product history remained clean at the exact base; uncommitted changes remained only in the five original MP09 lease paths.

## Recovery disposition

Changing the protected Vitest command is not authorized. Renaming the mandated Node suite would contradict the original path contract. The minimal correct recovery is to add `web/vitest.config.ts` to the writable lease and exclude only `scripts/check-bundle-size.test.mjs` from Vitest discovery while preserving all Vitest default exclusions.

The Node suite remains mandatory and must run separately through Node as part of the bundle-policy command. The frontend Vitest suite must remain `45` files and `653` tests.

Terminal disposition:

`P3_5_MP09_BLOCKED_BY_NODE_TEST_DISCOVERY_MP09_R1_REQUIRED`
