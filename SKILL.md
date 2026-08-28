---
name: progressive-project-design
description: Guides project architecture documentation through progressive, Just-in-Time design, with LLM-maintained code↔doc links and backlinks. Use when starting a new project, restructuring documentation, or designing project architecture — especially when the user wants to avoid Big-Design-Up-Front (BDUF), reduce documentation cognitive load, adopt a slice-driven incremental approach, or keep docs in sync with code.
---

# Progressive Project Design

## Response Language

Always respond in the language used by the user, unless the user explicitly requests another language.

## Core Principles

The essence of progressive design is: **Documentation is an output of decisions, not their starting point.** Write documentation only when a decision needs to be made; do not write it when no decision is needed.

| Principle | Description |
| --- | --- |
| Just-in-Time | Refine module details only before implementation; do not lay them out in advance |
| Slice-driven | Use the smallest runnable end-to-end loop as the design unit, rather than expanding module by module |
| Stop point | Stop after completing the documentation for each stage and wait for the next trigger |
| Three depth levels | L0 boundary → L1 slice needs → L2 full refinement |

## First Activation Checklist

When this skill is triggered for the **first time**, immediately perform the following checks to ensure the project has the foundational structure for progressive design.

**Proactive trigger conditions** (automatically propose this method when any of the following is true, without waiting for an explicit user request):

- The project root does not contain a `.ppd/` directory
- The project already has `.ppd/`, but its content was laid out all at once and has no status labels or slice plan
- The user has just run an initialization command such as `git init`, `uv init`, or `pnpm create`

Checklist:

- [ ] Check whether the project root contains a `.ppd/` directory
  - Reuse it if it exists
  - If it does not exist → create `.ppd/` with these subdirectories: `01-overview/` `02-architecture/` `03-plan/` `04-progress/` `05-modules/` (inside `04-progress/`, create subdirectories by slice: `s1/ s2/ ...`; see "Slice Archive Directory")
- [ ] Check whether `.ppd/README.md` exists; if not, create a skeleton document containing the documentation strategy table, writing cadence table, and an empty navigation table
- [ ] Check whether `.gitignore` already contains `.ppd/`; if not, suggest adding it

After completing these checks, **produce only the skeleton documentation** and do not write more. If this is an **existing project** (code already exists), additionally perform one reverse-analysis pass and automatically generate initial wiki drafts:

- Scan the code to produce a module inventory (D-status table, registered at L0)
- Generate skeleton documents for implemented modules (responsibility boundary + interface table + code locations, marked D4 reverse-engineered)
- Generate a draft project overview based on inferences from the code, with items requiring confirmation clearly marked

Then enter the requirements-confirmation conversation (see Step 1).

Do not repeat this process when the project is opened later; go directly to the appropriate step.

## Status System

### Documentation Maturity (D0–D4)

| Status | Meaning | Confidence |
| --- | --- | --- |
| D0 | Not designed; only a registered name or placeholder | None |
| D1 | Draft, not validated by implementation | Low |
| D2 | Finalized and approved for implementation | Medium |
| D3 | In implementation; may be overturned by actual code | Medium |
| D4 | Calibrated and aligned after implementation | High |

### Design Depth (L0–L2)

| Depth | Trigger | Content |
| --- | --- | --- |
| L0 boundary | Project kickoff or module registration | One-sentence responsibility, input/output boundaries, dependencies |
| L1 slice needs | The module is first involved in a vertical slice | L0 + interfaces, data models, and flows used by the current slice |
| L2 full refinement | Before the module is fully implemented | L1 + edge cases, error handling, and performance considerations |

## Documentation Relationship Model (LLM Wiki)

This methodology organizes documentation as a wiki, with relationships maintained automatically by the LLM:

