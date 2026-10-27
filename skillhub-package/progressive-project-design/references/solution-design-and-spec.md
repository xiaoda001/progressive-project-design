# Solution design, specification, and slicing

Read this after requirements are aligned and before planning functional slices for a new feature or substantial change. This is a spec-driven workflow adapted to progressive design: shared intent is made explicit before implementation, while detailed design remains limited to the active slice.

## Sequence

1. **Set architecture boundaries.** Identify the system context, major responsibilities, data and interface boundaries, critical quality attributes, and decisions that constrain the solution. Compare alternatives only where a material decision exists. Record accepted choices and rationale. Keep unstarted areas at L0/L1; do not design every module in advance.
2. **Write the feature spec.** Describe the problem, users, desired outcomes, functional behavior, constraints, non-goals, assumptions, and acceptance criteria. Link each requirement to the relevant architecture boundary when useful. Separate confirmed requirements from open questions. The spec explains what the system must do; it does not prescribe implementation details unless a confirmed constraint requires them.
3. **Prepare acceptance and test scenarios before implementation.** Derive observable scenarios from the spec. Cover the main user or system flow, relevant boundaries, failure and recovery behavior, permissions or data constraints, and regression behavior where existing behavior must remain. State expected outcomes and the evidence that will demonstrate them. Keep these as scenarios, not claims that tests already exist or have passed.
4. **Decompose into functional vertical slices.** Map spec requirements and scenarios to the smallest runnable end-to-end slices. Record dependencies, an implementation order, and which acceptance scenarios each slice satisfies. Keep a requirement-to-slice mapping so no accepted requirement disappears during decomposition. Do not split solely by technical layer when an end-to-end slice is practical.
5. **Plan the active slice.** Before implementation, refine only that slice: involved modules and interfaces, completion condition, success/boundary/failure/recovery/regression verification cases, planned unit-test coverage, and expected evidence. Name test cases and commands when known; mark them TBD if implementation discovery is needed.
6. **Implement, verify, and reconcile.** Implement the active slice, run the checks selected from impact analysis, and map requirements to evidence. If implementation reveals a necessary change to behavior or architecture, update the spec or decision record with the reason before treating the changed behavior as accepted. Calibrate module documentation after the slice is complete.

## Artifacts and depth

Use existing project documents and systems where possible. A project-level feature spec and architecture overview may be concise for a small change. A substantial feature may need a versioned spec, an architecture decision record, and a roadmap mapping slices to requirements and scenarios. Do not create separate files just to satisfy a template.

Plan acceptance scenarios for the whole confirmed feature before slicing so decomposition can be checked for coverage. Specify detailed executable tests for the active slice before coding; future slices need only scenario-level coverage until they become active. Scenarios are design evidence; test results are implementation evidence and must be recorded separately.

## Completion gates

Do not start functional slicing while material requirements remain unresolved. Do not start implementation until the active slice has a confirmed completion condition and applicable verification scenarios. User confirmation is required for choices that materially affect scope or expected behavior; low-impact technical details may remain explicit assumptions.
