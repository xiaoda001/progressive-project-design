# Targeted repair workflow

Read this when a user reports a specific failure or asks to fix a defect. Keep the repair tied to that symptom and avoid unrelated refactoring.

## Establish the failure

Record a short failure card:

- observed symptom and error type;
- affected requirement or prior behavior;
- reproduction steps, fixed input, and expected versus actual result;
- available evidence, reasonable inferences, and unknowns.

If the failure cannot yet be reproduced, identify the smallest useful diagnostic or verification step. Separate observed facts from hypotheses.

## Find and verify a cause

List a small number of plausible root-cause hypotheses with supporting evidence and a way to distinguish each one. Investigate the most likely hypothesis with the narrowest useful check. Add or update a regression case that reproduces the failure when practical; otherwise record the alternative verification and why a test is unsuitable.

## Make and verify the repair

Change only what the verified cause requires. Analyze affected units, interfaces, dependencies, callers, and prior behavior, then select verification using the impact-scope rules in [verification-and-backtest.md](verification-and-backtest.md). Report commands and evidence. Until the verification result is available, describe the repair as pending verification; do not claim the defect is fixed.
