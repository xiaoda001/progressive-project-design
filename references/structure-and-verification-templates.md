# Structure and verification templates

Read this file when creating either of the two new artifacts introduced by the progressive workflow.

## Project structure

Path: `.ppd/01-overview/project-structure.md`

```markdown
# Project structure

> Status: D1 or D4-reverse-engineered

## Directory overview

| Path | Responsibility | Evidence | Status |
|---|---|---|---|
| src/ | ... | path#line | D4 |

## Key entry points

- Application:
- Configuration:
- Tests:
- Deployment:

## Conclusions

- Observed facts:
- Inferences:
- Unresolved questions:
```

## Slice verification

Path: `.ppd/03-plan/<slice>-verification.md`

```markdown
# [Slice] verification and backtest cases

> Status: D2

## Completion condition

- [ ] Runnable result
- [ ] Observable result

## Cases

| ID | Scenario | Fixed input/fixture | Expected result | Command | Evidence | Status |
|---|---|---|---|---|---|---|
| S1-V1 | Main success path | ... | ... | ... | ... | pending |
| S1-V2 | Boundary input | ... | ... | ... | ... | pending |
| S1-V3 | Failure/recovery | ... | ... | ... | ... | pending |
| S1-V4 | Regression | ... | ... | ... | ... | pending |
```

For time-series, trading, recommendation, or model work, also record dataset version, time window, parameters, metrics, thresholds, baseline, and reproducibility controls.