| Relationship | Carrier |
| --- | --- |
| Navigation index | Navigation table in `.ppd/README.md` (the single entry point) |
| Bidirectional links | The module document's "Backlinks" section + cross-document references |
| Code mapping | The "Code location" column in interface tables (`file#line`) |
| Status tracking | D0–D4 status throughout all documents |
| Dependency graph | Aggregated module declarations of "depends on / depended on by" |

Management value: documentation changes from one-off, static files into a navigable, traceable knowledge network that stays synchronized with the code. The LLM maintains the relationships; people make the decisions.

## Writing Cadence

Organize work around five triggers. Stop after producing the artifact for each step; do not cross into the next step.

| Cadence | Trigger | Artifact | Quantity guideline |
| --- | --- | --- | --- |
| 1. Skeleton | Project initialization | Main README index: empty navigation table + D/L status conventions + writing cadence table | 1 document |
| 2. Requirements | After requirements are confirmed | Project overview: positioning, boundaries, key decisions, and an explicit non-goals list | 1 document |
| 3. Slice kickoff | One week before each slice starts | Finalized technology choices + L1 designs for modules involved in the slice + slice registration in the roadmap | 2–4 documents |
| 4. During implementation | Each change | Development log (3–5 lines: change summary + decision rationale + outstanding items) | As changes occur |
| 5. Calibration | Slice completion | Update module documents from D3→D4, record designs overturned by implementation, and synchronize code links | Update only; do not add documents |

## Slice Archive Directory

Organize `.ppd/04-progress/` by slice, with one subdirectory per slice (`s1/ s2/ ...`). Create the slice directory when the slice is registered in the roadmap (cadence 3):

```text
.ppd/04-progress/
├── s1/                         # All development logs + slice retrospective
│   ├── 2026-08-19-xxx.md       # Development log (cadence 4, written directly into its slice directory)
│   └── S1-2026-08-19-review.md # Slice retrospective (archived during calibration, alongside the logs)
└── s2/                         # Next slice ...
```

Conventions:

- **Slice cohesion**: Keep logs and the retrospective in the same directory; locate and investigate work by slice directory
- **Lightweight main-index maintenance**: In the `.ppd/README.md` navigation table, category 04 links only to directories (one link per slice + a link to the retrospective), rather than registering every file
- **Cross-document references**: Module-document backlinks and roadmap archive links consistently use `../04-progress/<slice>/<file>.md`
- **Logs for `.ppd` management itself** (non-business-slice changes such as directory-structure adjustments) go in the root of `04-progress/` and do not occupy a slice directory

## Workflow

### Phase One: Confirm Requirements (Cadence 2 Trigger)

Before writing any documentation, lock down boundary decisions through conversation. Select questions relevant to the project type from the following four dimensions; it is not necessary to ask every question.

**General dimensions (required):**

- **Target users**: Who will use the system? End users / internal teams / developers
- **Deployment model**: Local standalone / public web service / team self-hosted

**Select by project type:**

- **Data-intensive projects**: Where is data stored? Local self-hosted / cloud / hybrid
- **AI projects**: Where does the model run? Local / cloud API / switchable between both; what inputs are processed? Plain text / multimodal / structured data
- **Business systems**: What are the core entities? What is the user flow? What roles and permissions are needed?

**Write the overview only after confirmation; do not write it before confirmation.**

**Industry-practice options**: After confirming requirements and before writing the overview, the agent proposes 2–3 options based on industry practices (technology choices / architecture shape / feature scope), explains tradeoffs and applicable scenarios, and lets the user choose before writing. The user's ideas lead; industry guidance is a reference. Do not decide for the user.

### Phase Two: Define Vertical Slices

A slice is the smallest runnable end-to-end loop. It crosses multiple modules but contains only one data flow:

```text
Split by module (BDUF):
  Design Module A → Design Module B → Design Module C → Implement

Split by slice (progressive):
  Design + implement Slice 1 (smallest loop) → Design + implement Slice 2 → ...
```

Slice criteria:

