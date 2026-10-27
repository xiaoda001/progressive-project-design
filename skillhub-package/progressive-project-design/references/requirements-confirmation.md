# Requirements confirmation

Use this before writing or promoting the project overview. Ground questions in the user's request and available project evidence. Confirm material decisions that affect boundaries, such as:

- target users and the problem they need solved;
- deployment model and operating environment;
- data location for data-intensive systems;
- model location and input types for AI systems;
- entities, user flow, roles, and permissions for business systems;
- constraints, non-goals, and what would count as success.

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
