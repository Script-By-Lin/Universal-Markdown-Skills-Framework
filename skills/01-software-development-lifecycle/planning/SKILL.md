---
name: planning
description: Actionable guidelines for decomposing complex features into atomic tasks and dependency-ordered execution roadmaps.
version: 1.7.0
category: planning
tags: [planning, task-breakdown, milestones, roadmaps, sequencing]
---

# Skill: Task & Project Planning

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 01 — Software Development Lifecycle  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `planning`
- **Category**: Software Development Lifecycle (Domain 01)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Decompose complex engineering initiatives into granular, dependency-ordered, non-conflicting tasks with verifiable completion criteria.
- **When to Use**: Initiating multi-stage features, cross-module refactoring, or clarifying vague tasks in TASKS.md.
- **Essential Invariants**:
  1. All tasks must have explicit, empirically verifiable completion criteria.
  2. Tasks must be dependency-ordered with no circular blockers.
  3. Size tasks to fit within discrete agent execution steps without context exhaustion.
- **Minimal Workflow**:
  1. Inspect requirements and identify critical path dependencies.
  2. Decompose initiative into atomic subtasks in TASKS.md with explicit verification criteria.
  3. Order subtasks sequentially, highlighting prerequisites and blockers.
  4. Update task states (Pending -> In Progress -> Completed) as empirical evidence is gathered.
- **Expected Deliverables**: Structured TASKS.md update with prioritized subtasks, dependencies, and exit criteria.
- **Critical Restrictions**: Never mark tasks completed without empirical evidence; never create untracked parallel work streams.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
This skill provides rigorous methodologies for decomposing complex engineering initiatives into granular, dependency-ordered, non-conflicting tasks. It ensures that work proceeds deterministically without scope creep or missed prerequisites.

---

### Scope
- **In-Scope**:
  - Translating technical requirements into dependency-ordered task graphs.
  - Sizing tasks to fit within discrete agent execution steps.
  - Identifying critical path dependencies and blocking conditions.
  - Updating [`TASKS.md`](../../../TASKS.md) with verifiable completion criteria.
- **Out-of-Scope**:
  - Requirements discovery and ambiguity resolution (delegate to [`skills/requirements-analysis/SKILL.md`](../../requirements-analysis/SKILL.md)).
  - Architecture design and tech stack selection (delegate to [`skills/software-architecture/SKILL.md`](../../software-architecture/SKILL.md)).

---

### When to Use
- At the outset of a multi-stage feature or system refactoring effort.
- When a user request spans multiple modules, services, or architectural layers.
- When existing tasks in `TASKS.md` are vague, un-sequenced, or lacking verifiable acceptance criteria.

---

### When Not to Use
- For one-line bug fixes or trivial documentation typos.
- When requirements remain fundamentally ambiguous or undefined.

---

### Prerequisites
- Scoped requirements or functional specifications available.
- Repository structure inspected and verified against [`CONTEXT.md`](../../../CONTEXT.md).

---

### Required Context
- Active tasks in [`TASKS.md`](../../../TASKS.md).
- Mandatory constraints in [`RULES.md`](../../../RULES.md).
- Architectural constraints in [`docs_agent/ARCHITECTURE.md`](../../../docs_agent/ARCHITECTURE.md).

---

### Core Instructions
1. **Atomic Task Sizing**: A task should touch at most 2–4 related files and represent a verifiable increment of progress.
2. **Dependency-First Sequencing**: Sequence tasks such that foundations (schemas, core types, domain models) are completed and validated before consumers (endpoints, UI views) begin.
3. **Explicit Verification Criteria**: Every task must define how an agent or developer proves it is complete (e.g., passing a specific test, verifying a build command).
4. **Isolated Edit Zones**: Design task boundaries so independent tasks do not create merge conflicts or file contention.

---

### Step-by-Step Workflow
1. **Step 1: Inventory Deliverables**
   - Extract the list of required code modules, schema changes, and documentation updates.
2. **Step 2: Construct Dependency Graph**
   - Identify which deliverables depend on others. Establish strict linear or DAG ordering.
3. **Step 3: Define Acceptance Gates**
   - For each task, author explicit pass/fail acceptance criteria.
4. **Step 4: Register in TASKS.md**
   - Append or update tasks in [`TASKS.md`](../../../TASKS.md) with initial state `Pending`.

---

### Quality Standards
- **Exhaustive**: No implicit or "hidden" prerequisite steps left undocumented.
- **Traceable**: Every task links directly to a verifiable user or architectural requirement.
- **Deterministic**: Any coding agent reading the task list will execute steps in the correct logical order.

---

### Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Dependency Validation | Graph trace | No circular dependencies in task sequence |
| Criteria Completeness | Inspection of `TASKS.md` | 100% of tasks have explicit completion checks |

---

### Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Monolithic Tasks ("Build the app") | Impossible to track incremental progress; high risk of hallucination | Decompose into domain models, data layers, APIs, UI, and tests |
| Premature Implementation | Coding UI before data types exist causes repeated rework | Plan and implement foundational types first |

---

### Restrictions
- Do NOT declare tasks completed without executing their verification criteria.
- Do NOT plan changes that violate repository constraints in [`RULES.md`](../../../RULES.md).

---

### Expected Deliverables
- Structured, sequenced task list in [`TASKS.md`](../../../TASKS.md).
- Dependency notes for multi-agent or multi-session continuity.

---

### Documentation Requirements
- Record planning rationale and milestone definitions in [`TASKS.md`](../../../TASKS.md).
- Log planning completion in [`docs_agent/SESSION_LOG.md`](../../../docs_agent/SESSION_LOG.md).

---

## Level 3 — Optional References & Supplementary Assets
  - None (self-contained Level 1 & Level 2 guidance)
