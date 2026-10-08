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

| ID | Type | Scenario | Fixed input/fixture | Expected result | Test file/case | Command | Evidence | Status |
|---|---|---|---|---|---|---|---|---|
| S1-V1 | acceptance | Main success path | ... | ... | planned/TBD | planned/TBD | ... | pending |
| S1-V2 | unit | Changed behavior or boundary | ... | ... | planned/TBD | planned/TBD | ... | pending |
| S1-V3 | unit or acceptance | Failure/recovery, when applicable | ... | ... | planned/TBD | planned/TBD | ... | pending |
| S1-V4 | regression | Existing behavior, when applicable | ... | ... | planned/TBD | planned/TBD | ... | pending |

Allowed statuses: `pending`, `passed`, `failed`, `not run`, `not applicable`. Attach evidence to passed cases and a reason to `not run` or `not applicable` cases. Finalize planned/TBD test locations and commands during implementation.
```

For time-series, trading, recommendation, or model work, also record dataset version, time window, parameters, metrics, thresholds, baseline, and reproducibility controls.
