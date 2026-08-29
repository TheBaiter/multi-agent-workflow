---
name: multi-agent-workflow
description: Orchestrates real subagents through iterative, evidence-seeking review loops instead of a single linear plan. Use when detecting, validating, scoping, planning, implementing, or reviewing changes where false positives, incomplete scope, planning gaps, propagated assumptions, or regression risk must be challenged before advancing.
---

# Multi-Agent Workflow

## Purpose

Use this skill to reduce error propagation in complex agent workflows by separating responsibilities across real subagents and requiring important conclusions to survive independent review.

The workflow is intentionally not a one-shot chain. A plausible conclusion from one agent is an input hypothesis for the next stage, not established truth.

## Core requirements

1. **Use real subagents.**
   Delegate work into separate agent contexts when the host supports subagents. Do not simulate the full workflow as several personas inside one uninterrupted reasoning chain.

2. **Keep one primary objective per subagent.**
   Avoid assigning detection, diagnosis, scoping, planning, implementation, and validation to the same worker.

3. **Allow lightweight initial detection.**
   The detector may perform a direct first pass and emit a candidate issue. Detection alone does not confirm the incident.

4. **Do not perform downstream stages in one linear pass.**
   Validation, scoping, root-cause analysis, planning, and later review must revisit their subject through multiple evidence-seeking passes before producing a strong conclusion.

5. **Treat inherited conclusions as hypotheses.**
   A downstream subagent must be allowed to confirm, refine, expand, contradict, or reject the previous stage.

6. **Prefer falsification over agreement.**
   Include passes whose explicit purpose is to find counterexamples, alternative explanations, hidden dependencies, missing scope, or evidence that the current interpretation is wrong.

7. **Persist each meaningful pass.**
   Do not keep critical investigation only in temporary agent context. Record enough information for another agent to audit what happened.

8. **Do not force completion.**
   If critical uncertainty remains, return an inconclusive or rejected state rather than manufacturing confidence to keep the workflow moving.

## Evidence record

Until a more specific artifact contract is defined, each meaningful investigation pass should preserve at least:

- objective of the pass;
- actions or sources inspected;
- evidence found;
- contradictions or counterevidence;
- unresolved questions;
- resulting conclusion or state.

A later subagent should be able to understand why a conclusion exists without relying on hidden reasoning from a previous agent.

## Working model

The current model is deliberately incomplete.

Conceptually:

```text
candidate detection
        ↓
iterative validation
        ↓
iterative scope / understanding
        ↓
iterative planning
        ↓
future implementation + adversarial validation stages
```

Each transition is a gate, not an automatic handoff.

A stage may return backward, broaden the investigation, reject the candidate, or remain inconclusive.

## Cost model

This workflow deliberately trades speed and compute cost for additional independent scrutiny.

Do not optimize by removing the independent checks that provide the safety benefit. Optimize by:

- giving subagents narrow objectives;
- limiting context to what each objective needs;
- avoiding duplicate passes that seek the same evidence;
- recording results so later agents do not need to rediscover everything;
- spending additional passes where uncertainty or blast radius is highest.

## Current design boundary

This initial version does **not** define:

- the final roster or names of subagents;
- an exact minimum number of passes per stage;
- final confidence scoring;
- final approval/rejection schemas;
- the orchestrator state machine;
- implementation permissions;
- final QA and regression protocols.

Do not invent those as permanent rules. They remain design decisions for future versions of this skill.
