# Development task navigation

Read the current roadmap, then the L1 documents for its in-progress slice. Compare declared interfaces, models, dependencies, and verification cases with the code.

For any task that may affect a module with prior repair records—not only a repeated defect—start at `.ppd/README.md`, check the linked repair index if present, and find entries matching the module or behavior. Read only matching repair notes and affected module documents. Treat past findings as evidence about the earlier state; compare them with current code before applying the same diagnosis or recommendation.

Report:

- current slice and completion condition;
- completed interfaces and passing cases;
- next unblocked interfaces or cases, ordered by dependency;
- blocked items and the missing dependency;
- whether the slice is ready for calibration.

If no slice is active, route to requirements confirmation or slice planning. If code contains undocumented behavior, register it and link evidence before recommending further implementation.
