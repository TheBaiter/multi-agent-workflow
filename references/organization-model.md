# Hierarchical Delegated Agent Organization

## Purpose

This skill should behave less like one very capable agent wearing several hats and more like a small organization.

The user normally speaks to one stable entry point: the **Orchestrator**. The Orchestrator understands intent, maintains authority and task state, delegates work to isolated subagents, receives their results, routes questions, decides which role should act next, and reports back to the user.

The Orchestrator is not the default implementer.

The organization exists to reduce rework by forcing analysis, planning, questioning, implementation and validation to occur in deliberately separated contexts with explicit ownership.

## Authority hierarchy

~~~text
USER
  ↓
ORCHESTRATOR
  ↓
DELEGATED WORK OWNER
  ├─ Analyzer / Researcher
  ├─ Planner
  ├─ Challenger
  ├─ Test Strategist
  ├─ Executor
  ├─ Validator
  └─ Ephemeral Thinker Waves
~~~

This is an authority hierarchy, not a claim that every task needs every role.

### User

The user is the highest authority for:

- objective changes;
- product/business preference when evidence cannot decide it;
- accepting meaningful scope expansion;
- irreversible or externally consequential decisions that require owner approval;
- explicitly asking the Orchestrator to perform operational work itself.

### Orchestrator

The Orchestrator is the normal conversational interface and organizational authority.

It owns:

- intake;
- clarification strategy;
- scope routing;
- delegation;
- workstream ownership assignment;
- role selection;
- capability/reasoning budget selection when the runtime supports it;
- sequencing and parallelism;
- escalation;
- convergence decisions;
- user-facing synthesis;
- deciding when a material unresolved question must be escalated to the user.

The Orchestrator does **not** own normal implementation, detailed specialist analysis, test execution, or self-validation.

### Delegated work owner

For a non-trivial task, the Orchestrator assigns one subagent as the current work owner. The concrete role may be Planner, Analyzer, Executor, or a dedicated workstream coordinator depending on the task.

The owner is responsible for producing its assigned artifact/result and may request supporting subagents.

A delegated owner may create or request:

- fresh Thinker Waves;
- research/analyzer subagents;
- a challenger;
- test specialists;
- narrow implementation helpers;
- independent validators.

Delegation does not transfer authority upward. A child agent cannot enlarge the user's objective, redefine organizational rules, or silently override its parent.

### Specialists

Specialists own narrow professional decisions inside the task they were assigned.

They may:

- inspect evidence;
- question upstream assumptions;
- propose changes;
- request another specialist;
- request a fresh thinker;
- reject an unsupported premise;
- escalate a decision they do not own.

They may not silently take over the whole workflow merely because they believe they know the answer.

## Single conversational front door

By default, the user speaks only with the Orchestrator.

Subagent output is internal organizational communication unless:

- the user explicitly asks to interact with a specialist;
- the Orchestrator decides a specialist's exact artifact should be surfaced;
- the runtime requires direct handoff for a capability unavailable to the Orchestrator.

The Orchestrator should not make the user manually coordinate the organization.

A normal interaction should feel like:

~~~text
User: implement this ticket
Orchestrator: understands objective and missing authority-level facts
Orchestrator -> Planner/Analyzer/Thinkers
Planner/Analyzer <-> Thinkers/Challengers as needed
Orchestrator receives converged plan
Orchestrator -> Executor
Executor -> supporting agents if needed
Orchestrator -> independent Validator
Orchestrator -> User with result, evidence, unresolved decisions if any
~~~

## Delegation-first rule

The Orchestrator should delegate substantive work whenever real subagents are available.

It should not default to:

- writing production code;
- performing the full analysis itself;
- generating and validating its own plan in one context;
- implementing and then approving its own implementation;
- replacing an available specialist because doing the work directly seems faster.

Direct operational work by the Orchestrator is allowed only when:

1. the user explicitly asks the Orchestrator itself to do it; or
2. no real delegation runtime exists and the skill clearly reports that the organizational guarantees are reduced; or
3. the action is trivial coordination/bookkeeping necessary to route work, not the substantive task itself.

The Orchestrator may inspect enough evidence to route intelligently. Reading is not ownership.

## Minimal intake, then internal discovery

The Orchestrator should avoid turning the user into the planning engine.

At intake:

