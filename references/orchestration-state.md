# Canonical Orchestration State

## Purpose

Morrison must not rely on conversational memory to reconstruct the organization.

Every non-trivial task keeps one canonical durable state that records objective, authority, dependency availability, artifacts, questions, pair independence, batches, backlog, reopening, implementation and validation.

This may live in a GitHub Issue, structured task document/runtime state or another authoritative durable artifact. Do not create a competing source of truth when the project already has one.

## Canonical task record

Recommended logical schema:

```text
ORCHESTRATION-STATE

Task-ID: <stable anchor>
State-Revision: <integer>
Objective: <current user-approved outcome>
Task-Type: IDEA_OR_PRODUCT | TECHNICAL_CHANGE | INVESTIGATION | IMPLEMENTATION | VALIDATION | FUNCTIONAL_BACKEND_DEFECT | TRIVIAL
Risk-Level: LOW | MEDIUM | HIGH
Current-Gate: INTAKE | PRODUCT | PLAN | PLAN_REOPENING | EXECUTION | VALIDATION | USER_DECISION | COMPLETE | BLOCKED
Current-Owner: <Agent-Key | USER>
Plan-Maturity: NOT_STARTED | DRAFT | MATURE | REOPENING | REVISED | EXECUTION_READY | STALE | NOT_REQUIRED
Pairing-Policy: REQUIRED | OPTIONAL | EXEMPT
Pairing-Exception: <reason | NONE>
Reopening-Policy: REQUIRED | OPTIONAL | EXEMPT
Reopening-Exception: <reason | NONE>

Runtime-Capacity:
- Max-Concurrent-Children: <integer | UNKNOWN>
- Working-Batch-Size: <integer>
- Active-Batch: <Batch-ID | NONE>

Skill-Dependency-Mode: FULL | REDUCED | BLOCKED
Task-Skill-Context:
- agent-context-foundation: AVAILABLE | MISSING | BLOCKED
- intensive-ui-questioning: AVAILABLE | MISSING | BLOCKED | NOT_REQUIRED
- Dependency-Evidence: <anchors>
- Conditional-Activations: <skill/status list>

Council-Mode: OFF | REQUESTED | ACTIVE
Council-Session: <id | NONE>

Constraints:
- ...

Fixed-Decisions:
- Decision: ...
  Owner: ...
  Evidence/Authority: ...

Open-Material-Questions:
- <QUESTION entries>

Canonical-Artifacts:
- Product-Brief: <anchor/status>
- Role-Plans: <anchors/status>
- Technical-Integration-Plan: <anchor/status or NOT_REQUIRED>
- Plan-Reopening: <anchor/status>
- Verification-Contract: <anchor/status>
- Implementation: <anchor/status>
- Validation-Report: <anchor/status>

Pair-Groups:
- <PAIR-GROUP entries>

Delegation-Batches:
- <DELEGATION-BATCH entries>

Organizational-Backlog:
- <BACKLOG entries>

Active-Agents:
- <AGENT-INSTANCE entries>

Terminated-Agents:
- <instance + role + return/checkpoint anchor; compact>

UI-Questioning:
- <UI-QUESTIONING record or NOT_ACTIVE>

Plan-Reopening:
- <PLAN-REOPENING record or NOT_REQUIRED>

Gate-Status:
- Product: NOT_REQUIRED | OPEN | PASSED | STALE
- Plan: NOT_REQUIRED | OPEN | MATURE | REOPENING | EXECUTION_READY | STALE
- Execution: NOT_REQUIRED | OPEN | PASSED | STALE
- Validation: NOT_REQUIRED | OPEN | PASSED | FAILED | BLOCKED | STALE

Next-Action: <one concrete organizational action>
```

The logical fields are the contract even when physical storage differs.

## Skill dependency / activation registry

Use:

- `references/installation-and-dependencies.md` for availability;
- `references/skill-routing.md` for activation and role-boundary semantics.

A URL/profile mention is not proof of availability.

```text
SKILL-ACTIVATION

Skill: <name>
Canonical-Source: <repository/entrypoint>
Resolved-Source: <installed/mounted/current source anchor | NONE>
Availability: AVAILABLE | MISSING | BLOCKED | NOT_REQUIRED
Scope: <task | artifact | agent | department>
Owner: <Morrison/role instance>
Activation-Status: REQUIRED | ACTIVE | NOT_ACTIVE | COMPLETE | STALE | BLOCKED
Activate-When: <condition>
Started-From: <state revision/artifact>
Coverage-Anchor: <receipt/artifact | NONE>
Blocked-Reason: <reason | NONE>
```

When an upstream premise changes, mark only affected skill coverage stale and rerun required routes.

## Pair Group Registry

For every non-trivial cognitive workstream governed by `references/paired-delegation.md`:

