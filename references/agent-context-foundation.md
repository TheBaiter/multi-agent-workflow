# Integration with agent-context-foundation

This skill is intentionally organized using **$agent-context-foundation** principles.


Companion project:

https://github.com/TheBaiter/agent-context-foundation

Canonical skill name:

$agent-context-foundation

## Canonical reference

Repository:
https://github.com/TheBaiter/agent-context-foundation

Skill:
$agent-context-foundation

## Applied organization

Use progressive disclosure and canonical ownership:

- `SKILL.md` -> entrypoint and router only;
- `agents/<agent-key>/PROFILE.md` -> canonical owner of that role's mission, personality, knowledge boundary, limits, passes, and approval meaning;
- `references/scope.md` -> canonical scope owner;
- `references/workflow.md` -> canonical workflow/dormancy/return owner;
- `references/issue-protocol.md` -> canonical Issue identity, state, events, traceability, and communication owner;
- `references/state-machine.md` -> canonical state and transition owner;
- `references/consensus.md` -> canonical closure owner;
- GitHub Issue / repository task system -> current case chronology and execution state;
- source code/config/schema/migrations -> implementation truth;
- durable `Agent/` repository context -> only verified reusable knowledge, governed by $agent-context-foundation.

Do not make `SKILL.md` a second copy of every profile or reference. Route to the owner instead.

## Responsibility boundary

agent-context-foundation owns repository context concerns such as:

- minimum viable agent context;
- progressive disclosure;
- canonical knowledge ownership;
- Agent/ organization;
- reusable project rules;
- project maps;
- error memory;
- durable planning conventions;
- temporary workspace conventions;
- task traceability foundations.

multi-agent-workflow owns one functional backend defect case such as:

- candidate detection;
- adversarial investigation;
- cause and scope;
- repair planning;
- challenge;
- test strategy;
- implementation;
- final validation;
- per-role Issue state;
- cross-agent questions;
- unanimous closure.

## Use together

When agent-context-foundation is installed or available:

1. use it to locate the repository's authoritative instructions and context;
2. preserve its organization and canonical owners;
3. use the repository's existing Issue/task system;
4. keep this workflow's case chronology in that Issue;
5. promote only verified reusable conclusions back into durable context.

## Do not duplicate

Do not create parallel planning/history files under Agent/ merely to mirror the Issue.

Do not copy the full multi-agent conversation into error memory.

Do not turn temporary hypotheses into durable repository facts.

## Knowledge promotion

After closure, consider whether the case produced a reusable verified lesson.

If yes, use agent-context-foundation rules to promote only the durable conclusion to the appropriate canonical location.

If no reusable knowledge exists, leave the history in the Issue.

The correct result may be no durable context change.
