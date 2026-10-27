# AI-agent delivery loop

Read this when a project uses AI agents in planning, implementation, review, deployment, or operations. This workflow is designed to work across coding agents such as Codex, Claude Code, Trae, and others. It extends the existing progressive-design stages; it does not replace them.

## Portability contract

- Keep intent, requirements, plans, acceptance criteria, evaluation cases, and decisions in ordinary project artifacts or the project's established systems, using formats the team can inspect and revise.
- Express checks as repository commands or existing CI jobs where possible. Do not make the workflow depend on a particular agent's configuration file, command syntax, plugin system, tool protocol, or model.
- At the start of a task, inspect which capabilities the active agent actually provides. Translate the workflow into those capabilities without changing its decision boundaries. If a capability is missing, use a documented project command, CI, or a human step; do not silently skip the control.
- Agent-specific instruction files may point to the shared workflow or explain its local invocation. They are optional adapters, not the authoritative source for project policy or delivery decisions.
- When more than one agent is used on a project, keep the shared artifacts authoritative so work can continue in another agent without relying on private conversation history.

## End-to-end flow

1. **Capture intent.** Record the problem, desired outcome, affected users or systems, constraints, non-goals, success signals, and open questions. The originator corrects the draft; a responsible owner accepts it before work proceeds. Use the project's established source of truth. Do not put shared, versioned decisions under `.ppd/` when the consuming project's `.gitignore` excludes that directory.
2. **Shape a bounded specification and plan.** Turn accepted intent into the requirements and design needed for the current decision. Name affected modules, interfaces, dependencies, acceptance criteria, risks, and verification evidence. Review the implementation plan before code changes begin. Keep later slices at the boundary level.
3. **Provide maintained context.** Keep agent-facing project conventions, domain rules, and operating procedures concise, versioned where the team can review them, and linked to their authoritative sources. Assign an owner and a way to propose updates. Do not duplicate requirements across files without identifying which source is authoritative.
4. **Build a feedback loop.** Give the agent relevant checks it can run during the task, such as tests, builds, static checks, or observable output comparisons. Record what each check proves and what it cannot prove. For workflows where agent behavior is consequential, maintain representative evaluation cases and rerun them when prompts, instructions, tools, models, or other behavior-shaping inputs change. Use incident-derived cases to cover regressions.
5. **Review and gate by risk.** Use automated checks to handle repeatable policy and defect detection. Keep human approval for decisions that require judgment or carry material security, compliance, data, or production risk. Enforce permissions at the execution boundary, log decisions, and define a tested recovery or rollback path before granting consequential actions.
6. **Close the operational loop.** Monitor a small set of meaningful outcome and safety signals. Deterministic rules may trigger agent diagnosis or a proposed change, but bound the agent's available actions by risk tier. Route proposed changes through the normal review and acceptance flow. Turn confirmed incidents into regression checks or new intent; do not treat an alert or model diagnosis alone as an approved requirement.

## Adoption sequence

Start with a low-risk, human-reviewed workflow. Establish an intent format, a bounded plan, and checks that provide fast feedback. Measure cycle time, rework, verification failures, and review findings against a baseline. Add agent-behavior evaluations and automation gates only when the workflow has representative cases and clear ownership. Expand autonomy in small steps after permissions, logging, and recovery have been exercised.

## Decision record

For each workflow, record only what is needed to operate it:

- authoritative source for intent, requirements, and approvals;
- agent responsibilities and allowed actions;
- checks and evaluation cases, including known blind spots;
- human decision points and the risk that requires them;
- operational signals, action thresholds, and recovery path;
- owner, evidence location, and conditions for revisiting the design.

Use existing project artifacts and systems where possible. This reference does not require a new document or a particular agent product. Keep decisions in the appropriate source of truth, and link to them from project documentation when `.ppd/` is local-only.
