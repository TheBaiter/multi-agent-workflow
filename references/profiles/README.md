# Agent Profiles

Each subdirectory owns one stable role's identity, operational personality, knowledge boundary, approval meaning, and reactivation rules.

The profile filename is always `PROFILE.md`.

## Organizational identities

The organization uses human-readable identities from **Devil May Cry** while protocol behavior depends on stable `Agent-Key` values.

Human-readable names may change later. Agent-Key values are protocol identifiers and should remain stable.

| Agent-Key | Display identity | Role |
| --- | --- | --- |
| orchestrator | Morrison | Organizational Orchestrator / Manager |
| product-planner | Kyrie | Product / Scope Planner |
| detective | Dante Sparda | Backend Defect Detective |
| analyzer | Vergil | Analyzer |
| planner | V | Technical Planner |
| challenger | Lady | Challenger |
| test-strategist | Nico Goldstein | Test Strategist |
| executor | Nero | Executor / Reducer |
| validator | Trish | Final Validator |

Thinkers are intentionally **not** stable Agent-Key roles. They are disposable contexts governed by `references/thinker-waves.md` and terminate after one questioning delivery.

Do not reuse an Agent-Key for a different role.

## Organization-level roles

### Orchestrator

`references/profiles/orchestrator/PROFILE.md`

The Orchestrator is the normal user-facing entry point. It manages delegation, sequencing, authority, escalation, capability routing, and convergence.

It is not the default implementer.

### Product Planner

`references/profiles/product-planner/PROFILE.md`

The Product Planner matures broad ideas and major feature directions before detailed technical planning. It owns the Product Brief and requirement classification (`NOW`, `FOUNDATION`, `DEFERRED`, `OPTION`, `REJECTED`).

Read `references/idea-maturation.md` with this profile.

## Technical and specialized roles

The remaining profiles may participate in general work when their responsibility fits, and some also participate in the stricter backend-defect specialization.

- `analyzer`: investigate evidence, cause, scope, contracts, unknowns;
- `planner`: produce coherent technical implementation/repair plans;
- `challenger`: attack assumptions and expose contradictions;
- `test-strategist`: define falsifying verification and acceptance cases;
- `executor`: perform delegated implementation;
- `validator`: independently evaluate the implemented result;
- `detective`: specialized discovery role for functional backend defects.

## Backend defect specialization

When the Orchestrator routes a task into the strict functional-backend-defect department, the specialized sequence is:

`detective -> analyzer -> planner -> challenger -> test-strategist -> executor/manual owner -> validator -> consensus`

The strict Issue/state/event/pass rules for that specialization remain defined in the shared references.

Do not apply those fixed backend pass counts mechanically to every general product/software task.

## Editing a personality

When tuning one role:

- edit only that role's `PROFILE.md` unless a shared protocol truly changes;
- keep the primary responsibility narrow;
- preserve explicit forbidden actions;
- preserve organization authority boundaries;
- avoid turning it into a duplicate of another role;
- change the display name freely if desired, but change Agent-Key only as a breaking protocol migration.

## Profile contract

Each profile owns role-local behavior:

- mission and primary objective;
- operational personality;
- knowledge/practice boundary;
- explicit forbidden actions;
- work/pass method when applicable;
- approval/completion meaning;
- reactivation conditions.

Shared organization, delegation, Issue, state, event, return, consensus, thinker, and evidence rules belong in `references/`, not duplicated across every profile.

Useful shared contracts include:

- `references/organization-model.md`;
- `references/idea-maturation.md`;
- `references/thinker-waves.md`;
- `references/workflow.md`;
- `references/issue-protocol.md`;
- `references/evidence-policy.md`;
- `references/trust-boundary.md`;
- `references/consensus.md`.

## Execution ownership

Executor is activated only when the organization delegates implementation to an agent.

For strict backend workflows:

- `AGENT_EXECUTOR` activates Nero / `executor`;
- `MANUAL_OWNER` leaves Nero inactive and hands implementation to the repository owner/human.

For general organizational work, the Orchestrator may similarly assign implementation to an appropriate Executor or specialist, but should preserve independent final validation for substantial changes.