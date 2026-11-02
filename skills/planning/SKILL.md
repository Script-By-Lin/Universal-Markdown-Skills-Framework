---
name: planning
description: Actionable guidelines for decomposing complex features into atomic tasks and dependency-ordered execution roadmaps.
version: 1.0.0
category: planning
tags: [planning, task-breakdown, milestones, roadmaps, sequencing]
---

# Skill: Task & Project Planning

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.

---

## 1. Metadata
- **Identifier**: `planning`
- **Category**: Strategy & Planning
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
This skill provides rigorous methodologies for decomposing complex engineering initiatives into granular, dependency-ordered, non-conflicting tasks. It ensures that work proceeds deterministically without scope creep or missed prerequisites.

---

## 3. Scope
- **In-Scope**:
  - Translating technical requirements into dependency-ordered task graphs.
  - Sizing tasks to fit within discrete agent execution steps.
  - Identifying critical path dependencies and blocking conditions.
  - Updating [`TASKS.md`](../../TASKS.md) with verifiable completion criteria.
- **Out-of-Scope**:
  - Requirements discovery and ambiguity resolution (delegate to [`skills/requirements-analysis/SKILL.md`](../requirements-analysis/SKILL.md)).
  - Architecture design and tech stack selection (delegate to [`skills/software-architecture/SKILL.md`](../software-architecture/SKILL.md)).

---

## 4. When to Use
- At the outset of a multi-stage feature or system refactoring effort.
- When a user request spans multiple modules, services, or architectural layers.
- When existing tasks in `TASKS.md` are vague, un-sequenced, or lacking verifiable acceptance criteria.

---

## 5. When Not to Use
- For one-line bug fixes or trivial documentation typos.
- When requirements remain fundamentally ambiguous or undefined.

---

## 6. Prerequisites
- Scoped requirements or functional specifications available.
- Repository structure inspected and verified against [`CONTEXT.md`](../../CONTEXT.md).

---

## 7. Required Context
- Active tasks in [`TASKS.md`](../../TASKS.md).
- Mandatory constraints in [`RULES.md`](../../RULES.md).
- Architectural constraints in [`docs_agent/ARCHITECTURE.md`](../../docs_agent/ARCHITECTURE.md).

---

## 8. Core Instructions
1. **Atomic Task Sizing**: A task should touch at most 2–4 related files and represent a verifiable increment of progress.
2. **Dependency-First Sequencing**: Sequence tasks such that foundations (schemas, core types, domain models) are completed and validated before consumers (endpoints, UI views) begin.
3. **Explicit Verification Criteria**: Every task must define how an agent or developer proves it is complete (e.g., passing a specific test, verifying a build command).
4. **Isolated Edit Zones**: Design task boundaries so independent tasks do not create merge conflicts or file contention.

---

## 9. Step-by-Step Workflow
1. **Step 1: Inventory Deliverables**
   - Extract the list of required code modules, schema changes, and documentation updates.
2. **Step 2: Construct Dependency Graph**
   - Identify which deliverables depend on others. Establish strict linear or DAG ordering.
3. **Step 3: Define Acceptance Gates**
   - For each task, author explicit pass/fail acceptance criteria.
4. **Step 4: Register in TASKS.md**
   - Append or update tasks in [`TASKS.md`](../../TASKS.md) with initial state `Pending`.

---

## 10. Quality Standards
- **Exhaustive**: No implicit or "hidden" prerequisite steps left undocumented.
- **Traceable**: Every task links directly to a verifiable user or architectural requirement.
- **Deterministic**: Any coding agent reading the task list will execute steps in the correct logical order.

---

## 11. Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Dependency Validation | Graph trace | No circular dependencies in task sequence |
| Criteria Completeness | Inspection of `TASKS.md` | 100% of tasks have explicit completion checks |

---

## 12. Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Monolithic Tasks ("Build the app") | Impossible to track incremental progress; high risk of hallucination | Decompose into domain models, data layers, APIs, UI, and tests |
| Premature Implementation | Coding UI before data types exist causes repeated rework | Plan and implement foundational types first |

---

## 13. Restrictions
- Do NOT declare tasks completed without executing their verification criteria.
- Do NOT plan changes that violate repository constraints in [`RULES.md`](../../RULES.md).

---

## 14. Expected Deliverables
- Structured, sequenced task list in [`TASKS.md`](../../TASKS.md).
- Dependency notes for multi-agent or multi-session continuity.

---

## 15. Documentation Requirements
- Record planning rationale and milestone definitions in [`TASKS.md`](../../TASKS.md).
- Log planning completion in [`docs_agent/SESSION_LOG.md`](../../docs_agent/SESSION_LOG.md).

