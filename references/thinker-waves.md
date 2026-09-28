# Ephemeral Thinker Waves

## Purpose

A normal agent can plan a task well and still stop questioning its own frame once it has a plausible path forward.

Ephemeral Thinker Waves exist to repeatedly search for missing questions, hidden assumptions, uncovered branches, validation gaps, and unexamined failure modes before the workflow treats a stage as mature.

They are not another implementation team and they are not another approval panel. Their only job is to make the active workflow ask better questions.

## Core model

The host/orchestrator owns the durable workflow.

A Thinker Wave is a temporary set of isolated subagents created for one questioning round. Each thinker receives the current objective and enough primary/current evidence to inspect the problem, but does not inherit the conversational memory, chain of reasoning, or conclusions of previous thinker waves.

Each wave lives for one delivery only:

1. inspect the current objective and work product;
2. generate material unanswered questions and gaps;
3. return them to the orchestrator;
4. terminate.

After the workflow owners answer or incorporate those questions, the orchestrator may create a completely new wave against the newly updated state.

The new wave must start fresh. It must not be asked to continue the previous thinker's reasoning.

## Why the contexts are disposable

The point is not merely parallelism. The point is to reduce self-confirmation.

An agent that remembers how the previous review was framed can unconsciously keep searching inside the same boundaries. A fresh thinker should be able to rediscover the task from the current evidence and ask questions that the previous wave did not consider.

Therefore:

- do not reuse a thinker context for the next questioning round;
- do not give a new thinker the previous thinker's hidden reasoning or conversational transcript;
- do not tell the new thinker what it is expected to agree with;
- do not make the thinker defend previous questions;
- do not treat previous thinker output as authority.

Fresh context does not mean blind context. A thinker may read the current canonical Issue, current plan, current implementation state, current contracts, and current evidence required to understand the task. What must not be inherited is the previous thinker's reasoning history.

## Orchestrator responsibilities

The orchestrator is responsible for turning raw questioning into useful workflow pressure.

For each wave it must:

1. define the current objective or stage being questioned;
2. provide the current canonical work product and relevant evidence anchors;
3. spawn one or more isolated thinkers;
4. collect their questions independently;
5. deduplicate equivalent questions;
6. reject questions that are cosmetic, out of scope, already answered by current evidence, or non-material;
7. route each material question to the role that owns the premise;
8. require an evidence-backed answer, change, or explicit unresolved state;
9. update the canonical artifact/Issue state;
10. terminate the entire thinker wave;
11. spawn a fresh wave when another questioning round is required.

Thinkers never own the durable resolution. The existing workflow role that owns the questioned premise must answer it.

## Thinker contract

A thinker should optimize for coverage, not for producing a solution.

Its output should focus on questions such as:

- What are we assuming without evidence?
- What has to be true for this plan to work?
- What branch, state, caller, migration path, rollback path, concurrency path, or failure path is not represented?
- What happens before, during, and after the proposed change?
- What must be validated before implementation?
- What must be validated after implementation?
- Which contract defines the expected behavior?
- Which edge cases would force us to redesign this later?
- What evidence would falsify the current explanation?
- What dependency or side effect has not been modeled?
- Are we solving the observed symptom or the owning cause?
- What could make this plan technically correct but operationally incomplete?
- What would a future maintainer or caller need that the current design does not expose?

A thinker may also identify contradictions directly, but should express them as a question or gap that can be routed to an owner and resolved with evidence.

## Output format

Prefer compact, independently actionable records:

~~~text
THINKER-QUESTION

Question: <material question>
Why-It-Matters: <failure/rework risk if unanswered>
Premise-Owner: <agent-key or workflow owner when identifiable>
Evidence-Needed: <what would resolve the question>
Affected-Area: <plan | scope | contract | implementation | test | validation | other>
~~~

Do not pad the wave with generic brainstorming. A long list of weak questions is worse than a small set of material ones.

## Relationship to stable roles

Thinkers are not stable `Agent-Key` roles and do not participate directly in consensus.

They do not replace:

- Analyzer, which owns cause/scope analysis;
- Planner, which owns the repair design;
- Challenger, which adversarially attacks the proposed repair;
- Test Strategist, which owns falsifying verification cases;
- Validator, which independently evaluates the implemented result.

Instead, Thinker Waves can be inserted before a stage handoff or after a material revision to expose questions those roles must answer.

A thinker question has no authority by itself. Authority comes from the owning role's evidence-backed resolution and the normal workflow gates.

## Recommended insertion points

Use a fresh Thinker Wave when it materially reduces rework, especially:

1. after Analyzer believes cause and scope are complete, before Planner relies on them;
2. after Planner has a coherent repair, before Challenger/Test Strategist treat it as mature;
3. after a material plan or implementation revision;
4. before final consensus/closure when the change is broad, high-risk, or has already looped backward;
5. whenever the orchestrator detects that active agents are repeatedly refining the same frame without generating new questions.

Do not invoke waves as ritual after every tiny action. They are a coverage mechanism, not token-count theater.

## Re-questioning loop

The intended loop is:

~~~text
current canonical state
        ↓
spawn fresh Thinker Wave A
        ↓
collect + deduplicate material questions
        ↓
owners answer/change with evidence
        ↓
update canonical state
        ↓
destroy Wave A contexts
        ↓
spawn fresh Thinker Wave B
        ↓
search again from the updated state
        ↓
...
~~~

Each wave must be capable of disagreeing with the assumptions exposed by the previous result without having inherited the previous wave's conversation.

## Convergence gate

Do not loop forever merely because another question can always be invented.

A questioning cycle is converged when:

- no material thinker question remains unresolved; and
- a fresh wave produces no novel material gap that changes scope, design, verification, implementation, or risk handling.

For higher-risk work, the orchestrator may require two consecutive fresh waves with no novel material questions.

If fresh waves continue producing material new gaps beyond the configured review budget, do not force convergence. Keep the stage non-final and report it as QUESTIONING, INCONCLUSIVE, or BLOCKED as appropriate.

## Anti-patterns

Do not:

- reuse the same thinker for every round;
- ask the thinker to validate its own previous answer;
- preload the next wave with the previous wave's full reasoning;
- turn thinker questions into automatic requirements without owner review;
- count duplicate questions as additional confidence;
- ask thinkers to implement fixes while they are in questioning mode;
- let the orchestrator silently answer material questions that belong to another role;
- create permanent thinker state comments for disposable contexts;
- keep spawning waves after convergence only to increase pass counts.

## Design principle

The durable workflow should remember the resolved state.

The questioning agents should not remember how the previous questioning agent thought.

This intentionally separates **task memory** from **reviewer memory**: the project keeps the evidence and decisions it needs, while every new questioning wave receives a fresh opportunity to challenge the current result.