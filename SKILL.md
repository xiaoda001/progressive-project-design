---
name: progressive-project-design
description: Plan and maintain project architecture documentation with Just-in-Time design, vertical slices, and code↔doc calibration. Use when the user asks to adopt or inspect this method, classify a new requirement or change, plan or prepare a vertical slice, determine or implement the next task from these documents, calibrate documentation against implementation, or archive a completed slice. Do not use for ordinary project setup, generic architecture questions, unrelated documentation work, or merely because a repository lacks a docs directory.
---

# Progressive Project Design

Apply progressive, decision-driven documentation: write only what the current decision or vertical slice needs, then calibrate it against implementation.

## Short action protocol

When invoked as `$progressive-project-design <action>` or through the `$ppd` alias, parse the first action token using this table. Accept the listed Chinese and English synonyms.

| Action | Synonyms | Behavior | Write authority |
|---|---|---|---|
| `状态` | `status`, `诊断`, `速览` | Inspect project, documents, active slice, drift, and evidence; report the smallest next action | Read-only |
| `初始化` | `init`, `采用`, `迁移` | Inspect existing documentation, then create or migrate only the minimum progressive-design skeleton | Documentation writes only |
| `需求 [内容]` | `requirement`, `新需求` | Clarify the user-observable outcome and acceptance evidence, analyze impact, and classify where the requirement belongs | Read-only; do not edit the roadmap or implement |
| `变更 [内容]` | `change`, `change request`, `需求变更` | Assess how a proposed change affects the active slice, interfaces, data, dependencies, and verification | Read-only; apply only through a subsequent authorized action |
| `规划` | `plan`, `切片` | Propose the next vertical slice; write it only after confirmation or delegated choice | No write before confirmation |
| `准备 [Sx]` | `prepare [Sx]` | Prepare the named or active slice to L1 and stabilize only required decisions | Documentation writes only |
| `下一步` | `next` | Determine and report the next implementation task from current evidence | Read-only |
| `推进` | `go`, `continue`, `开发` | Determine, implement, and verify exactly one smallest safe unblocked task in the active slice; update related progress documentation only when materially affected | Code, tests, and related documentation for one task |
| `校准 [Sx]` | `calibrate [Sx]`, `同步` | Compare documents with implementation evidence and update requested documents; mark D4 only after verification | Documentation writes only |
| `归档 [Sx]` | `archive [Sx]`, `收尾 [Sx]` | Verify the completed slice is safe to remove from active context, preserve a compact summary, then move only historical slice artifacts to cold storage | Documentation moves and writes only |
| `帮助` | `help`, omitted/unknown action | Show this action table and one-line examples; perform no project action | Read-only |

Treat additional text after the action as scope or constraints. If `准备`, `校准`, or `归档` omits the slice ID, use the unique matching slice; if none or multiple match, report the ambiguity and ask for the missing choice. `需求` and `变更` end with an impact assessment and recommended route; they never silently change the active slice. For `推进`, do not start a second task in the same invocation. Stop after verification or a genuine blocker and report what changed.

## Operating boundaries

Default to read-only diagnosis.

- Do not create or modify files when the user asks to analyze, inspect, explain, review, suggest, run `状态`, `需求`, `变更`, or `下一步`.
- Treat `初始化`, `准备`, `推进`, `校准`, and `归档` as explicit write authorization only within the limits in the action table.
- Never treat a missing `docs/` directory as permission to write.
- Preserve repository conventions and `AGENTS.md` instructions. Adapt this structure when the project already has ADR, RFC, or documentation conventions.
- Never overwrite an existing document blindly. Read it first and make the smallest compatible change.
- Do not modify `.gitignore` unless the skill creates a directly related generated artifact that must be ignored.
- Stop after the artifact or implementation task required for the current action; do not pre-design later slices.

Before writing a document, answer: **Who reads it, when do they read it, and what decision will it support?** If any answer is unclear, do not write it yet.

## Missing documentation bootstrap

At the start of every action except `帮助`, check whether `docs/` or an equivalent established progressive-design document set exists.

