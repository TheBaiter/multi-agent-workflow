# Installation and Skill Dependencies

## Purpose

`multi-agent-workflow` is a valid standalone Agent Skill, but its full organizational guarantees depend on other procedural skills being available to the runtime when their contracts require them.

A repository URL is **provenance**, not proof that the dependency is installed or accessible in the current Codex/agent runtime.

Morrison must resolve dependency availability before spawning affected stable children.

## Dependency set

### `multi-agent-workflow`

Role: primary organization/orchestration skill.

Repository:

`https://github.com/TheBaiter/multi-agent-workflow`

Entrypoint:

`SKILL.md`

### `agent-context-foundation`

Role: required baseline context/memory discipline for every stable role, including Morrison and the historical backend-defect department.

Repository:

`https://github.com/TheBaiter/agent-context-foundation`

Entrypoint:

`SKILL.md`

Requirement:

`REQUIRED` for full stable-role operation.

### `intensive-ui-questioning`

Role: specialized questioning/evidence procedure for meaningful visible/perceptible UI/frontend work.

Repository:

`https://github.com/TheBaiter/intensive-ui-questioning`

Entrypoint:

`SKILL.md`

Requirement:

`REQUIRED_WHEN_ACTIVE` for work routed to meaningful visible/perceptible UI/frontend questioning, planning, implementation/review or validation.

## Dependency state

Before affected work begins, Morrison records each dependency as:

- `AVAILABLE`: current canonical skill source can actually be loaded by the runtime;
- `MISSING`: dependency is not installed/mounted/otherwise accessible;
- `BLOCKED`: source is expected but cannot currently be read or completed;
- `NOT_REQUIRED`: dependency does not apply to the current task/surface.

Recommended task-level record:

```text
SKILL-DEPENDENCIES

multi-agent-workflow: AVAILABLE
agent-context-foundation: AVAILABLE | MISSING | BLOCKED
intensive-ui-questioning: AVAILABLE | MISSING | BLOCKED | NOT_REQUIRED
Resolution-Evidence:
- <installed skill/path/current source anchor>
Mode: FULL | REDUCED | BLOCKED
```

Do not infer `AVAILABLE` merely because a profile mentions the skill or contains its GitHub URL.

## Runtime behavior

### Missing `agent-context-foundation`

Because `agent-context-foundation` is the required baseline for every stable role:

- do not claim full Multi-Agent Workflow guarantees;
- mark the organization `REDUCED` or the affected stable-role path `BLOCKED` according to the task/risk;
- do not reconstruct the missing current skill from memory;
- do not claim its memory/context protocol was applied;
- tell the user/operator which dependency is missing when that prevents requested work.

Disposable Thinkers may still operate only when the governing parent can preserve the required canonical task state without falsely claiming the missing baseline skill was used.

### Missing `intensive-ui-questioning`

When no meaningful visible/perceptible UI work is active, record `NOT_REQUIRED`.

When it is required:

- do not claim intensive UI questioning was performed;
- do not replace the current external procedure with a remembered summary;
- keep the affected UI path `PARTIAL`/`BLOCKED` according to its governing contract;
- do not claim the required 4/5 fresh-round audit closure without access to the current canonical skill sources.

## Standalone installation set

For full general use, install/provide all three skills to Codex/the host:

```bash
npx skills add TheBaiter/agent-context-foundation
npx skills add TheBaiter/intensive-ui-questioning
npx skills add TheBaiter/multi-agent-workflow
```

`intensive-ui-questioning` is only operationally required when the task activates meaningful visible/perceptible UI work, but installing it with the base set avoids a later dependency gap.

If the installation mechanism uses a different skill registry or local mount, the requirement is equivalent: the current canonical skill must be discoverable/readable by the child that needs it.

## Install-once packaging

A future install-once distribution should be an actual Agent Plugin bundle that packages/discovers the three skills according to the current OpenAI Agent Plugins/Skills format.

Do **not** add a cosmetic `plugin.json` while the dependent skills still live only as external URLs. A plugin manifest is valid packaging only when its declared/bundled skill resources are actually present and discoverable according to the plugin contract.

Until such a bundle is maintained, this repository remains a standalone skill with an explicit dependency set.

## Spawn-time dependency preflight

Before Morrison creates any stable child:

1. resolve the atomic role;
2. resolve inherited and conditional skill dependencies;
3. check actual runtime availability of every required/active skill;
4. record dependency state and evidence;
5. populate `Required-Skills`, `Conditional-Skills` and `Context-Checkpoint-Target` in the concrete `AGENT-MANIFEST`;
6. only then spawn the child.

A child is not allowed to downgrade its own required dependency silently after spawn.

## Core principle

**A skill reference is not an installation. Full-mode guarantees require the current procedural dependency to be actually available at runtime.**