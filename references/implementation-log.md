# Implementation log workflow

During a slice, write short logs under `.ppd/04-progress/<slice>/`. Each log contains:

- change summary;
- decision and rationale;
- verification cases run and their result;
- outstanding items or deviations.

Do not expand module design during implementation unless the current change requires it. Record the change first; write the durable design back during calibration.
