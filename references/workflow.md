# Historical Functional Backend Defect Workflow

## Scope

This document governs the **historical specialized functional-backend-defect department** only.

It does not define the normal general organization. Morrison enters this workflow only when `references/scope.md` classifies the task as an in-scope functional backend defect.

## Normal direction

```text
1 Detective
  -> 2 Analyzer
  -> 3 Planner
  -> 4 Challenger
  -> 5 Test Strategist
  -> 6 Implementation
       - AGENT_EXECUTOR -> Executor / Reducer
       - MANUAL_OWNER   -> Human / repository owner
  -> 7 Final Validator
  -> 8 Consensus / Close
```

This is the normal dependency direction, not a guarantee that work never returns upstream.

## Core rule

Every downstream role may question upstream conclusions.

Prior approval is evidence of earlier review, not immunity from new evidence.

Historical Agent-Keys remain specialized and are not aliases for general roles.

## Pass semantics

Configured passes/cycles represent distinct investigation purposes.

They do not mean:

- repeat the same prompt;
- restate the same conclusion;
- search the same files mechanically;
- force APPROVED because the configured count was reached.

A role may complete its passes and still return `REJECTED`, `INCONCLUSIVE` or `BLOCKED`.

## Independent cycle semantics

When a project configuration gives a historical role multiple review cycles:

- Cycle A performs the normal role investigation;
- Cycle B reconstructs from canonical/primary evidence and actively tries to disprove Cycle A;
- Cycle B must not start from "Cycle A is probably right";
- later cycles must search a materially different cause/path/configuration/data state/contract interpretation/counterexample when relevant;
- one explicit synthesis compares the independent cycle artifacts.

### Runtime-context rule

A logical cycle does **not** require keeping the previous runtime context alive.

Prefer fresh instances from the authoritative Issue/task evidence when independence or slot pressure makes that safer.

If an old specialized profile says `reactivate`, `wake`, or `remain dormant`, interpret that as **reactivate the logical role**, not necessarily resume the same model context.

Completed runtime contexts should normally terminate after their durable checkpoint.

## Thinker Waves inside the historical workflow

Morrison may insert temporary Thinkers before a stage handoff or after a material revision.

Thinkers obey the global current contract:

**one Thinker = one strongest material question (or clean) = terminate.**

A wave may contain several fresh isolated Thinkers when capacity permits, but each individual Thinker returns at most one question.

Workflow:

```text
current canonical Issue/state
  -> fresh one-question Thinkers
  -> each returns THINKER-QUESTION or THINKER-CLEAN
  -> all Thinker contexts terminate
  -> Morrison deduplicates/materiality-filters
  -> surviving questions receive Question-IDs and premise owners
  -> stable owner updates evidence/artifact/state
  -> new fresh wave only if useful
```

Thinkers never approve, implement, validate, answer their own question or maintain durable memory.

Use `references/thinker-waves.md` for the current canonical Thinker contract.

## Stage handoff gate

A historical role does not hand work forward merely because one pass is persuasive.

For a configured fixed-pass role, downstream work normally begins only when:

1. configured differentiated passes/cycles are complete;
2. its durable state says `Assessment-Maturity: FINAL` when that field applies;
3. terminal decision/reason/evidence is recorded in the authoritative Issue/task state.

Before that, downstream roles remain waiting/provisional and may only inspect durable provisional findings or route material questions.

Project-specific orchestration may increase pass count. The configured count then becomes that workflow instance's gate; count alone never implies approval.

## Dormancy means logical addressability, not a zombie context

When a historical role completes/approves its stage, the **logical role becomes dormant for the Issue**.

Dormant means:

- its durable artifact/state remains addressable by Agent-Key;
- its runtime child context may and normally should terminate;
- it does not recompute/comment merely because downstream work is active;
- it can be instantiated fresh later if a directed question/new evidence requires that profession again.

Wake/reactivate the logical role only when:

