# P3-MP13 Recovery Control

- WEB1 branch: `p3/mp13-recent-anomalies-desktop`
- WEB1 status: `STALLED_NO_REMOTE_DELIVERY`
- Remote divergence from assigned base `01bf6edae2795a5e118148ad7b291a285a70a8d8`: ahead 0 / behind 0.
- Product commit: none.
- PR: none.
- Connector report: none.

The original web-worker session produced no remote product state. To prevent a late race from that stalled session, WEB1 is superseded as an execution source.

Recovery policy:

1. Leave the original WEB1 branch untouched.
2. Do not reuse the stalled session.
3. Create a replacement branch from the current accepted Phase 3 SHA.
4. Use a new immutable WEB2 contract and a new web-worker chat.
5. Require one normal product commit, one draft PR, one connector report, exact-path proof, and complete green CI.
