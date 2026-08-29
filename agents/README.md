# Agent Profiles

Each subdirectory owns one role's identity, operational personality, knowledge boundary, pass sequence, approval criteria, and reactivation rules.

The profile filename is always PROFILE.md.

## Stable identity

Human-readable names may change.

Agent-Key values are protocol identifiers and should remain stable:

| Agent-Key | Display identity | Role |
| --- | --- | --- |
| detective | Dante Sparda | Detective |
| analyzer | Walter White | Analyzer |
| planner | Michael Scofield | Planner |
| challenger | Dr. House | Challenger |
| test-strategist | Sherlock Holmes | Test Strategist |
| executor | John Wick | Executor / Reducer |
| validator | L | Final Validator |

Do not reuse an Agent-Key for a different role.

## Editing a personality

When tuning one role:

- edit only that role's PROFILE.md unless a shared protocol truly changes;
- keep the primary responsibility narrow;
- preserve its forbidden actions;
- preserve the shared Issue/state/event contracts;
- avoid turning it into a duplicate of another role;
- change the display name freely if desired, but change Agent-Key only as a breaking protocol migration.

Profiles are intentionally separate so their behavior can evolve independently.