- Each slice is independently verifiable (it can run and be demonstrated)
- Keep dependencies between slices as one-directional as possible
- Choose the "shortest path" for the first slice: cover the most core modules with the lightest implementation

### Phase Three: Delay Refinement (Cadence 3 Trigger)

Only during the week before a slice starts:

1. **Finalize technology choices**: Promote from D1 to D2 and lock versions
2. **Refine module design**: Write L1 documentation for involved modules according to the slice's needs
3. **Register the slice roadmap**: Record the slice name, covered modules, and goal in the roadmap

**Keep uninvolved modules at D0 throughout; do not touch or write them.**

### Phase Four: Write Logs, Not Design (Cadence 4)

During implementation, record only development logs (3–5 lines) and do not add design documents. Record design changes in logs and wait until the calibration phase to write them back. Logs are the first source for troubleshooting: "Decision and rationale" records why the implementation took this form, and "Outstanding items" records known issues.

**Archiving**: When the slice is complete (calibration cadence), summarize its development logs into a slice retrospective (`.ppd/04-progress/<slice>/<slice>-<date>-review.md`, alongside the logs) so logs remain searchable and are not lost. For logs involving interface or model changes, also update the "Code location" links and backlinks in the relevant module documents.

### Phase Five: Calibrate (Cadence 5)

After slice implementation is complete:

1. Verify deviations between design documentation and actual code
2. Update module-document status from D3 → D4
3. Write back design decisions that were overturned
4. **Do not expand** — D4 aligns only; it does not add scope
5. **Synchronize code mappings**: Update the "Code location" column and "Backlinks" section in interface tables for modules involved in the slice, ensuring bidirectional navigation between documentation and code

**Automatic LLM synchronization**: During calibration, the agent automatically scans `git diff` and code symbols (endpoints / models / functions) and compares them with the interface inventory in L1 documentation:

- Interface implemented and already documented → complete the code-location link and change status to D4
- Interface implemented but not documented → register it first, then set it to D4, preventing documentation lag
- Interface documented but removed from the code → mark it as an overturned design and write back the decision

## Anti-Patterns

| Anti-pattern | Problem | Correct approach |
| --- | --- | --- |
| Designing every module all at once | Cognitive overload; design has not been validated by implementation | Write only the L1 detail needed by the current slice |
| Writing the overview, architecture, and all modules together | Reader, timing, and purpose are unclear | Confirm requirements → write overview → stop |
| Writing module documentation to L2 before implementation | L2 details are likely to be overturned during implementation | L1 is enough to start; refine to L2 together with implementation when needed |
| Ignoring documentation after implementation | Documentation quickly becomes stale and useless | Use calibration cadence to update D3→D4 |
| Failing to define verifiable criteria for a slice | It is unclear when the slice is complete | Define "what can run" as the completion condition for every slice |
| Forgetting what to do next during development | Work stalls or priorities are guessed from memory | Run the Development Task Navigation section and derive the next step from documentation + code |

## Development Task Navigation

When the user asks "What should I do next?", use the following process to diagnose the state and produce an actionable task list.

### Step 1: Read the Slice Plan

Read `.ppd/03-plan/roadmap.md` to identify the current in-progress slice and the modules it covers.

### Step 2: Scan Module L1 Documentation

Read the module documents involved in the current slice (`.md` files under `.ppd/05-modules/` marked with statuses such as S1a/S1b) and extract:

- Declared public interfaces
- Declared data models
- Dependencies (which modules must be completed first)

### Step 3: Compare the Code Implementation

Scan the project code and compare it item by item with the interface inventory in the L1 documentation:

- **Implemented**: The interface exists; skip it
- **Not implemented, with dependencies not ready**: Mark it blocked and do not proceed for now
- **Not implemented, with dependencies ready**: Mark it as a next-step candidate

### Step 4: Sort by Dependency and Output

Organize the result as a next-step task list in this format:

