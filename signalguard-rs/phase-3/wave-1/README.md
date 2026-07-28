# Phase 3 Wave 1 Authorization

Checkpoint 0 is closed at Phase 3 SHA:

`3587ec9b70b677121aa796467d5bb359ffb4d174`

Authorized independent web-worker tasks:

- P3-MP05 — timeline normalization;
- P3-MP07 — Market Health preview model;
- P3-MP08 — Recent Anomalies preview model;
- P3-MP09 — dashboard resource-state mapping.

All four tasks start from the exact same Phase 3 SHA and use non-overlapping new-file path leases. No task may modify `DashboardPage.tsx`, another worker's files, routes, CSS, data boundaries, backend, OpenAPI, package/configuration files, or the upper ticker.

P3-MP06 remains blocked until P3-MP05 is independently accepted and integrated.