# Calibration workflow

Run this when a slice is complete or documentation drift is discovered.

## Scope

Calibrate only documents affected by the completed slice or confirmed drift. Use the change-impact analysis to identify affected units, interfaces, dependencies, callers, configuration, and prior behavior. Do not turn calibration into a repository-wide rewrite or update unrelated future-scope documents.

## Reconcile implementation and intent

For each affected requirement, interface, or behavior, distinguish:

| Status | Meaning | Documentation action |
|---|---|---|
| `implemented and verified` | Implemented behavior matches the accepted spec and applicable checks have evidence | Update relevant module and architecture facts; link implementation and verification evidence |
| `implemented, verification pending` | Code exists, but required checks have not run, failed, or lack adequate evidence | Record actual behavior and the verification gap; keep affected maturity at D3 |
| `not implemented` | Accepted scope is not present in the implementation | Keep it out of current-behavior claims; leave it in the roadmap/spec with its actual status |
| `spec mismatch` | Implemented behavior differs from the accepted spec or the difference is unexplained | Document the observed behavior and the discrepancy separately; do not rewrite the spec to make the implementation appear approved |

When a behavior change is intentional and material, get the required decision from the user, then update the spec, decision record, acceptance scenarios, and tests before treating the new behavior as accepted. If a discrepancy is unresolved or unapproved, leave it visible as a gap and do not promote the affected claims to D4.

## Steps

1. Compare only the affected roadmap entries, L1 module documents, spec, tests, configuration, verification evidence, and actual code.
2. Register implemented but undocumented interfaces and behavior, linking each claim to implementation evidence. A filename alone is not evidence.
3. Update relevant `path#line` code locations, module backlinks, dependencies, and responsibility boundaries.
4. Record decisions that changed, why they changed, and where the accepted decision is documented.
5. Promote affected modules from D3 to D4 only when their documented behavior matches the accepted scope and implementation evidence, and applicable verification has passed or an explicitly accepted alternative is recorded. Never mark unrun or failed checks as passed.
6. Archive a slice retrospective beside its logs, including deviations, verification gaps, and follow-up items.

## Completion check

Calibration is complete when every affected document has been reconciled, code links point to current locations, accepted requirements map to implementation and evidence or a visible gap, and no material spec mismatch is silently hidden. Unresolved gaps may remain, but affected documentation stays at D3 and the result is reported as pending verification or decision—not as fully calibrated.

Calibration aligns existing scope. It does not add the next slice or expand requirements.
