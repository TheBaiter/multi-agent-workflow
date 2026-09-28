# Canonical Orchestration State

## Purpose

The Orchestrator must not rely on its conversational memory to remember the organization.

Every non-trivial multi-agent task should have one canonical orchestration state that allows a fresh Orchestrator to reconstruct:

- what the user wants;
- what has already been decided;
- which department/roles are active;
- which child agents exist and who owns them;
- what each child is doing and waiting for;
- which artifacts are current;
- which material questions remain open;
- which gate must pass next.

This state may live in a GitHub Issue, task document, structured runtime state, or another durable artifact appropriate to the environment.

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
Current-Gate: <INTAKE | PRODUCT | PLAN | EXECUTION | VALIDATION | USER_DECISION | COMPLETE | BLOCKED>
Current-Owner: <Agent-Key or USER>

Constraints:
- ...

Fixed-Decisions:
- Decision: ...
  Owner: ...
  Evidence/Authority: ...

Open-Material-Questions:
- Question-ID: Q-...
  Question: ...
  Owner: ...
  Status: OPEN | ROUTED | ANSWERED | BLOCKED
  Impact: ...

Canonical-Artifacts:
- Product-Brief: <anchor/status>
- Technical-Plan: <anchor/status>
- Verification-Contract: <anchor/status>
- Implementation: <anchor/status>
- Validation-Report: <anchor/status>

Active-Agents:
- <Agent Instance Registry entries>

Terminated-Agents:
- <instance + role + final return anchor; compact only>

Gate-Status:
- Product: NOT_REQUIRED | OPEN | PASSED | STALE
- Plan: NOT_REQUIRED | OPEN | PASSED | STALE
- Execution: NOT_REQUIRED | OPEN | PASSED | STALE
- Validation: NOT_REQUIRED | OPEN | PASSED | FAILED | BLOCKED | STALE

Next-Action:
<one concrete organizational action>
~~~

Not every storage system must serialize exactly this text. The logical fields are the contract.

## Agent Instance Registry

For every active stable child, keep a reconstructable entry:

~~~text
AGENT-INSTANCE

Agent-Instance: <unique id>
Agent-Key: <stable profile key>
Parent: <agent instance / orchestrator>
Reasoning-Class: LIGHT | STANDARD | DEEP | MAX
Lifecycle-State: CREATED | WORKING | QUESTIONING | WAITING_PARENT | WAITING_CHILD | BLOCKED | RETURNED_COMPLETE | RETURNED_INCONCLUSIVE | RETURNED_REJECTED
Objective: <one-line objective>
Expected-Return: <artifact>
Waiting-On: <question/agent/evidence or NONE>
Spawn-Permission: NONE | THINKERS_ONLY | NAMED_SUPPORT_ROLES | DELEGATED_OWNER
Started-From: <canonical state revision/artifact anchors>
Last-Checkpoint: <timestamp/revision when available>
~~~

The full child contract remains the Agent Manifest. The registry is the compact operational view.

## Thinker registry

Thinkers are temporary and should not become durable pseudo-employees.

While a wave is active, the orchestration state may record:

~~~text
THINKER-WAVE
Wave-ID: ...
Parent: ...
Objective: ...
Started-From: <state revision>
State: WORKING | RETURNED
Return-Anchor: ...
~~~

After termination, retain only enough evidence to preserve material questions/results in canonical artifacts. Do not preserve thinker conversational memory as workflow state.

## Question registry

Material questions are first-class workflow objects because unanswered questions are one of the main sources of avoidable rework.

A material question should record:

- stable Question-ID;
- question text;
- why it matters;
- premise/decision owner;
- evidence needed;
- current status;
- resolution and anchor when answered;
- which downstream artifacts become stale if the answer changes a premise.

Duplicate questions should be merged, not counted as separate confidence.

## Artifact freshness

Every canonical artifact should be understood relative to the decisions/evidence it depends on.

If a material upstream premise changes:

1. mark dependent downstream artifacts/gates `STALE`;
2. identify the earliest owner that must re-evaluate;
3. do not continue relying on a stale approval merely because it existed earlier;
4. re-run only the affected portions when possible.

Examples:

- Product Brief changes a required user role -> Technical Plan may become STALE;
- Technical Plan changes authorization boundary -> Verification Contract and implementation may become STALE;
- implementation diverges from plan -> Validation target must use the real implementation and plan question returns upstream.

## State update ownership

The Orchestrator owns the overall orchestration record.

Children own their return artifacts and may report their own status, but they do not rewrite other agents' state or silently advance global gates.

When a delegated Work Owner manages permitted children, it reports child lifecycle/status upward so the Orchestrator can keep the canonical organization reconstructable.

## Revision discipline

Increment state revision for material organizational change, such as:

- objective/task type changes;
- new material decision;
- material question opened/resolved;
- work owner changes;
- stable agent spawned/terminated;
- gate passes/fails/becomes stale;
- canonical artifact replaced by a new authoritative version.

Do not create noisy revisions for inconsequential formatting.

## Recovery after context loss

A fresh Orchestrator should be able to recover by:

1. reading the canonical orchestration state;
2. loading the Orchestrator profile/runtime;
3. reading only current canonical artifacts and active role profiles;
4. identifying stale/active child contexts;
5. terminating or recreating contexts as needed;
6. continuing from `Next-Action`.

Do not reconstruct the task from raw chat history if the canonical state already contains the authoritative decisions.

## Completion state

Set `Current-Gate: COMPLETE` only when:

- current objective is satisfied;
- required gates are passed;
- no open material question remains inside current scope;
- no required agent remains BLOCKED/QUESTIONING/WAITING;
- validation is passed when required;
- user-authority decisions are either resolved or explicitly outside/deferred from current scope;
- active child contexts no longer required for the task are terminated.

## Core principle

**The organization may forget conversations; it must not forget state.**

Agent contexts are disposable. Canonical decisions, questions, artifacts, ownership and evidence are durable.