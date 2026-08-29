# Agent Profiles

Each subdirectory owns one role's identity, operational personality, knowledge boundary, pass sequence, approval criteria, and reactivation rules.

The profile filename is always PROFILE.md.

## Stable identity

All human-readable agent identities in this skill are characters from **Devil May Cry**. This keeps the organization visually distinct while the protocol remains independent of the display name.

Human-readable names may change later.

Agent-Key values are protocol identifiers and should remain stable:

| Agent-Key | Display identity | Role |
| --- | --- | --- |
| detective | Dante Sparda | Detective |
| analyzer | Vergil | Analyzer |
| planner | V | Planner |
| challenger | Lady | Challenger |
| test-strategist | Nico Goldstein | Test Strategist |
| executor | Nero | Executor / Reducer |
| validator | Trish | Final Validator |

Do not reuse an Agent-Key for a different role.

## Editing a personality

When tuning one role:

- edit only that role's PROFILE.md unless a shared protocol truly changes;
- keep the primary responsibility narrow;
- preserve its forbidden actions;
- preserve the shared Issue/state/event contracts;
- avoid turning it into a duplicate of another role;
- change the display name freely if desired, but change Agent-Key only as a breaking protocol migration.

## Profile contract

Each profile owns only role-local behavior:

- mission and primary objective;
- operational personality;
- knowledge/practice boundary;
- explicit forbidden actions;
- differentiated pass sequence when applicable;
- approval meaning;
- reactivation conditions.

Shared Issue, state, event, return, and consensus rules belong in `references/`, not duplicated across profiles.

Profiles are intentionally separate so their behavior can evolve independently.
