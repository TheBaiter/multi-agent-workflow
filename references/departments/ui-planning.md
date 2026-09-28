# UI Planning Department

## Mission
Plan user-facing interface decisions before frontend implementation without collapsing UX, information architecture, visual design, accessibility, interaction behavior, or code into one agent.

## Activation
Activate when work materially changes screens, navigation, journeys, interface structure, visual hierarchy, interaction patterns, or user-facing component behavior. Select only roles materially required.

For meaningful visible/perceptible work, this department also activates the external skill:

- `intensive-ui-questioning` — `https://github.com/TheBaiter/intensive-ui-questioning` / `SKILL.md`.

Read `references/skill-routing.md` for skill inheritance/activation rules.

The UI skill is a procedure for exhaustive routed questioning and evidence, not a replacement role. Every UI planner remains inside its own atomic ownership while traversing applicable UI questions and routing findings owned by neighboring specialists.

All stable UI roles also inherit `agent-context-foundation` through the organization-wide skill rule.

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

## Intensive UI Questioning integration

When `intensive-ui-questioning` is active:

1. the assigned agent reads the current canonical skill entrypoint rather than relying on remembered guidance;
2. it traverses the applicable router/question packs using progressive disclosure;
3. it resolves only questions inside its role authority;
4. questions belonging to another atomic role become routed dependencies rather than being answered by convenience;
5. material skill findings are persisted in the authoritative task/canonical planning artifacts under `agent-context-foundation` placement rules;
6. when the UI plan changes materially, affected UI-questioning routes are reopened rather than assuming previous coverage still passes.

Examples:

- `ux-planner` owns user-job/journey/usability decisions but routes visual-system choices;
- `information-architecture-planner` owns grouping/navigation/findability but routes interaction/accessibility choices;
- `graphic-design-planner` owns visual communication but routes behavior and semantic accessibility;
- `interaction-design-planner` owns control/state mechanics but routes accessibility policy;
- `design-system-planner` owns primitive/reuse/governance boundaries but not page-level styling;
- `accessibility-planner` owns accessibility requirements but not the entire interaction/product plan.

The external skill may expose many domains; that breadth is a questioning surface, not permission to create a composite UI agent.

## Routing
Use `ux-planner` for how a user understands, reaches, performs or recovers from a task.
Use `information-architecture-planner` for where information/actions belong and how they are grouped, named, ordered or navigated.
Use `graphic-design-planner` for visual communication after behavior and structure are sufficiently known.
Use `interaction-design-planner` for the temporal/behavioral mechanics of controls and interface state changes.
Use `design-system-planner` when repeated UI patterns need explicit reuse, token, variant or governance boundaries.
Use `accessibility-planner` for accessibility constraints and testable accessibility requirements; it constrains adjacent plans without absorbing them.

A question outside a role is returned as a routed dependency. Finding it does not transfer ownership.

## Downstream continuation

The UI skill remains relevant after planning when visible/perceptible work continues. Morrison should conditionally attach `intensive-ui-questioning` to:

- `frontend-architect` for visible/perceptible structural consequences;
- `implementation-owner` for UI/frontend implementation;
- `quality-strategist` for UI verification planning;
- `independent-validator` for UI validation;
- plan-reopening reviewers when the artifact under review is materially UI-facing.

Each downstream role still applies only the subset it owns and routes the rest.

## Gate
Pass when every activated role has a valid same-role pair or documented trivial exception; material contradictions are resolved/escalated; cross-role dependencies are reconciled without merging authority; relevant loading/empty/error/permission-sensitive states are accounted for; activated `intensive-ui-questioning` routes are closed or explicitly blocked/owner-required; unresolved user-authority choices are surfaced; and canonical artifacts are ready for frontend architecture.

## Anti-patterns
Do not create a generic `ui-expert`. Do not let graphic design decide navigation behavior, UX own backend contracts, IA become visual styling, or any planning role write production UI code. UX + graphic design never counts as the required A/B pair for either role. Do not treat `intensive-ui-questioning` as authority to merge UI specialties into one agent, and do not claim the skill was applied from memory without consulting its current canonical source.