```text
Current slice: [slice name]
Slice completion condition: [slice acceptance criteria defined in the L1 documentation]

Completed:
- [x] Interface A (code exists)
- [x] Interface B (code exists)

Next steps:
1. [Highest priority] Interface C — defined in L1 documentation, absent from code, no dependency blockers
2. [Second priority] Interface D — requires Interface C first

Blocked:
- Interface E — waiting for Module X (that module is not in the current slice)
```

### Special Cases

- **No in-progress slice**: Switch to cadence 2 (requirements confirmation) or cadence 3 (pre-slice refinement)
- **All interfaces in the slice are implemented**: State that the slice can enter calibration cadence and suggest starting the next slice
- **Code contains more than the L1 documentation** (an interface is implemented but not registered): First update the documentation to D4 by registering the interface and code location, then continue, preventing documentation lag
- **Interface is implemented but its code location is not registered**: Complete the code link before continuing to preserve valid bidirectional links

## Troubleshooting Navigation

When a bug or unexpected behavior occurs, trace it in this order:

1. Identify the module involved in the symptom → read the interface table and responsibility boundary in `.ppd/05-modules/<module>.md`
2. Search development logs under `.ppd/04-progress/<slice>/` (locate by slice directory and check the retrospective in the same directory): inspect "Decision and rationale" for why it was implemented this way and "Outstanding items" for known issues
3. Follow the "Code location" link directly to the implementation and compare documented behavior with actual behavior
4. After fixing it, write a cadence-4 log recording the root cause for future troubleshooting

## Project Snapshot

When the user asks "What is the state of this project?" or opens an existing project, perform this snapshot process:

1. **Read `.ppd/README.md`**: Obtain the documentation strategy and writing cadence conventions
2. **Read `.ppd/01-overview/project-overview.md`**: Obtain positioning, boundaries, and key decisions
3. **Read `.ppd/03-plan/roadmap.md`**: Obtain the slice plan and current progress
4. **Read `.ppd/05-modules/README.md`**: Obtain each module's D-status table
5. **Read `.ppd/02-architecture/tech-stack.md`** (if it exists): Obtain technology choices

Summarize using this format:

```text
Project: [name]
Positioning: [one sentence extracted from the overview]
Current phase: [slice status extracted from the roadmap]
Progress: S1a [in progress] / S1b [not started] ...

Module confidence:
  ├ Account and permissions  D3 in implementation (reference documentation is usable)
  ├ Document management      D1 draft (not validated)
  └ Knowledge-base engine    D0 (not designed)

What can be done next:
  Incomplete items in the current slice (see Development Task Navigation)
```

If `.ppd/` does not exist or most documents are missing, tell the user that progressive-design initialization has not yet been performed for the project and suggest running the first-activation process.

## Existing-Project Adaptation (Reverse Calibration)

When a project already contains code and `.ppd/` is missing or outdated, read [references/migration.md](references/migration.md) and follow its reverse-calibration process. Read that file only when handling an existing project.

Preserve these three core conventions:

- Treat the current code as the source of truth; mark implemented but undocumented modules as D4 (reverse-engineered)
- A slice in an existing project is a "documentation + calibration" loop; do not redesign functionality that is already implemented
- Choose a shortest path for the first slice that covers the core data flow with the least documentation

## Documentation Template Reference

When creating or updating `.ppd/` documentation, read only the template corresponding to the current artifact from [references/templates.md](references/templates.md). Do not load unrelated templates merely to create one kind of document, and do not create competing documentation when an existing project convention can be reused.

## Decision Standard

Before writing any document, answer these three questions. If they cannot be answered → the document should not be written now:

> **Who will read it? When will they read it? What decision will they make after reading it?**

Examples:

- "Someone might read this module document someday" → Do not write it
- "The developer implementing this module next Monday needs to determine the interface parameters" → Write L1

## Related

- This is a methodology document and is not tied to any technology stack
