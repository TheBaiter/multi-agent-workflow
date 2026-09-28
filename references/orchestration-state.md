# Canonical Orchestration State

## Purpose

The Orchestrator must not rely on conversational memory to remember the organization.

Every non-trivial task should have one canonical orchestration state that lets a fresh Orchestrator reconstruct:

- what the user wants;
- what is fixed vs unresolved;
- which departments/roles are active or queued;
- which child agents exist and who owns them;
- which procedural skills are required/active and whether their current sources are actually available;
- which same-role A/B pairs belong to each decision;
- which delegation batch is active and which work is queued;
- what each child returned before termination;
- which one-question Thinker findings remain open;
- which canonical artifacts are current/stale;
- whether a mature plan is still being reopened;
- whether a user-visible council is active;
- which gate/batch must run next.

This state may live in a GitHub Issue, task document, structured runtime state or another durable artifact appropriate to the environment.

Do not create a second competing source of truth when the project already has an authoritative task artifact capable of holding this information.

## Canonical task record

Recommended logical schema:

~~~text
ORCHESTRATION-STATE

Task-ID: <stable id/anchor>
State-Revision: <integer>
Objective: <current user-approved outcome>
Task-Type: <IDEA_OR_PRODUCT | TECHNICAL_CHANGE | INVESTIGATION | IMPLEMENTATION | VALIDATION | FUNCTIONAL_BACKEND_DEFECT | TRIVIAL>
Risk-Level: <LOW | MEDIUM | HIGH>
Current-Gate: <INTAKE | PRODUCT | PLAN | PLAN_REOPENING | EXECUTION | VALIDATION | USER_DECISION | COMPLETE | BLOCKED>
Current-Owner: <Agent-Key or USER>
Plan-Maturity: <NOT_STARTED | DRAFT | MATURE | REOPENING | REVISED | EXECUTION_READY | STALE | NOT_REQUIRED>
Pairing-Policy: REQUIRED | OPTIONAL | EXEMPT
Pairing-Exception: <reason or NONE>
Reopening-Policy: REQUIRED | OPTIONAL | EXEMPT
Reopening-Exception: <reason or NONE>

Runtime-Capacity:
- Max-Concurrent-Children: <integer | UNKNOWN>
- Working-Batch-Size: <integer>
- Active-Batch: <Batch-ID | NONE>

Council-Mode: OFF | REQUESTED | ACTIVE
Council-Session: <id or NONE>

Skill-Dependency-Mode: FULL | REDUCED | BLOCKED
Task-Skill-Context:
- agent-context-foundation: AVAILABLE | MISSING | BLOCKED
- intensive-ui-questioning: AVAILABLE | MISSING | BLOCKED | NOT_REQUIRED
- Dependency-Evidence: <installed/mounted/current source anchors>
- Conditional-Activations: <skill/status list>

Constraints:
- ...

Fixed-Decisions:
- Decision: ...
  Owner: ...
  Evidence/Authority: ...

Open-Material-Questions:
- Question-ID: Q-...
  Question: ...
  Source: <Thinker instance / role instance>
  Owner: ...
  Status: OPEN | ROUTED | ANSWERED | BLOCKED | REJECTED_NON_MATERIAL
  Impact: ...
  Resolution-Anchor: ...

Canonical-Artifacts:
- Product-Brief: <anchor/status>
- Role-Plans: <anchors/status>
- Technical-Plan: <anchor/status>
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
- <Agent Instance Registry entries>

Terminated-Agents:
- <instance + role + final return anchor; compact only>

Gate-Status:
- Product: NOT_REQUIRED | OPEN | PASSED | STALE
- Plan: NOT_REQUIRED | OPEN | MATURE | REOPENING | EXECUTION_READY | STALE
- Execution: NOT_REQUIRED | OPEN | PASSED | STALE
- Validation: NOT_REQUIRED | OPEN | PASSED | FAILED | BLOCKED | STALE

Next-Action:
<one concrete organizational action>
~~~

The logical fields are the contract even when storage format differs.

## Skill Dependency and Activation Registry

Use `references/installation-and-dependencies.md` for availability semantics and `references/skill-routing.md` for activation/role-boundary policy.

Every stable role requires `agent-context-foundation` for full-mode operation. Additional skills are task/assignment-specific.

Do not record a skill as available merely because a profile contains its repository URL. Availability requires an actual current source that the runtime/child can load.

Record dependency/activation state compactly enough that a fresh child or later batch does not need conversational memory to know which procedure still applies.

~~~text
SKILL-ACTIVATION

Skill: <stable skill name>
Canonical-Source: <repository/entrypoint>
Resolved-Source: <installed/mounted/current source anchor or NONE>
Availability: AVAILABLE | MISSING | BLOCKED | NOT_REQUIRED
Scope: <task | artifact | agent instance | department>
Owner: <Morrison or role instance>
Activation-Status: REQUIRED | ACTIVE | NOT_ACTIVE | COMPLETE | STALE | BLOCKED
Activate-When: <condition>
Started-From: <state revision/artifact>
Coverage-Anchor: <receipt/artifact/question coverage>
Blocked-Reason: <reason or NONE>
~~~