- For `初始化`, the action itself is explicit authorization to create the minimum compatible documentation skeleton. Inspect the repository first, preserve existing conventions, and create only the files needed to establish an entry point.
- For read-only actions such as `状态`, `需求`, `变更`, and `下一步`, complete any useful inspection that does not depend on project documents. Clearly report that the document set is absent, explain what cannot be determined, and offer the exact next command: `$progressive-project-design 初始化`. Do not create files.
- For `规划`, `准备`, `推进`, `校准`, or `归档` when the requested work depends on a missing document set, do not bootstrap it implicitly. Pause before documentation writes and ask one concise authorization question: **“未发现项目文档目录。是否先执行 `$progressive-project-design 初始化`，然后继续当前操作？”**
- If the user authorizes initialization in reply, treat that reply as documentation-write authority for the minimum skeleton, then resume only the originally requested action when its remaining scope is clear.
- If a partial or differently named documentation set exists, report it and adapt or migrate through `初始化`; never create a competing `docs/` tree without authorization.

## State model

Track three independent dimensions. Never combine them into one ambiguous status.

### Document maturity

| State | Meaning | Transition condition |
|---|---|---|
| D0 | Registered only; not designed | The module or decision is only named |
| D1 | Draft | Relevant assumptions and open questions are visible |
| D2 | Ready to implement | Scope, interfaces, dependencies, and acceptance evidence are agreed |
| D3 | Implementation in progress | Implementation has started and may invalidate the draft |
| D4 | Calibrated | Current code, tests, configuration, and observed behavior have been checked against the document |

Use `D0 -> D1 -> D2 -> D3 -> D4`. Do not mark D4 from source-name similarity or an unverified implementation. A user confirmation may satisfy D2 in a solo project; record that basis.

### Design depth

| Depth | Include |
|---|---|
| L0 | Responsibility, input/output boundary, dependencies |
| L1 | L0 plus interfaces, data shape, current-slice flow, acceptance criteria |
| L2 | L1 plus relevant edge cases, failure handling, concurrency, security, or performance constraints |

Use L1 as the normal implementation-ready depth. Add L2 only when the current slice actually requires it.

### Slice identity and execution

Use stable IDs such as `S1`, `S2`, and keep execution state separate: `planned`, `ready`, `in-progress`, `blocked`, `calibrating`, or `done`. Do not invent forms such as `S1a` unless the repository explicitly defines them.

For module documents, record all dimensions explicitly:

```markdown
> 成熟度：D2
> 设计深度：L1
> 所属切片：S1
> 最后校准：—
```

## Route by user intent

### Diagnose or summarize

1. Inspect existing project instructions and documentation without writing.
2. Read `docs/README.md`, overview, roadmap, module index, and technology decisions when present.
3. Report what exists, inconsistencies, missing evidence, active slice, and the smallest useful next action.
4. If this documentation system is absent, offer initialization; do not perform it automatically.

### Initialize or adopt

1. Inspect existing documentation before proposing a structure.
2. If `docs/` already contains material, read [references/migration.md](references/migration.md) and preserve it.
3. Create only missing directories and the smallest index skeleton authorized by the user.
4. Do not write the project overview until target users, deployment boundary, core user path, and explicit non-goals are known or reasonably discoverable.
5. Read [references/templates.md](references/templates.md) only for artifacts being created.

Recommended structure; adapt rather than force it:

```text
docs/
├── README.md
├── 01-overview/project-overview.md
├── 02-architecture/tech-stack.md
├── 03-plan/roadmap.md
├── 04-progress/<slice-id>-log.md
├── 05-modules/README.md
└── 99-archive/README.md
```

Create `99-archive/` only when the first slice is actually archived.

### Define a vertical slice

1. Identify one user-observable outcome and the shortest end-to-end path that proves it.
2. Propose up to three candidate slices when the boundary is uncertain.
3. Require an observable acceptance criterion, involved modules, dependencies, and exclusions.
4. Prefer one-way dependencies and the lightest implementation that exercises the core path.
5. Write the selected slice to the roadmap only after the user confirms it or explicitly delegates the choice.

### Handle new requirements and changes

Do not inject a new request directly into an `in-progress` slice. First identify the user-observable outcome, acceptance evidence, affected modules and interfaces, dependencies, exclusions, and whether the request invalidates an existing decision.

Classify it as exactly one of:

- **Clarification**: makes an existing acceptance criterion precise without expanding the outcome; recommend updating the current slice through `规划` or `准备`.
- **Small extension**: expands the current outcome but preserves its dependency direction and verification path; recommend inclusion only after the user confirms the scope change.
- **Independent capability**: delivers a separately observable outcome; recommend a new later slice.
- **Cross-cutting change**: alters shared architecture, data, security, operations, or multiple planned slices; report affected decisions and recommend replanning before implementation.
- **Defect**: observed behavior violates an already accepted criterion; treat it as repair work rather than a new requirement, and route implementation through `推进` only when it is the smallest safe task in the active slice.

