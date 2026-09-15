# Initialization workflow

Read this file when `.ppd/` is absent, incomplete, or has never been initialized.

## New project

1. Confirm the project is new and no existing documentation convention should be preserved.
2. Create `.ppd/README.md` and the five minimum directories.
3. Record the documentation strategy, status model, writing cadence, and an empty navigation table.
4. Do not create an overview, architecture decision, module design, roadmap slice, or verification plan yet.
5. Stop and begin requirements confirmation only when the user provides or confirms requirements.

## Existing project

1. Preserve existing README, ADR, RFC, roadmap, tests, and runbooks.
2. Read [migration.md](migration.md) and perform one reverse-analysis pass.
3. Create a project-structure summary and a module inventory marked `D4-reverse-engineered` or `D1-draft` when evidence is incomplete.
4. Mark inferred facts and contradictions explicitly.
5. Do not redesign implemented behavior or claim that a generated draft is user-approved.

The `.ppd/` directory is normally versioned. Ignore it only when the project explicitly requires local-only documentation.
