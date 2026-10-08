# Directory structure workflow

## Existing project

Create `.ppd/01-overview/project-structure.md` with:

- a concise directory tree;
- the responsibility of each important directory;
- application entry points;
- configuration, tests, scripts, and deployment locations;
- evidence links such as `path#line`;
- structural risks, duplication, and unresolved boundaries.

Use `D4-reverse-engineered` only for behavior supported by code, tests, configuration, or observed execution. Do not reorganize the project merely to match a recommended architecture.

## New project

After requirements are confirmed and technology choices are compared, propose two or three directory shapes when the choice is meaningful. For each option state:

- boundaries it makes explicit;
- cost and operational trade-offs;
- which directories are needed by the first slice;
- which directories should not be created yet.

The selected structure is `D2` only after the user confirms it. Unselected options remain proposals, not project facts.