Keep an `in-progress` slice stable unless the change is necessary to satisfy its existing acceptance criterion or the user explicitly accepts the revised scope and tradeoffs. After classification, recommend one next action: `规划`, `准备 [Sx]`, `推进`, or no project change. Do not edit documents or code during `需求` or `变更`.

### Prepare a slice for implementation

Run when the user says a slice is about to start or asks to prepare it; do not rely on a calendar phrase such as “one week before.”

1. Move the slice from `planned` to `ready` only when acceptance evidence and dependencies are clear.
2. Stabilize only the technology decisions needed by this slice.
3. Design only involved modules to L1; add L2 selectively.
4. Mark documents D2 when ready, then D3 when implementation actually starts.

### Record implementation changes

Record only changes that affect architecture, interfaces, data models, slice scope, operational behavior, or key decisions. Prefer one append-only log per slice. Skip formatting changes, spelling fixes, routine tests, and behavior-preserving local refactors.

### Archive a completed slice

Treat archives as cold historical evidence, not a second source of current truth.

1. Require the slice to be `done`, its observable acceptance criterion to have passed, affected documents to be calibrated to D4, and no unresolved blocker to remain. Implementation existing by itself is insufficient.
2. Confirm every still-valid interface, data constraint, architecture rule, operational behavior, and reusable decision remains in an active module, architecture, ADR/RFC, or overview document. Never archive the only current source of truth.
3. Read the archive templates in [references/templates.md](references/templates.md). Create one compact summary and an archive index entry, then move only slice-specific plans, logs, superseded drafts, resolved issue records, and bulky historical evidence under `99-archive/slices/<slice-id>/`.
4. Keep a compact `done / archived` row and summary link in the active roadmap. Remove archived files from active navigation and select the next active slice when one exists.
5. Preserve repository history and links where practical. Do not delete evidence, archive shared current module documents, or rewrite native ADR/RFC history merely to fit this layout.
6. If any gate fails, do not archive. Report the missing calibration, evidence, decision, or document promotion as the smallest next action.

`状态` and `校准` may recommend an eligible archive but must not perform it. Archive only through explicit `归档` authorization.

### Use cold context

Do not recursively scan or read archive bodies during routine `状态`, `规划`, `准备`, `下一步`, `推进`, or `校准` actions. Read only the archive index when active evidence is insufficient and history is plausibly relevant.

Escalate retrieval progressively:

1. Inspect current code, tests, configuration, and active documents.
2. Read `99-archive/README.md` only when a regression, migration, compatibility rule, legacy configuration, unexplained constraint, or explicit history request points to past work.
3. Read matching slice summaries.
4. Read detailed archived plans or logs only if the summary does not answer the question.

In a CodeGraph-indexed repository, inspect current implementation and call paths with CodeGraph before using archived explanations. Treat current evidence as authoritative when it conflicts with history, and report the drift.

### Calibrate or determine the next task

1. Read the active slice, its acceptance criteria, involved module documents, and dependencies.
2. Inspect implementation, tests, configuration, migrations, and runnable entry points. In a CodeGraph-indexed repository, use CodeGraph first as repository instructions require.
3. Classify evidence as:
   - **complete**: implementation exists and verification evidence passes;
   - **possibly complete**: implementation exists but verification is missing;
   - **next**: in the active slice, unimplemented, and dependencies are ready;
   - **blocked**: dependency or user decision is missing;
   - **document drift**: implementation and D1-D3 documentation disagree.
4. Update documents only if the selected action authorizes it. Mark D4 only after evidence-based comparison.
5. Mark the slice `done` only when its observable acceptance criterion is satisfied.
6. When the slice is eligible for cold storage, recommend `归档 [Sx]`; do not load unrelated archives to make that recommendation.

## Output discipline

- Clearly distinguish facts found in files from inferences.
- Report missing files as missing; do not assume their contents.
- Preserve existing naming and language where practical.
- Prefer small updates over creating parallel documents.
- Use [references/templates.md](references/templates.md) for stable field shapes, but follow established repository templates when they conflict.
