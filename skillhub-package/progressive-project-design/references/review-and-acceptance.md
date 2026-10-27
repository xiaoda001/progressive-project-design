# Review and acceptance workflow

Read this when reviewing an implemented slice or checking whether its requirements are ready to deliver. Use it when the task or risk calls for a review; a separate review pass is not required for every small change.

## Code review

Review the actual diff against the slice, requirements, and repository conventions. Report findings before proposing fixes, ordered by severity. For each finding include:

- location and the behavior or contract affected;
- evidence and likely impact;
- a concrete correction or follow-up.

Check for missing or out-of-scope behavior, correctness and boundary risks, regressions, and gaps in tests or verification evidence. If there are no findings, say so and state what was reviewed. Keep review separate from implementation unless fixing findings is within the current task's authorized scope.

When reviewing tests, check them against the confirmed spec and acceptance scenarios. Confirm that assertions can fail for a meaningful defect, expected results come from the contract rather than being copied from implementation behavior, applicable boundary and recovery cases are represented, and no test was skipped, deleted, or weakened only to obtain a passing result. Verify reported test status against actual execution evidence.

## Requirement acceptance

Check each requirement against observable behavior and available evidence. Use a compact traceability table:

| Requirement | Acceptance criterion | Implementation location | Evidence | Status |
|---|---|---|---|---|

Use the verification statuses `passed`, `failed`, `pending`, `not run`, and `not applicable`. A `passed` status requires evidence. Use `not run` or `not applicable` only with a reason. State whether the slice is ready to deliver and list remaining gaps; passing tests alone do not prove that every requirement is satisfied.

## Decision boundaries

Keep acceptance criteria within the confirmed scope. Ask the user only when a finding exposes an unresolved choice that changes scope, expected behavior, or another material project decision. Otherwise report the finding and continue with the authorized task.
