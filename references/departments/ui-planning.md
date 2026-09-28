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
4. `interaction-design-planner` A+B — control behavior, transitions, feedback, cancellation/reversal and interaction state mechanics.
5. `design-system-planner` A+B — reusable primitives, component families, variants/states, tokens and UI-system governance when reuse is material.
6. `accessibility-planner` A+B — explicit keyboard, focus, semantic, assistive-technology, visual/motion and accessible-status requirements.
7. Resolved artifacts feed frontend architecture. UI planning roles do not implement frontend code.

Each non-trivial stage uses the same Agent-Key A+B with initial isolation, same-role cross-review and resolved synthesis.

## Routing
Use `ux-planner` for how a user understands, reaches, performs or recovers from a task.
Use `information-architecture-planner` for where information/actions belong and how they are grouped, named, ordered or navigated.
Use `graphic-design-planner` for visual communication after behavior and structure are sufficiently known.
Use `interaction-design-planner` for the temporal/behavioral mechanics of controls and interface state changes.
Use `design-system-planner` when repeated UI patterns need explicit reuse, token, variant or governance boundaries.
Use `accessibility-planner` for accessibility constraints and testable accessibility requirements; it constrains adjacent plans without absorbing them.

A question outside a role is returned as a routed dependency. Finding it does not transfer ownership.

## Gate
Pass when every activated role has a valid same-role pair or documented trivial exception; material contradictions are resolved/escalated; cross-role dependencies are reconciled without merging authority; relevant loading/empty/error/permission-sensitive states are accounted for; unresolved user-authority choices are surfaced; and canonical artifacts are ready for frontend architecture.

## Anti-patterns
Do not create a generic `ui-expert`. Do not let graphic design decide navigation behavior, UX own backend contracts, IA become visual styling, or any planning role write production UI code. UX + graphic design never counts as the required A/B pair for either role.
