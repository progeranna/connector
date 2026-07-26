# SignalGuard RS — Orchestration Workflow Contract

This document is the permanent operating contract for AI-assisted development of
`progeranna/signalguard-rs`.

## Repositories

### Product repository

`https://github.com/progeranna/signalguard-rs`

Contains only accepted product work:

- source code;
- tests;
- migrations;
- CI and scripts;
- public engineering documentation.

It must not contain raw prompts, worker reports, orchestration notes, handoff
archives, chat exports, or temporary AI-process artifacts.

### Control repository

`https://github.com/progeranna/connector`

Contains the development control plane:

- phase plans;
- worker contracts and prompts;
- worker delivery reports;
- orchestrator reviews;
- correction prompts;
- integration records;
- phase status.

## Roles

### Owner

The owner:

- approves the proposed decomposition and parallelisation for each phase;
- may request changes before workers start;
- after integration, may run one consolidated local Codex verification task;
- performs localhost visual QA when the phase affects observable behaviour;
- explicitly approves the final merge of a completed phase into `main`.

The owner is not expected to download, copy, re-upload, or manually transfer
handoff archives, patches, reports, or source files between workers.

### Orchestrator

The orchestrator owns planning, contracts, validation, integration, and phase
progression.

At the beginning of every phase, the orchestrator:

1. Reads the authoritative project plan, architecture target, workflow rules,
   current repository state, and prior phase evidence.
2. Produces a proposed dependency graph and wave plan.
3. Specifies:
   - parallel and sequential tasks;
   - branch topology;
   - allowed and forbidden paths;
   - integration order;
   - required gates;
   - principal risks and stop conditions.
4. Presents that proposal to the owner before creating worker tasks.
5. Does not start workers until the owner approves or corrects the proposal.

After approval, the orchestrator:

1. Writes the phase control plan and complete worker contracts into `connector`.
2. Commits those files to `connector`.
3. Provides the owner with short launcher prompts that point workers to exact
   contract paths in `connector`.
4. Preferably includes the exact connector commit SHA in launcher prompts so the
   worker reads an immutable contract version.

After each worker delivery, the orchestrator:

1. Reads the worker report from `connector`.
2. Reviews the corresponding `signalguard-rs` branch and pull request.
3. Verifies the exact base SHA, head SHA, changed paths, full diff, tests, CI,
   scope, architecture, compatibility, and repository hygiene.
4. Returns one decision:
   - `ACCEPT`;
   - `ACCEPT_WITH_NOTES`;
   - `REJECT`.
5. For rejected work, writes a correction contract or repair prompt into
   `connector`, commits it, and supplies a new short launcher prompt.
6. For accepted work, integrates the exact reviewed commit into the current
   phase branch using the expected head SHA.
7. Records the review and integration evidence in `connector`.
8. Writes and releases the next worker contracts only when their dependencies
   are satisfied.

The orchestrator may integrate accepted task pull requests into the active phase
branch. The orchestrator must not merge the phase branch into `main` without the
owner's explicit approval after final phase validation.

### Worker

Each worker receives one isolated task.

The worker:

1. Reads the full assigned contract from `connector` before changing code.
2. Works only in `progeranna/signalguard-rs` on the assigned task branch.
3. Starts from the exact base SHA declared by the contract.
4. Modifies only allowed paths and implements only the assigned scope.
5. Runs every available required gate and reports unavailable gates honestly.
6. Creates one atomic commit unless the contract explicitly allows otherwise.
7. Pushes only the assigned task branch.
8. Opens a pull request into the declared phase branch.
9. Does not merge the pull request.
10. Writes a complete delivery report into `connector` at the contract-defined
    unique path.
11. Stops after returning the product commit SHA, product PR URL, report path,
    and report commit SHA.

A worker must never:

- push directly to `signalguard-rs/main`;
- push directly to the active phase branch;
- modify another worker's branch;
- merge its own pull request;
- force-push;
- start a dependent task early;
- place prompts or worker reports in the product repository;
- require the owner to relay archives or patches manually.

## Branch model

For every phase:

