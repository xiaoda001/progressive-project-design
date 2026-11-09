# Requirements confirmation

Use this before writing or promoting the project overview. Ground questions in the user's request and available project evidence. Confirm material decisions that affect boundaries, such as:

- target users and the problem they need solved;
- deployment model and operating environment;
- data location for data-intensive systems;
- model location and input types for AI systems;
- entities, user flow, roles, and permissions for business systems;
- constraints, non-goals, and what would count as success.

## Task framing and gap scan

Start by stating whether the request is a targeted change in an existing flow, a bounded end-to-end feature, or a cross-cutting/new subsystem. Use that classification to scale discovery and documentation. It describes the work's complexity; it does not by itself require a new document or approval ceremony.

Before refining details, check the relevant code, project documents, and recent changes. Build a task-specific impact map from the user's workflow and existing boundaries. Consider users and roles, UI/API/service layers and callers, data lifecycle/history/audit and state transitions, side effects and integrations, concurrency and failure/recovery behavior, compatibility and migrations, deployment/operations, and verification. Include only areas that could affect this request. Record observed facts separately from assumptions and open decisions; explicitly mark important areas as out of scope or not applicable where useful.

Give the user a compact framing that helps improve the request: desired outcome, proposed scope, likely affected modules/interfaces, relevant omissions or risks, non-goals, success criteria, and material decisions still open. For broad feature requests, surface the highest-impact relevant gaps in the first framing instead of only promising to inspect them later. Make additions concrete (for example, “status changes also notify assignees,” “record who changed status and when,” “failed updates can be retried safely,” or “existing mobile clients must remain compatible”) and explain why each matters. Label each as confirmed impact, risk to verify, or optional scope so a possible concern is not silently turned into a requirement. Do not expand the task merely because an adjacent feature exists.

If the request spans multiple independent subsystems, identify the pieces, their dependencies, and a sensible order before asking detailed feature questions. Recommend starting with one coherent vertical slice unless the user's goal requires a broader first release. When discovery reveals new cross-module impact, reclassify the task and present the changed scope before proceeding.

## Question and decision-tree loop

1. List the material decisions that remain unresolved. Separate facts supported by project evidence from assumptions and user choices.
2. Show a compact decision tree when one choice changes which later questions or designs apply. If the choices are independent, use a short numbered list instead; do not invent branches for decisions that do not depend on each other.
3. Ask the user concise, answerable questions in their language. Bundle questions only when their answers are independent. For choices, state the practical trade-offs and a recommendation when there is a sound basis for one.
4. After each answer, update the decision tree and the working summary. Ask follow-up questions when the answer introduces a conflict, changes scope, or leaves a material branch undecided. Do not silently resolve a material choice or treat silence as approval.
5. When no material decision remains open, restate the shared understanding: problem, users, desired outcome, scope, constraints, non-goals, success criteria, confirmed decisions, and any explicitly accepted assumptions. Invite correction and wait for confirmation before treating the requirements as aligned.
6. If the user corrects the summary, update it and repeat the loop for affected decisions. Stop asking once the user confirms the summary and only low-impact implementation details remain; record those as assumptions and resolve them during the relevant slice.

Do not ask about details already established by the user or reliable project evidence. If the user asks to proceed with unresolved choices, identify the assumptions and their consequences, then proceed only within the authorized scope; do not label the requirements fully confirmed.

After alignment, offer two or three architecture, technology, or scope options with trade-offs when a decision is still needed. Let the user choose before promoting the overview and technology decisions to `D2`.

The overview must include positioning, boundaries, key decisions, non-goals, and unresolved assumptions. There must be no unresolved material requirement hidden in the summary.
