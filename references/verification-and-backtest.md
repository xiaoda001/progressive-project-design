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

## Test integrity and anti-shortcut checks

Treat tests as evidence about the accepted contract, not as a way to make the implementation appear correct. Apply these checks when designing, changing, or reviewing tests:

- Derive expected behavior from the confirmed spec, acceptance criteria, or another authoritative contract. Do not infer the expected result solely from the implementation under test. If the contract is ambiguous or no reliable oracle exists, state the uncertainty and ask for clarification when it changes behavior; otherwise leave the case pending with the assumption recorded.
- Make assertions observable and discriminating: each test should fail when its target behavior is removed or meaningfully broken. Avoid empty assertions, unconditional success, tests that only execute code without checking outcomes, and mocks that verify internal calls without asserting a contract-relevant result.
- Cover applicable boundary classes selected from the feature's risks, such as empty or missing values, invalid input, minimum/maximum values, permission boundaries, duplicate requests, state transitions, and failure recovery. Do not mechanically test every class; mark irrelevant classes `not applicable` with a reason.
- Do not weaken or delete an existing assertion, skip a failing test, broadly relax a threshold, or change expected results merely to obtain a green run. A changed expectation must trace to an accepted spec or documented behavior change. If that change affects scope or user-visible behavior, resolve it with the user before implementation.
- Keep fixtures deterministic and isolated where practical. Record environment, dataset, randomness, and time dependencies when they can affect the result.
- Before reporting completion, inspect the test diff and verify that the named command was actually run against the current change. Record its real result and evidence. Never invent test output, infer a pass from code inspection, or report a stale run as current.
- Map each acceptance criterion to one or more scenarios or explain why it has no automated case. A test suite passing does not establish coverage of unrepresented requirements.

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