```text
PAIR-GROUP

Pair-Group: <stable id>
Agent-Key: <same contracted role for A+B>
Purpose: <research/planning/review/etc>
Owner: <synthesis owner>
State: CREATED | INDEPENDENT_WORK | FIRST_RETURNS | CROSS_REVIEW | SYNTHESIS | RESOLVED | BLOCKED | STALE
Pair-Execution-Mode: CONCURRENT | FROZEN_SNAPSHOT_SEQUENTIAL
Pair-Start-Revision: <one frozen canonical revision/input-set id>
Independence-Requirement: INITIAL_ISOLATION
Member-A: <agent instance>
Member-B: <agent instance>
First-Return-A: <anchor/status>
First-Return-B: <anchor/status>
Peer-Visibility-Before-First-Returns: NONE
Agreements: <anchor/summary>
Contradictions: <anchor/summary>
Unique-Findings-A: <anchor/summary>
Unique-Findings-B: <anchor/summary>
Cross-Review: <anchor/status>
Synthesis-Artifact: <anchor/status>
Unresolved-Material-Disagreement: <NONE | question ids>
```

Rules:

- both pair members start from the same logical frozen inputs;
- in `FROZEN_SNAPSHOT_SEQUENTIAL`, B must not see A's first return and A-derived changes must not alter B's start state;
- if equivalent starting evidence cannot be preserved, full pair independence is not satisfied;
- agreement alone is not proof;
- different Agent-Keys never satisfy the pair.

## Delegation Batch Registry

```text
DELEGATION-BATCH

Batch-ID: <stable id>
Parent: <owner>
Started-From: <state revision>
Slot-Budget: <integer | UNKNOWN_CONSERVATIVE>
State: QUEUED | ACTIVE | COLLECTING | COMMITTED | TERMINATED
Active-Children: <instance ids>
Pair-Groups: <ids>
Objectives: <compact list>
Expected-Returns: <anchors/classes>
Committed-Returns: <anchors>
Queued-After: <backlog item ids>
```

A batch becomes `COMMITTED` only after every material result/question/decision needed from it is durable elsewhere.

Pair members can span sequential child executions under a single logical pair even when one slot forces `FROZEN_SNAPSHOT_SEQUENTIAL`; preserve pair start revision and isolation explicitly.

## Organizational Backlog

```text
ORGANIZATIONAL-BACKLOG-ITEM

Item-ID: <id>
Required-Role: <contracted Agent-Key | CAPABILITY_GAP:<specialty>>
Objective: <bounded result>
Depends-On: <artifact/question ids>
Priority: <value>
Expected-Return: <artifact>
Status: QUEUED | READY | BLOCKED | DONE | DROPPED
Last-Revalidated-At: <state revision>
```

Queued work must be revalidated after material upstream changes.

## Agent Instance Registry

```text
AGENT-INSTANCE

Agent-Instance: <unique id/name>
Agent-Key: <stable contracted profile key>
Parent: <owner>
Reasoning-Class: LIGHT | STANDARD | DEEP | MAX | SPECIALIST
Lifecycle-State: CREATED | WORKING | QUESTIONING | WAITING_PARENT | WAITING_CHILD | BLOCKED | RETURNED_COMPLETE | RETURNED_INCONCLUSIVE | RETURNED_REJECTED
Work-Phase: DISCOVER | PLAN | REVIEW | SYNTHESIZE | IMPLEMENT | VERIFY
Production-Write-Authority: YES | NO
Batch-ID: <id | NONE>
Required-Skills: <skill + availability/source/coverage>
Conditional-Skills: <skill + activation/availability/status>
Context-Checkpoint-Target: <anchor>
Objective: <one-line objective>
Expected-Return: <artifact>
Waiting-On: <question/agent/evidence | NONE>
Spawn-Permission: NONE | THINKERS_ONLY | NAMED_SUPPORT_ROLE_REQUESTS | DELEGATED_OWNER
Started-From: <canonical revision/artifact anchors>
Pair-Group: <group id | NONE>
Pair-Position: A | B | NONE
Peer-Artifact-Visibility: NONE_UNTIL_FIRST_RETURN | AFTER_FIRST_RETURN | NOT_APPLICABLE
Last-Checkpoint: <timestamp/revision when available>
```

The full child contract remains the manifest; this registry is the compact operational view.

## Thinker registry

Thinkers are disposable and may contribute at most one question/clean result.

```text
THINKER-WAVE

Wave-ID: <id>
Parent: <owner>
Objective: <artifact/stage being questioned>
Started-From: <state revision>
Batch-ID: <id>
Thinker-Count: <integer>
Independence: FRESH_ISOLATED
State: WORKING | RETURNED | TERMINATED
Returned-Question-IDs: <ids>
Clean-Returns: <count>
```

Thinkers do not own durable memory. Parent decides how any material result is persisted/promoted.

## Question registry

