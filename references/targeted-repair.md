# Targeted repair workflow

Read this when a user reports a specific failure or asks to fix a defect. Keep the repair tied to that symptom and avoid unrelated refactoring.

## Establish the failure

Record a short failure card:

- observed symptom and error type;
- affected requirement or prior behavior;
- reproduction steps, fixed input, and expected versus actual result;
- available evidence, reasonable inferences, and unknowns.

If the failure cannot yet be reproduced, identify the smallest useful diagnostic or verification step. Separate observed facts from hypotheses.

## Choose the durable record

- If the defect belongs to the active slice, put the failure card, decision, and verification evidence in that slice's existing progress log and cases. Do not create a duplicate repair record.
- If it is independent of an active slice and its root cause, decision, behavior constraint, or verification lesson is likely to help future work, create `.ppd/04-progress/repairs/YYYY-MM-DD-<slug>.md` and add it to `.ppd/04-progress/repairs/README.md`.
- Fold a trivial local correction into an existing relevant progress log. Create the repairs directory and index only when the first durable standalone repair needs them.

Link the affected requirement, module, relevant code as `path#line`, regression case, and evidence. Keep confirmed facts, hypotheses, unresolved questions, and accepted decisions distinct. The repair index is a retrieval aid; the repair note is the evidence record.

## Find and verify a cause

List a small number of plausible root-cause hypotheses with supporting evidence and a way to distinguish each one. Investigate the most likely hypothesis with the narrowest useful check. Add or update a regression case that reproduces the failure when practical; otherwise record the alternative verification and why a test is unsuitable.

## Make and verify the repair

Change only what the verified cause requires. Analyze affected units, interfaces, dependencies, callers, and prior behavior, then select verification using the impact-scope rules in [verification-and-backtest.md](verification-and-backtest.md). Report commands and evidence. Until the verification result is available, describe the repair as pending verification; do not claim the defect is fixed.

After verification, update the record with the actual result and remaining risk. Link the repair index from `.ppd/README.md` when the index is first created. If the repair changes a lasting module responsibility or accepted behavior, add a backlink from the affected module document during calibration. A later task should read only matching repair notes, then re-check the current implementation before relying on prior conclusions.
