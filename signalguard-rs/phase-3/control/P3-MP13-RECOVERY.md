# P3-MP13 Recovery Control

## Superseded WEB1

- Original branch: `p3/mp13-recent-anomalies-desktop`
- Original assigned base: `01bf6edae2795a5e118148ad7b291a285a70a8d8`
- Original session was superseded after remaining remotely at `0 0` with no commit, PR, or report.

A late WEB1 delivery subsequently appeared:

- Head: `138a7cd39334755a1e45e61ef5d45ac61d6703d5`
- PR: `#37` — closed, unmerged.
- CI: `30368142923` — success.
- Report: `signalguard-rs/phase-3/reports/P3-MP13/138a7cd39334755a1e45e61ef5d45ac61d6703d5.md`.
- Review: `signalguard-rs/phase-3/reviews/P3-MP13/138a7cd39334755a1e45e61ef5d45ac61d6703d5.md`.
- Verdict: `REJECT` because the execution used the superseded original branch and WEB1 contract after WEB2 had become authoritative.

Green CI and apparent code quality do not override execution identity. The original branch/head remain immutable rejected evidence and must not be merged, amended, rebased, reset, force-pushed, or repaired with another commit.

## Authoritative WEB2 recovery

- Replacement branch: `p3/mp13-recent-anomalies-desktop-r1`
- Exact assigned base: `93a870010730c458417ccfff392cb97aff23d6c9`
- Contract: `signalguard-rs/phase-3/prompts/P3-MP13-WEB2.md`
- Contract commit: `03c9d90d06054a4eb84e136a1ad58bc0c664d3c3`

Recovery policy:

1. Use only the replacement branch and WEB2 contract.
2. Require one normal product commit, one draft PR, one connector report, exact-path proof, remote blob read-back, and complete green current-tree CI.
3. Do not modify or reuse the original branch.
4. Do not accept PR `#37` or head `138a7cd39334755a1e45e61ef5d45ac61d6703d5` as the P3-MP13 integration source.
5. The rejected head may be read as implementation evidence only; acceptance requires a fresh compliant WEB2 delivery.
