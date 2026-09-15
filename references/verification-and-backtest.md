# Verification and backtest workflow

Read this whenever a slice is created or its acceptance condition changes. Verification cases are required before implementation begins.

## Minimum case set

Define at least:

1. one main success path;
2. one boundary or invalid-input case;
3. one failure/recovery case;
4. one regression case when prior behavior exists.

Each case records an ID, scenario, fixed input or fixture, expected result, execution command, evidence location, and result status.

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
- During implementation: results are pending or observed evidence.
- During calibration: link passing evidence, record deviations, and do not silently change expected behavior.