```text
main
└── <phase-branch>
    ├── <task-branch-A>
    ├── <task-branch-B>
    └── ...
```

Rules:

- task workers push only to their task branches;
- accepted task PRs target the phase branch;
- only the orchestrator/integrator advances the phase branch;
- the phase branch reaches `main` only after final audit and owner approval;
- integration must be pinned to the exact reviewed task head SHA;
- unexpected branch movement invalidates the prior acceptance and requires
  revalidation.

## Connector layout

The normal structure is:

```text
signalguard-rs/
├── WORKFLOW_CONTRACT.md
└── phases/
    └── <phase-id>/
        ├── CONTROL.md
        ├── STATUS.md
        ├── prompts/
        │   ├── <task-id>.md
        │   └── <repair-id>.md
        ├── reports/
        │   └── <task-id>.md
        ├── reviews/
        │   └── <task-id>.md
        └── integration/
            └── <wave-id>.md
```

Each worker report path is unique. Concurrent workers must not edit the same
report or status file. The orchestrator updates shared phase status after
validating deliveries.

## Phase cycle

Every phase follows this cycle:

```text
Authoritative plan and repository state
→ Orchestrator proposes decomposition and parallelisation
→ Owner approves or corrects it
→ Orchestrator commits contracts and prompts to connector
→ Owner sends short launcher prompts to workers
→ Workers implement on isolated signalguard-rs task branches
→ Workers publish reports in connector and open product PRs
→ Orchestrator validates exact deliveries
→ Rejected tasks receive connector-based repair prompts
→ Accepted tasks are integrated into the phase branch
→ Orchestrator records evidence and releases dependent work
→ One consolidated local verification and localhost QA when needed
→ Final phase audit
→ Owner explicitly approves phase merge into main
```

## Delivery and validation requirements

A worker delivery is not accepted merely because code exists or tests were
claimed as passing.

The orchestrator must independently verify, as applicable:

- exact parent/base SHA;
- exact task head SHA;
- complete changed-file list;
- full patch;
- allowed-path compliance;
- absence of unrelated changes;
- implementation correctness;
- public API and behavioural compatibility;
- architecture invariants;
- test quality and regression coverage;
- CI status for the exact head commit;
- dependency and lockfile changes;
- repository hygiene;
- report accuracy.

A required gate that was unavailable is `NOT_RUN` or `DEFERRED`, never `PASS`.
The orchestrator decides whether deferred local verification is required before
integration or may be consolidated after a wave.

## Integration policy

Accepted task work is integrated into the active phase branch, not directly into
`main`.

Before integration, the orchestrator must confirm:

- the PR head still equals the reviewed SHA;
- the PR base is the intended phase branch;
- required checks are acceptable;
- no unresolved review findings remain;
- the integration order matches the approved wave plan.

After integration, the orchestrator records:

- task PR and reviewed head SHA;
- integration method;
- resulting phase-branch SHA;
- CI/gate state;
- known limitations;
- dependencies now unblocked.

## Owner interaction budget

The intended owner interaction per wave is limited to:

1. approving or correcting the proposed wave plan;
2. sending the short launcher prompts supplied by the orchestrator;
3. optionally running one consolidated post-integration Codex verification;
4. checking localhost visually when relevant.

The workflow must not depend on repeated manual downloading, copying, unpacking,
re-uploading, or applying worker archives.

## Conflict and stop rules

The orchestrator or worker must stop and report instead of improvising when:

- the exact base or branch state differs from the contract;
- unrelated changes are present;
- task scopes overlap unexpectedly;
- a required dependency is not integrated;
- a semantic conflict appears;
- a required available gate fails;
- the requested change would violate an architecture or product invariant;
- credentials, personal data, or non-public artifacts would be exposed.

## Contract precedence

Order of precedence:

1. explicit current owner instruction;
2. this workflow contract;
3. current phase control plan;
4. worker-specific contract;
5. repository-local contributor instructions.

A worker-specific contract may narrow permissions and scope, but may not weaken
this workflow's safety, branch, review, or product-cleanliness rules.