Rules:

- stable agents default to `agent-context-foundation: REQUIRED`; full mode requires `Availability: AVAILABLE`;
- meaningful visible/perceptible frontend work records `intensive-ui-questioning` when activated; active use requires `Availability: AVAILABLE`;
- a skill becoming active does not change role ownership or production-write authority;
- if an upstream premise changes materially, mark dependent skill coverage `STALE` and reopen only the affected route;
- if a required external skill source cannot be accessed, mark availability `MISSING`/`BLOCKED` and the dependent work `REDUCED`, `PARTIAL` or `BLOCKED` according to the owning contract rather than reconstructing the skill from memory;
- do not duplicate the external skill body into orchestration state.

## Pair Group Registry

For every non-trivial cognitive workstream governed by `references/paired-delegation.md`, keep:

~~~text
PAIR-GROUP

Pair-Group: <stable id>
Agent-Key: <same role for A+B>
Purpose: <planning/review/research/etc>
Owner: <synthesis owner>
State: CREATED | INDEPENDENT_WORK | CROSS_REVIEW | SYNTHESIS | RESOLVED | BLOCKED | STALE
Started-From: <canonical state revision/artifact anchors>
Member-A: <agent instance>
Member-B: <agent instance>
First-Return-A: <anchor/status>
First-Return-B: <anchor/status>
Agreements: <anchor/summary>
Contradictions: <anchor/summary>
Unique-Findings-A: <anchor/summary>
Unique-Findings-B: <anchor/summary>
Cross-Review: <anchor/status>
Synthesis-Artifact: <anchor/status>
Unresolved-Material-Disagreement: <NONE or question ids>
~~~

Do not mark a pair resolved merely because both members agree.

## Delegation Batch Registry

For `references/batched-delegation.md` keep:

~~~text
DELEGATION-BATCH

Batch-ID: ...
Parent: ...
Started-From: <state revision>
Slot-Budget: <integer | UNKNOWN_CONSERVATIVE>
State: QUEUED | ACTIVE | COLLECTING | COMMITTED | TERMINATED
Active-Children: <instance ids>
Pair-Groups: <ids>
Objectives: <compact list>
Expected-Returns: <anchors/classes>
Committed-Returns: <anchors>
Queued-After: <backlog item ids>
~~~

A batch must be `COMMITTED` before completed children are discarded as memory sources.

`COMMITTED` means material results/questions/decisions are now durable elsewhere.

## Organizational backlog

Work waiting for future slots should be durable rather than represented by idle children.

~~~text
ORGANIZATIONAL-BACKLOG-ITEM

Item-ID: ...
Required-Role: <Agent-Key>
Objective: ...
Depends-On: <artifact/question ids>
Priority: ...
Expected-Return: ...
Status: QUEUED | READY | BLOCKED | DONE | DROPPED
Last-Revalidated-At: <state revision>
~~~

Revalidate queued items after upstream changes before spawning them.

## Agent Instance Registry

For every active stable child:

~~~text
AGENT-INSTANCE

Agent-Instance: <unique id>
Agent-Key: <stable profile key>
Parent: <agent instance/orchestrator>
Reasoning-Class: LIGHT | STANDARD | DEEP | MAX
Lifecycle-State: CREATED | WORKING | QUESTIONING | WAITING_PARENT | WAITING_CHILD | BLOCKED | RETURNED_COMPLETE | RETURNED_INCONCLUSIVE | RETURNED_REJECTED
Work-Phase: DISCOVER | PLAN | REVIEW | SYNTHESIZE | IMPLEMENT | VERIFY
Production-Write-Authority: YES | NO
Batch-ID: <id or NONE>
Required-Skills:
- <skill + availability/source/coverage>
Conditional-Skills:
- <skill + activation/availability/status>
Context-Checkpoint-Target: <anchor>
Objective: <one-line objective>
Expected-Return: <artifact>
Waiting-On: <question/agent/evidence or NONE>
Spawn-Permission: NONE | THINKERS_ONLY | NAMED_SUPPORT_ROLES | DELEGATED_OWNER
Started-From: <canonical state revision/artifact anchors>
Pair-Group: <group id or NONE>
Pair-Position: A | B | NONE
Peer-Artifact-Visibility: NONE_UNTIL_FIRST_RETURN | AFTER_FIRST_RETURN | NOT_APPLICABLE
Last-Checkpoint: <timestamp/revision when available>
~~~

The full child contract remains the Agent Manifest. The registry is the compact operational view.

## Thinker registry: one question per instance

Thinkers are disposable micro-reviewers, not durable pseudo-employees.

While a wave is active:

~~~text
THINKER-WAVE
Wave-ID: ...
Parent: ...
Objective: ...
Started-From: <state revision>
Batch-ID: ...
Thinker-Count: <integer>
Independence: FRESH_ISOLATED
State: WORKING | RETURNED | TERMINATED
Returned-Question-IDs: <Q ids>
Clean-Returns: <count>
~~~

Each Thinker instance may contribute at most one Question-ID, or one `THINKER-CLEAN` return.

