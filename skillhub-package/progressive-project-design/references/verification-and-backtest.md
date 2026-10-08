# Verification and backtest workflow

Read this whenever a slice is created or its acceptance condition changes. Plan applicable verification cases before implementation. Behavior changes should have corresponding unit tests added or updated during implementation; use another appropriate test level with a recorded rationale when unit isolation is impractical.

## Minimum case set

For slices that change behavior, define applicable cases for:

1. the main success path;
2. boundary or invalid input;
3. failure or recovery;
4. regression when prior behavior may be affected.

Mark a case `not applicable` with a reason when that behavior has no meaningful case for the slice. Documentation-only slices define checks for the documentation output when available; they do not need behavior-level unit cases.

Each case records an ID, type (unit, regression, acceptance, replay, or backtest), scenario, fixed input or fixture, expected result, execution command, evidence location, and status. Use these statuses consistently: `pending`, `passed`, `failed`, `not run`, and `not applicable`. A passed case requires evidence; `not run` and `not applicable` require a reason. Include planned unit-test cases for changed behavior and relevant boundary/failure behavior. At planning time, the test file/case and command may be marked planned or `TBD`; finalize them during implementation using repository conventions.

## Backtest specialization

For trading, time-series, recommendation, or model behavior, also record:

- dataset version and time window;
- parameters, feature/configuration versions, and environment;
- metrics and acceptance thresholds;
- leakage, randomness, and reproducibility controls;
- comparison baseline and known limitations.

For ordinary business systems, call these verification, acceptance, replay, or regression cases rather than backtests.

## Lifecycle

- Before implementation: cases are `D2` acceptance definitions.
- During implementation: for behavior changes, add or update unit tests alongside the change, or use an appropriate alternative test level with a recorded rationale; results are pending or observed evidence. Documentation-only changes do not require behavior-level unit tests.
- After implementation: for code or behavior changes, analyze changed units, interfaces, dependencies, callers, and prior behavior. For a change contained within one unit, run that unit's tests and relevant regressions. For cross-unit or interface impact, include affected dependents and the relevant module/package suite. Use the full repository suite when a shared/core contract affects multiple areas or no bounded suite provides meaningful coverage. If impact remains unclear after investigation, run the broadest bounded relevant suite and record why. For documentation-only changes, skip unit tests and run applicable documentation checks when available. For configuration-only changes, select tests based on the behavior the configuration affects. Record scope, selection rationale, commands, results, evidence, and gaps in the implementation log.
- If a test cannot be authored or run, record the reason, alternative verification, and remaining risk. Unrun tests must remain `not run`, never marked as passing; use `not applicable` only when the test type does not apply and explain why.
- During calibration: link passing evidence, record deviations, and do not silently change expected behavior.
