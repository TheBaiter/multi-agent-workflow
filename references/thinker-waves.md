# Ephemeral Thinker Waves

## Purpose

A normal agent can plan a task well and still stop questioning its own frame once it has a plausible path forward.

Ephemeral Thinker Waves repeatedly search for missing questions, hidden assumptions, uncovered branches, validation gaps, unnatural user flows, avoidable rework and unexamined failure modes before a stage is treated as mature.

They are not an implementation team, another planner or an approval panel. Their only job is to make the active workflow ask better questions.

## Core rule: one thinker, one question, then terminate

A Thinker instance is intentionally tiny and disposable.

Each Thinker receives the current objective and canonical evidence, independently discovers the **single strongest material unanswered question** it can find, returns exactly one `THINKER-QUESTION`, and terminates.

Do not ask one Thinker to produce a long checklist. If more coverage is needed, create more fresh Thinkers, potentially across several batches/waves.

This keeps each context narrow, reduces cognitive accumulation and prevents a questioning agent from gradually becoming a planner or long-lived reviewer.

Lifecycle:

~~~text
CREATED
  ↓
WORKING
  ↓
ONE MATERIAL QUESTION
  ↓
RETURNED
  ↓
TERMINATED
~~~

## Wave model

A Thinker Wave is a temporary batch of isolated one-question Thinkers created for one questioning round.

For non-trivial work, use at least two fresh Thinkers when capacity permits. When more coverage is valuable, use additional Thinkers in the same or later batches under `references/batched-delegation.md`.

Each thinker:

1. inspects the same current objective and canonical work product;
2. chooses one strongest material gap/question independently;
3. returns one question record;
4. terminates immediately.

After owners answer/incorporate those questions, create a completely fresh wave against the updated state when another round is useful.

The new wave must not continue the previous Thinker's reasoning.

## Why the contexts are disposable

The point is not merely parallelism. The point is to reduce self-confirmation and context saturation.

A reviewer that remembers all previous questioning can unconsciously keep searching inside the same frame. A fresh Thinker should be able to rediscover the task from current evidence and ask something the previous context did not.

Therefore:

- do not reuse a Thinker context for another question;
- do not ask a Thinker to answer its own question;
- do not keep it waiting while an owner resolves the question;
- do not preload a new Thinker with previous hidden reasoning;
- do not make a Thinker defend an earlier Thinker's question;
- do not turn previous Thinker output into authority;
- do not let Thinkers plan, implement or validate as owners.

Fresh context does not mean blind context. A Thinker may read current canonical state, plans, implementation evidence, contracts and decisions required to understand the task. What it must not inherit is reviewer reasoning history.

## Orchestrator responsibilities

For each wave, the Orchestrator or delegated owner must:

1. define the stage/artifact being questioned;
2. provide current canonical evidence anchors;
3. choose an appropriate number of Thinker slots without exceeding runtime capacity;
4. create fresh isolated one-question Thinkers;
5. collect their questions independently;
6. deduplicate equivalent questions;
7. reject cosmetic, already-answered, out-of-scope or non-material questions;
8. assign a stable Question-ID to every surviving material question;
9. route each question to the lowest role that owns the premise;
10. require an evidence-backed answer/change/explicit unresolved state;
11. update canonical artifacts/state;
12. ensure all Thinkers from the wave are terminated;
13. create a fresh wave if another questioning round is warranted.

Thinkers never own durable resolution.

## Thinker contract

A Thinker optimizes for discovering **one high-value blind spot**.

Good question families include:

- What are we assuming without evidence?
- What has to be true for this plan to work?
- What normal user behavior or familiar flow does this plan ignore?
- What step would feel awkward, surprising or unnecessarily difficult to a user?
- What obvious adjacent requirement is likely to force immediate rework?
- What branch, state, caller, migration path, rollback path, concurrency path or failure path is missing?
- What happens before, during and after the proposed change?
- What must be validated before implementation?
- Which contract defines the expected behavior?
- Which edge case would force redesign later?
- What evidence would falsify the current explanation?
- What dependency or side effect is not modeled?
- Are we solving the symptom instead of the owning cause?
- What could make this technically correct but operationally incomplete?
- What would a future maintainer/caller need that the design does not expose?
- Could the same objective be achieved much more simply or naturally?
- What are we not considering because the artifact already looks finished?