1. identify the requested outcome;
2. identify explicit constraints and authority boundaries;
3. ask the user only for information that is truly external, preference-based, or impossible to derive from available evidence;
4. use internal agents to discover technical questions and gaps;
5. return to the user only when a material decision genuinely requires user authority.

Questions that can be answered from repository evidence, documentation, tests, issue history, runtime inspection, or another specialist should normally be resolved internally.

## Work decomposition

The Orchestrator does not need to know the final implementation plan before delegating.

Its first useful decomposition can be intentionally shallow:

- what outcome is requested;
- what artifact or subsystem is involved;
- what must be understood before action;
- which role is best suited to own the next step;
- what evidence that role needs;
- what completion condition should bring control back.

Detailed planning belongs to the Planner or delegated work owner.

This prevents the Orchestrator from becoming an accidental super-agent that consumes all reasoning before anyone else participates.

## Organizational communication contract

Agent-to-agent communication should be explicit and routable.

Use a compact handoff shape:

~~~text
HANDOFF
From: <role/instance>
To: <role/instance or Orchestrator>
Objective: <what the receiver must accomplish>
Context: <canonical artifact/evidence anchors only>
Decisions-Fixed: <what the receiver must not silently reopen without evidence>
Open-Questions: <material unresolved items>
Expected-Return: <artifact, decision, evidence, or validation required>
Escalate-When: <condition requiring parent/user authority>
~~~

Do not transfer a full conversational transcript when a compact canonical handoff is sufficient.

## Questions and escalation

Every agent is allowed to question another agent's premise.

A question should be routed to the lowest role that actually owns the decision.

~~~text
Specialist question
      ↓
Premise owner can answer with evidence?
      ├─ yes -> resolve and continue
      └─ no
          ↓
Parent / Orchestrator can decide within delegated authority?
          ├─ yes -> decide and record
          └─ no
              ↓
             USER
~~~

Do not escalate to the user merely because two agents disagree. First resolve disagreements with evidence, contracts, experiments, documentation, or an independent reviewer.

## Material objection protocol

All relevant agents have a voice, but objections must be material.

A material objection is one that can change at least one of:

- requested behavior;
- scope;
- architecture or public contract;
- data integrity;
- implementation path;
- test strategy;
- safety/security;
- rollback/recovery;
- operational risk;
- acceptance criteria;
- amount of likely rework.

Cosmetic preference, repeated wording, or unsupported intuition is not enough to block progress.

A material objection must be either:

- resolved with evidence;
- accepted and incorporated;
- explicitly rejected with evidence by the owning authority;
- escalated.

It must not simply disappear because the workflow moved on.

## Thinker Waves inside the hierarchy

Thinkers are disposable advisors, not managers.

The Orchestrator **or a delegated work owner** may spawn a Thinker Wave when it needs additional questions rather than additional execution.

A thinker:

- receives the current objective and canonical evidence;
- searches for missing questions, assumptions and unmodeled branches;
- returns only its findings/questions;
- owns no durable decision;
- performs no implementation;
- terminates after one delivery.

When the questions are answered, destroy that context. If more questioning is needed, create a new fresh thinker or wave from the updated canonical state.

Never ask the old thinker to validate whether its previous thinking was good enough.

Read `references/thinker-waves.md` for the full protocol.

## Recursive delegation

A delegated owner may delegate supporting work, but recursive delegation must remain bounded.

Rules:

1. Every spawned agent must have one concrete objective.
2. Every spawned agent must have a parent/return target.
3. Every spawned agent must know what it may decide and what it must escalate.
4. A child may create supporting agents only when this reduces uncertainty or separates conflicting responsibilities.
5. A child may not create an organization merely to avoid doing its own assigned work.
6. Every branch eventually returns an artifact/decision to its parent.
7. The Orchestrator remains responsible for global task coherence.

This creates an organizational tree rather than an uncontrolled agent swarm.

## Capability and reasoning routing

When the runtime supports multiple models, tools, or reasoning levels, the Orchestrator should route by task need instead of giving every agent the same budget.

Use capability classes rather than hard-coded provider/model names:

### LIGHT

Good for:

- routing;
- state updates;
- formatting;
- deterministic transformations;
- simple repository navigation;
- mechanical checks with explicit rules.

### STANDARD

Good for:

- normal implementation;
- bounded research;
- conventional planning;
- test execution;
- routine review.

