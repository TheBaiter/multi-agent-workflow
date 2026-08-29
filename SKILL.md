---
name: multi-agent-workflow
description: Find, challenge, fix, and validate functional backend defects with independent subagents that maintain auditable GitHub Issue state, question one another, and require unanimous evidence-backed approval before closure. Use for backend behavior, persistence, migrations, state, contracts, transactions, or data-integrity bugs; not for frontend, generic refactors, code cleanup, or architecture improvements without a demonstrated functional defect.
---

# Multi-Agent Workflow

## Purpose

Investigate and repair real functional backend defects without allowing one agent's early hypothesis to become unquestioned truth.

Use real subagents with separate contexts. Do not simulate the entire organization as several personas inside one uninterrupted reasoning chain when the host can delegate to actual subagents.

## Runtime Requirements

The full workflow requires:

- a host capable of delegating to real subagents or equivalent isolated agent contexts;
- authenticated read/write access to the repository's GitHub Issues through any supported integration, CLI, or tool;
- access to the repository evidence required by the active role.

If real subagents are unavailable, do not simulate all roles inside one reasoning context.

If the authoritative Issue cannot be read or updated, do not create a private parallel state system.

In either case, report the workflow as BLOCKED or unsupported for the current runtime rather than claiming the multi-agent protocol was executed.

## Hard Scope Boundary

This skill handles **functional backend correctness**.

Read references/scope.md before opening or accepting a candidate Issue.

Reject work that is only:

- frontend or visual;
- simplification;
- code style;
- naming;
- generic refactoring;
- duplication cleanup;
- performance tuning without correctness impact;
- architectural instability without a demonstrated functional defect.

A structural, migration, architecture, or data concern is relevant only when it produces or plausibly explains a concrete backend functional failure.

## Companion Context Skill

This repository is organized using **$agent-context-foundation** from:
https://github.com/TheBaiter/agent-context-foundation

Use it when available to establish repository context, canonical owners, progressive disclosure, project organization, and durable task trace rules.

Read references/agent-context-foundation.md for the boundary between both skills and the canonical ownership map used by this skill.

Do not duplicate per-Issue investigation history into durable Agent/ documentation.

## Operating Model

The Issue is the shared case file.

Each required role:

1. reads the Issue and relevant repository evidence;
2. loads only its own profile from references/profiles/<agent-key>/PROFILE.md;
3. finds or creates its unique state comment by Agent-Key;
4. performs its distinct passes;
5. records material questions and decisions as permanent event comments;
6. updates only its own state comment;
7. approves, rejects, waits, blocks, or reopens with explicit reason and evidence.

Read references/issue-protocol.md for exact comment ownership and communication rules.

Read references/evidence-policy.md whenever a role proposes, evaluates, executes, or accepts a test case. Documentation-backed validation is valid when authoritative documentation fully resolves the relevant behavior; execution is not mandatory ritual.

## Role Router

| Order | Agent-Key | Profile | Primary responsibility |
| --- | --- | --- | --- |
| 1 | detective | references/profiles/detective/PROFILE.md | discover a candidate backend functional defect |
| 2 | analyzer | references/profiles/analyzer/PROFILE.md | confirm defect, cause, origin, and scope |
| 3 | planner | references/profiles/planner/PROFILE.md | design the smallest coherent repair |
| 4 | challenger | references/profiles/challenger/PROFILE.md | attack assumptions, scope, and proposed repair |
| 5 | test-strategist | references/profiles/test-strategist/PROFILE.md | create and evaluate falsifying test cases |
| 6 | executor | references/profiles/executor/PROFILE.md | implement and reduce the change |
| 7 | validator | references/profiles/validator/PROFILE.md | independently challenge the final result |
| 8 | close gate | references/consensus.md | close only on unanimous evidence-backed approval |

Do not load every profile into every subagent. Load the profile owned by the current subagent and only the shared references required for its next decision.

## Non-Linear Workflow

The numbered order is the normal direction, not a one-way pipeline.

Any later role may challenge an earlier role. If the challenge is material, the owner of that decision reopens and answers it.

A failure at validation may return to executor, test strategy, challenger, planner, analyzer, or detective depending on which premise failed.

Read references/workflow.md and references/state-machine.md.

## Required Passes

Pass counts are differentiated investigations, not repeated prompts.

- detective: unbounded discovery across candidate defects; one candidate Issue is then handed forward;
- analyzer: 8 distinct passes;
- planner: 5 distinct passes;
- challenger: 3 distinct passes;
- test-strategist: 5 distinct passes;
- executor: variable, bounded by the approved plan and smallest coherent implementation;
- validator: 10 distinct passes.

Completing the number does not force approval. An agent may end REJECTED, INCONCLUSIVE, BLOCKED, or return the case backward.

After approval, become dormant. Wake only for a directed question, material new evidence, explicit return, test failure, or implementation divergence.

## Decision Contract

Every material approval, rejection, question resolution, or backward return must state:

- DECISION: what the agent decides;
- REASON: why;
- EVIDENCE: precise anchors supporting it;
- IMPACT: what changes in the workflow.

Do not use bare agreement such as "LGTM", "looks fine", or equivalent.

## Issue Identity Contract

All subagents may operate through the same GitHub account.

GitHub account identity is therefore not agent identity.

Each state comment must contain a stable Agent-Key and a human-readable agent name. Locate state by Agent-Key, not by author and not by remembering comment_id.

An agent may read every comment but may edit only the single state comment whose Agent-Key equals its own.

If zero matching state comments exist, create one.
If exactly one exists, update it.
If more than one exists, declare STATE_CONFLICT and do not overwrite any of them.

## Consensus Gate

Do not close an Issue because the last role approves.

Close only when the current state of every required Agent-Key is APPROVED, every approval has a reason and evidence, no directed question remains unresolved, and no state is stale due to material new evidence.

Read references/consensus.md before closure.

## Durable Knowledge Boundary

Per-Issue chronology stays in the Issue.

Promote only verified reusable knowledge into repository context, following agent-context-foundation when present.

The skill must remain evidence-driven, auditable, non-linear, and willing to discard expensive prior work when later evidence disproves it.