The Thinker should select only the most material question it can justify from its assigned context.

## Output format

Every instance returns exactly one record:

~~~text
THINKER-QUESTION

Question: <one material question>
Why-It-Matters: <failure/rework/user-cost if unanswered>
Premise-Owner: <agent-key/authority when identifiable>
Evidence-Needed: <what would resolve it>
Affected-Area: <product | plan | UX | architecture | contract | implementation | test | validation | risk | other>
Novelty: NOVEL | POSSIBLE_DUPLICATE
~~~

If the Thinker cannot find a material question, return:

~~~text
THINKER-CLEAN
No-Material-Novel-Question: YES
~~~

and terminate.

## Relationship to stable roles

Thinkers are not stable `Agent-Key` roles and do not participate directly in consensus.

They do not replace:

- Product/technical/domain planners, which own plans;
- `review-challenger`, which tries to falsify a mature artifact;
- `alternative-planner`, which constructs a materially different viable plan;
- `risk-reviewer`, which maps downside/rework risk;
- QA/quality roles, which own verification strategy;
- validators, which evaluate delivered state.

A Thinker only exposes one question. The owning role must resolve it.

## Recommended insertion points

Use fresh one-question waves when they materially reduce rework, especially:

1. during idea/product maturation;
2. after a planning pair thinks its artifact is coherent;
3. before the `plan-reopening` gate;
4. after a material plan revision;
5. when multiple agents keep refining the same frame without discovering new branches;
6. before final execution readiness for broad/high-risk work;
7. after implementation reveals a premise that planning missed.

Do not invoke Thinkers as ritual after every tiny action.

## Re-questioning loop

~~~text
current canonical state
        ↓
Wave N: fresh one-question Thinkers
        ↓
collect + deduplicate material questions
        ↓
terminate every Thinker immediately
        ↓
owners answer/change with evidence
        ↓
update canonical state
        ↓
Wave N+1: entirely new Thinkers
        ↓
...
~~~

The task remembers resolved state. Thinkers do not.

## Batched execution under slot limits

When the host cannot run all desired Thinkers and specialist pairs simultaneously, use `references/batched-delegation.md`.

Example:

~~~text
Batch 1
  Thinker-1 -> Q-1 -> terminate
  Thinker-2 -> Q-2 -> terminate
  Product Planner A+B -> Product Brief -> terminate

persist questions + Product Brief + backlog

Batch 2
  new Thinker-3 -> Q-3 -> terminate
  new Thinker-4 -> CLEAN -> terminate
  UX Planner A+B -> UX Plan -> terminate
~~~

Do not keep completed Thinkers alive waiting for later batches.

## Convergence gate

A questioning cycle converges when:

- no material Thinker question remains unresolved; and
- a fresh wave produces no novel material question that would change scope, plan, UX, verification, implementation or risk handling.

For higher-risk work, require two consecutive fresh waves/batches with no novel material question if capacity/time allows.

If fresh Thinkers keep finding material new gaps beyond the configured review budget, do not manufacture consensus. Keep the stage `QUESTIONING`, `INCONCLUSIVE` or `BLOCKED` and route/escalate appropriately.

## Anti-patterns

Do not:

- let one Thinker produce many questions;
- reuse one Thinker for multiple questions or rounds;
- ask a Thinker to answer or validate its own question;
- keep a Thinker alive as task memory;
- preload a new Thinker with prior hidden reviewer reasoning;
- turn a Thinker into planner/executor/validator;
- treat Thinker questions as automatic requirements;
- count duplicate questions as confidence;
- keep spawning waves after convergence only to inflate pass counts.

## Design principle

**One Thinker discovers one material question and dies. The durable workflow remembers the question, evidence and resolution; the questioning context does not.**