Thinkers do not own durable skill/memory state. Their parent applies `agent-context-foundation` placement/promotion rules to any material finding only when that skill is actually available; otherwise the parent persists ordinary canonical task state without claiming the missing skill's guarantees.

After termination, retain only the material question/evidence/result; never preserve thinker conversational memory as workflow state.

## Question registry

Material questions are first-class workflow objects.

A question should record:

- stable Question-ID;
- exact question;
- one-question Thinker/role source;
- why it matters;
- premise/decision owner;
- evidence needed;
- status;
- resolution and anchor;
- downstream artifacts that become stale if the answer changes a premise.

Duplicate questions should be merged, not counted as separate confidence.

## Plan reopening registry

For `references/plan-reopening.md` keep:

~~~text
PLAN-REOPENING

Reopening-ID: ...
Artifact: <plan anchor>
Started-From: <revision>
State: NOT_STARTED | ACTIVE | REVISION_REQUIRED | READY | BLOCKED | USER_DECISION
Thinker-Question-IDs: <ids>
Challenge-Pair: <pair id/status>
Alternative-Pair: <pair id/status>
Risk-Pair: <pair id/status or NOT_REQUIRED>
Material-Findings: <ids/anchors>
Alternative-Approaches: <anchors>
Decisions-Reopened: <ids>
Decisions-Preserved: <ids + evidence>
Plan-Revision: <anchor/status>
Remaining-Questions: <ids>
Disposition: EXECUTION_READY | REVISE_AGAIN | USER_DECISION | BLOCKED
~~~

A plan marked `MATURE` cannot be treated as `EXECUTION_READY` when required reopening is still active or unresolved.

## Council Session Registry

When the user requests specialist participation in the conversation:

~~~text
COUNCIL-SESSION

Council-ID: ...
Purpose: ...
Chair: orchestrator
Started-From: <state revision>
Visible-Participants: <agent instance ids/roles>
Host-Mode: DIRECT_MULTI_AGENT | ORCHESTRATOR_RELAY
Open-Questions: <ids>
Decisions-Made: <ids>
State: ACTIVE | COMPLETE | BLOCKED
~~~

Council participants keep their normal role boundaries. Council state is not permission to merge roles.

If host mode is `ORCHESTRATOR_RELAY`, Morrison must label specialist outputs truthfully and must not pretend users are directly connected to live subagents.

## Artifact freshness

Every canonical artifact depends on upstream decisions/evidence.

If a material premise changes:

1. mark dependent artifacts/gates `STALE`;
2. identify earliest owner that must re-evaluate;
3. mark affected pair synthesis stale;
4. invalidate relevant plan-reopening conclusions when necessary;
5. mark affected skill coverage stale and reactivate only relevant routes;
6. revalidate queued backlog items;
7. do not continue relying on stale approval because it existed earlier;
8. rerun only affected portions when possible.

## State update ownership

Morrison owns the overall orchestration record.

Children own their return artifacts/status but do not rewrite unrelated agents' state or advance global gates.

A delegated Work Owner managing children reports batch/pair/lifecycle/skill status upward so Morrison can keep the organization reconstructable.

## Revision discipline

Increment state revision for material changes such as:

- objective/task type changes;
- new/resolved material decision;
- material question opened/resolved;
- work owner change;
- stable agent spawned/terminated;
- dependency availability changes;
- required/conditional skill activated, blocked, completed or made stale;
- delegation batch created/committed/terminated;
- backlog item added/reclassified/dropped;
- pair group changes state;
- plan maturity/reopening state changes;
- council session opens/closes;
- gate passes/fails/becomes stale;
- canonical artifact is replaced.

Do not create noisy revisions for inconsequential formatting.

## Recovery after context loss

A fresh Morrison should recover by:

1. reading canonical orchestration state;
2. loading Orchestrator runtime plus pairing/batching/reopening, `references/installation-and-dependencies.md` and `references/skill-routing.md`;
3. reading only current artifacts and active role profiles;
4. re-resolving actual availability of required/active procedural skills and loading their current canonical sources;
5. identifying active/incomplete batch and pair groups;
6. terminating/recreating stale contexts as needed;
7. revalidating queued backlog;
8. continuing from `Next-Action`.

Do not reconstruct the task from raw chat history when canonical state already contains authoritative decisions.

## Completion state

Set `Current-Gate: COMPLETE` only when:

- current objective is satisfied;
- required gates passed;
- required pair groups resolved or valid exceptions exist;
- required plan reopening passed or valid exception exists;
- required dependency states are resolved and required skills were actually applied, or the affected path is explicitly outside/full-mode guarantees rather than falsely passed;
- applicable conditional skill routes are complete for current scope;
- no material paired contradiction remains;
- no open material question remains inside current scope;
- no required agent/batch is blocked/waiting;
- organizational backlog contains no required unfinished item inside scope;
- validation passed when required;
- user-authority decisions are resolved or explicitly deferred/outside scope;
- active child contexts no longer needed are terminated;
- council session is complete or intentionally closed.

## Core principle

**The organization may forget conversations and terminate entire batches; it must not forget state, dependency availability, questions, evidence, skill coverage, alternatives, risk, independence or ownership.**