```text
QUESTION

Question-ID: <stable id>
Question: <exact material question>
Source: <Thinker/role instance>
Why-It-Matters: <impact>
Owner: <Agent-Key | USER | capability gap>
Evidence-Needed: <resolution evidence>
Status: OPEN | ROUTED | ANSWERED | BLOCKED | REJECTED_NON_MATERIAL
Resolution: <answer/disposition>
Resolution-Anchor: <anchor>
Affected-Artifacts: <ids that become stale if premise changes>
```

Merge duplicates rather than counting them as confidence.

## UI Questioning Registry

When `intensive-ui-questioning` is active:

```text
UI-QUESTIONING

Skill: intensive-ui-questioning
Status: ACTIVE | COMPLETE | BLOCKED | STALE
Required-Rounds: 4 | 5
Completed-Rounds: <0..5>
Fresh-Round-Guarantee: FULL | REDUCED | BLOCKED
Current-Round: <1..5 | NONE>
Current-Artifact: <anchor/revision>
Round-Receipts: <anchors>
Open-Question-IDs: <ids>
Last-Material-Change: <anchor/revision>
Final-Route-Closure: COMPLETE | OPEN_DEPENDENCIES | BLOCKED | NOT_REACHED
```

Each round uses new agent identities. Same-round A+B may be concurrent or frozen-snapshot sequential according to `references/batched-delegation.md`.

## Plan Reopening Registry

```text
PLAN-REOPENING

Reopening-ID: <id>
Artifact: <plan anchor>
Started-From: <revision>
State: NOT_STARTED | ACTIVE | REVISION_REQUIRED | READY | BLOCKED | USER_DECISION
Thinker-Question-IDs: <ids>
Challenge-Pair: <pair id/status>
Alternative-Pair: <pair id/status>
Risk-Pair: <pair id/status | NOT_REQUIRED>
Material-Findings: <ids/anchors>
Alternative-Approaches: <anchors>
Decisions-Reopened: <ids>
Decisions-Preserved: <ids + evidence>
Plan-Revision: <anchor/status>
Remaining-Questions: <ids>
Disposition: EXECUTION_READY | REVISE_AGAIN | USER_DECISION | BLOCKED
```

A plan cannot be execution-ready while required reopening is unresolved.

## Council Session Registry

```text
COUNCIL-SESSION

Council-ID: <id>
Purpose: <bounded discussion>
Chair: orchestrator
Started-From: <state revision>
Visible-Participants: <instances/roles>
Host-Mode: DIRECT_MULTI_AGENT | ORCHESTRATOR_RELAY
Open-Questions: <ids>
Decisions-Made: <ids>
State: ACTIVE | COMPLETE | BLOCKED
```

Council mode never merges role authority.

## Artifact freshness

If a material premise changes:

1. mark dependent artifacts/gates `STALE`;
2. identify earliest premise owner that must reevaluate;
3. mark affected pair synthesis stale;
4. invalidate relevant reopening conclusions;
5. mark affected skill coverage stale;
6. revalidate queued backlog;
7. recreate fresh children where required;
8. rerun only affected portions when possible.

Do not preserve stale approval because work was already spent.

## State update ownership

Morrison owns overall orchestration state.

Children own their return artifacts/status inside their assignment and report upward. They do not rewrite unrelated agents' state or advance global gates independently.

## Revision discipline

Increment `State-Revision` for material organizational changes, including:

- objective/task type change;
- material decision/question resolution;
- owner change;
- stable child spawn/termination;
- dependency availability/activation change;
- pair/batch state change;
- backlog mutation;
- plan maturity/reopening change;
- Council open/close;
- gate change;
- canonical artifact replacement.

Do not create noisy revisions for cosmetic formatting.

## Recovery after context loss

A fresh Morrison recovers by:

1. reading this canonical state;
2. loading the current runtime/dependency/role contracts;
3. re-resolving actual skill availability;
4. loading only current artifacts/active role profiles;
5. identifying active/incomplete pairs/batches/backlog;
6. validating pair start revisions/independence mode;
7. recreating stale contexts as needed;
8. continuing from `Next-Action`.

Do not reconstruct authoritative task state from raw chat history when canonical state exists.

## Completion state

Set `Current-Gate: COMPLETE` only when:

- current objective is satisfied;
- required gates passed;
- required pair groups resolved or valid exceptions exist;
- required plan reopening passed or valid exception exists;
- required dependency states are resolved and required skills were actually applied, or affected paths remain explicitly reduced/blocked instead of falsely passed;
- conditional skill routes are closed for current scope;
- no material contradiction/question remains unowned;
- no required batch/agent is blocked/waiting;
- no required backlog item remains unfinished;
- validation passed when required;
- user-authority decisions are resolved or explicitly outside scope/deferred;
- unnecessary child contexts are terminated;
- Council Session is closed when used.

## Core principle

**The organization may forget conversations and terminate entire batches; it must not forget state, dependencies, pair independence, questions, evidence, artifacts, risk or ownership.**