# Existing-project analysis

Use this after initialization when code already exists and the documentation is missing, stale, or inconsistent.

## Evidence order

Inspect, in order:

1. repository README and contribution guidance;
2. package/build/deployment configuration;
3. application entry points and route/command registration;
4. domain modules, data models, persistence, and external integrations;
5. tests, fixtures, scripts, and observed run commands;
6. existing ADR/RFC/roadmap documents.

Summarize only what has evidence. Separate observed behavior, inferred behavior, and unresolved questions.

## Outputs

- `.ppd/01-overview/project-structure.md`: current directory structure and evidence;
- `.ppd/05-modules/README.md`: module inventory and maturity status;
- module skeletons only for modules needed by the first documentation/calibration slice;
- a draft overview only after its assumptions are clearly marked.

The first slice in an existing project is a documentation-and-calibration loop, not a redesign-and-reimplementation loop.
