# Implementation log workflow

During a slice, write short logs under `.ppd/04-progress/<slice>/`. Each log contains:

- change summary;
- decision and rationale;
- impact scope: affected units, interfaces, dependencies, callers, and prior behavior;
- tests selected and why, execution commands, results, and evidence;
- tests not run or failed, with reasons, alternative verification, and remaining risk;
- outstanding items or deviations.

Use `pending`, `passed`, `failed`, `not run`, and `not applicable` consistently. A passed test needs evidence; explain any not-run or not-applicable case. For code changes, select tests proportionally to impact: run the changed unit's tests for contained changes, include affected dependents and the relevant module/package suite for cross-unit changes, and use the full repository suite when a shared/core contract affects multiple areas or no bounded suite provides meaningful coverage. If scope remains unclear after investigation, run the broadest bounded relevant suite and record why. Documentation-only changes do not require unit tests; configuration-only changes require tests relevant to their behavioral effect.

Do not expand module design during implementation unless the current change requires it. Record the change first; write the durable design back during calibration.