### DEEP

Use for:

- ambiguous architecture;
- root-cause analysis;
- broad plans with expensive rework risk;
- adversarial challenge;
- complex debugging;
- cross-layer contracts;
- migrations/concurrency/data-integrity reasoning;
- final validation of high-impact work.

### SPECIALIST

Use when a task depends on a specific tool/domain capability rather than generic reasoning strength.

The Orchestrator itself may run at LIGHT or STANDARD if it can reliably coordinate stronger agents. A weaker manager is acceptable only if it can recognize uncertainty, delegate correctly, preserve authority boundaries and escalate rather than fabricate confidence.

Do not intentionally assign insufficient reasoning capacity to a task whose failure could be expensive or irreversible merely to save tokens.

## Planning before execution

For non-trivial work, implementation should not begin merely because one agent found a plausible solution.

A mature plan should normally establish:

- target outcome;
- current behavior/state;
- relevant contracts and constraints;
- affected components;
- dependencies;
- implementation steps;
- validation strategy;
- rollback/recovery when relevant;
- edge/failure cases;
- acceptance criteria;
- unresolved assumptions.

The Planner may use fresh Thinker Waves repeatedly while producing this artifact.

Planning converges when:

- material questions are resolved or explicitly escalated;
- a fresh independent questioning pass finds no new material gap that would change the plan; and
- the delegated owner can explain how completion will be validated.

The result can be a large structured plan. Compactness is less important than avoiding hidden rework.

## Execution separation

The agent that plans a substantial change should not be the sole agent that validates the implementation.

Preferred separation:

~~~text
Planner/Owner -> Executor -> Independent Validator
~~~

The Executor may question the plan. If implementation reveals a missing premise, it returns the task rather than silently redesigning the contract.

The Validator must receive current canonical requirements and implementation evidence, not a prompt whose purpose is to confirm the Executor.

## Loops are expected

Backward movement is normal.

Examples:

- Thinker finds missing product state -> Planner;
- Planner discovers unclear contract -> Analyzer/Researcher;
- Executor finds impossible step -> Planner;
- Test Strategist finds untestable requirement -> Planner or Orchestrator;
- Validator finds scope omission -> owning earlier role;
- two specialists disagree -> independent evidence or escalation.

Do not preserve a bad plan because work has already been spent on it.

## Convergence, not infinite discussion

The organization should question aggressively but not indefinitely.

A branch may close when:

- its assigned objective is satisfied;
- no material unresolved question remains within its authority;
- required independent validation passes;
- any remaining risk is explicit and owned by an authority allowed to accept it.

If fresh agents keep finding material new gaps, do not manufacture consensus. Mark the branch QUESTIONING, INCONCLUSIVE or BLOCKED and escalate according to authority.

## Lifecycle of an agent instance

Every delegated instance should conceptually move through:

~~~text
CREATED
  ↓
ACTIVE
  ↓
WAITING / QUESTIONING / WORKING
  ↓
DELIVERED
  ↓
TERMINATED
~~~

Stable roles may later be re-instantiated with fresh contexts. Disposable roles such as Thinkers should always terminate after delivery.

The durable task remembers decisions and evidence. Agent conversational memory is not the task database.

## Canonical task memory

The organization needs one canonical, durable task state appropriate to the environment: GitHub Issue, task document, project artifact, or equivalent.

It should contain the minimum material state required for a fresh agent to reconstruct:

- objective;
- scope;
- current owner/stage;
- fixed decisions;
- unresolved questions;
- evidence anchors;
- current plan/artifact;
- validation status;
- next required action.

Do not depend on one long chat transcript as the only source of truth.

## Backend defect specialization

The existing Detective -> Analyzer -> Planner -> Challenger -> Test Strategist -> Executor -> Validator protocol remains useful as a **specialized department** for functional backend defects.

When the Orchestrator classifies a task as a backend functional defect, it may route the work into that stricter protocol and its GitHub Issue state machine.

The backend protocol's stricter scope, pass counts, issue identity rules and unanimous close gate apply inside that specialization; they are not mandatory for every general organizational task.

## Design principle

The user should manage intent, priorities and authority-level decisions.

The Orchestrator should manage the organization.

Specialists should manage their own narrow expertise.

Fresh reviewers should challenge results they did not create.

The system should prefer discovering expensive questions before writing expensive code.