- a directed question targets its Agent-Key;
- material new evidence affects one of its decisions;
- a test fails against its premise;
- implementation diverges from its owned premise;
- a later stage explicitly returns the case.

When reactivated, prefer a **fresh instance** reconstructed from authoritative Issue/task evidence rather than a dormant hidden conversation.

Never keep a child alive solely as memory.

## Backward return

Any later stage can return to the owner of a failed premise.

Examples:

- Validator discovers expected behavior may actually be intentional -> Detective/Analyzer;
- Test Strategist finds scope not modeled -> Analyzer;
- Challenger finds an unhandled repair branch -> Planner;
- Executor cannot implement without changing a planned premise -> Planner and possibly Analyzer;
- Manual owner cannot implement plan as written -> Planner and possibly Analyzer;
- Validator finds implementation diverges from plan -> Executor in AGENT_EXECUTOR mode or manual owner in MANUAL_OWNER mode.

A backward return marks downstream conclusions that depended on the changed premise stale.

Re-evaluate only affected downstream stages after the premise owner updates canonical state.

## Slot/batch behavior

Historical workflow roles use the same global runtime capacity discipline:

- do not assume fixed concurrency;
- persist each role/cycle result to the authoritative Issue before terminating its context;
- use the durable Issue/state as continuity between stages;
- do not keep all seven personalities alive simultaneously;
- if same-role independent paired/cycle work is configured, use current `references/paired-delegation.md` and `references/batched-delegation.md` semantics where compatible with this historical protocol.

The historical stage order describes **logical ownership**, not simultaneous live agents.

## Cost principle

Do not continue a wrong path because it was expensive.

Tokens spent, passes completed, implemented lines or prior approvals are not evidence.

## Efficiency principle

The workflow is intentionally strict but should avoid waste:

- load only current stage/profile plus required shared contracts;
- reuse authoritative Issue evidence;
- use differentiated passes/cycles;
- checkpoint durable state compactly;
- reactivate only affected logical roles;
- terminate completed runtime contexts;
- do not rediscover evidence already anchored unless freshness is required.

## Manual implementation mode

When `Execution-Mode: MANUAL_OWNER`:

1. Test Strategist finishes/records the verification contract.
2. Workflow enters `WAITING_FOR_MANUAL_IMPLEMENTATION`.
3. No agent edits production source on behalf of Executor.
4. Repository owner implements.
5. Issue receives durable `MANUAL_IMPLEMENTATION` handoff identifying exact code state.
6. A fresh Validator instance validates that implementation.
7. Implementation-only defects return to manual owner rather than Executor.
8. Plan/scope/test defects return to the owning historical role normally.

Manual ownership removes automated implementation; it does not remove evidence, test or independent-validation requirements.

## Cross-session continuity

Never assume a later execution shares hidden context with an earlier one.

The authoritative Issue/task must expose enough state to reconstruct:

- current stage;
- role decisions/evidence;
- waiting/blocking condition;
- directed questions;
- implementation mode/state;
- validation state;
- next action.

A role checkpoint is updated when that logical role actually executes or materially transitions. A terminated/dormant role does **not** need a live agent repeatedly refreshing comments merely to prove it is dormant.

Waiting/dormancy is represented durably in state, not by keeping a context alive or by periodic no-op execution.

## Relationship to general MAW

General organization contracts still govern:

- dependency preflight;
- agent-context-foundation usage;
- durable state/memory discipline;
- one-question Thinkers;
- truthful runtime capacity;
- no zombie contexts;
- user authority and Morrison as manager.

Historical defect-specific contracts remain authoritative for:

- defect scope/admission;
- specialized Agent-Key responsibilities;
- Issue protocol/events;
- evidence policy;
- stage-specific pass semantics;
- consensus/closure rules.

## Core principle

**Historical roles remain logically addressable through durable Issue state; their runtime contexts are disposable. Wake the profession when evidence requires it, not the old conversation.**