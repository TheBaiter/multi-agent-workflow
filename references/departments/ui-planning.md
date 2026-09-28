# UI Planning Department

## Mission
Plan user-facing interface decisions before frontend implementation without collapsing UX, information architecture, visual design, accessibility, interaction behavior, or code into one agent.

## Activation
Activate when work materially changes screens, navigation, journeys, interface structure, visual hierarchy, interaction patterns, or user-facing component behavior. Select only roles materially required.

## Atomic planning sequence
When applicable:
1. `ux-planner` A+B — journeys, task flows, usability expectations and recovery behavior.
2. `information-architecture-planner` A+B — grouping, hierarchy, navigation, labels and findability.
3. `graphic-design-planner` A+B — visual hierarchy, typography, composition, color/imagery direction and consistency.
4. Later specialist pairs may cover interaction design, design systems and accessibility as separate roles.
5. Resolved artifacts feed frontend architecture. UI planning roles do not implement frontend code.

Each non-trivial stage uses the same Agent-Key A+B with initial isolation, same-role cross-review and resolved synthesis.

## Routing
Use `ux-planner` for how a user understands, reaches, performs or recovers from a task.
Use `information-architecture-planner` for where information/actions belong and how they are grouped, named, ordered or navigated.
Use `graphic-design-planner` for visual communication after behavior and structure are sufficiently known.

A question outside a role is returned as a routed dependency. Finding it does not transfer ownership.

## Gate
Pass when every activated role has a valid same-role pair or documented trivial exception; material contradictions are resolved/escalated; cross-role dependencies are reconciled without merging authority; relevant loading/empty/error/permission-sensitive states are accounted for; unresolved user-authority choices are surfaced; and canonical artifacts are ready for frontend architecture.

## Anti-patterns
Do not create a generic `ui-expert`. Do not let graphic design decide navigation behavior, UX own backend contracts, IA become visual styling, or any planning role write production UI code. UX + graphic design never counts as the required A/B pair for either role.
