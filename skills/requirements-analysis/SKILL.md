---
name: requirements-analysis
description: Structured intake, disambiguation, scoping, and acceptance criteria authoring for engineering requests.
version: 1.0.0
category: requirements
tags: [requirements, scoping, intake, acceptance-criteria, user-stories]
---

# Skill: Requirements Analysis & Scoping

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.

---

## 1. Metadata
- **Identifier**: `requirements-analysis`
- **Category**: Strategy & Intake
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
This skill establishes a systematic protocol for analyzing user prompts, resolving ambiguous or underspecified requirements, defining explicit technical scopes, and establishing unequivocal acceptance criteria prior to design or code changes.

---

## 3. Scope
- **In-Scope**:
  - Deconstructing user prompts into functional requirements and non-functional requirements.
  - Identifying edge cases, security boundaries, and performance constraints.
  - Formulating unambiguous acceptance criteria in Given-When-Then format.
  - Explicitly bounding the scope to prevent feature creep.
- **Out-of-Scope**:
  - Architectural blueprinting and tech stack selection (delegate to [`skills/software-architecture/SKILL.md`](../software-architecture/SKILL.md)).
  - Implementation task breakdown (delegate to [`skills/planning/SKILL.md`](../planning/SKILL.md)).

---

## 4. When to Use
- Whenever a user request presents broad, vague, or complex objectives (e.g. "Add user billing").
- When a prompt contains conflicting requirements or missing boundary conditions.
- At Stage 2 of the canonical engineering lifecycle defined in [`WORKFLOW.md`](../../WORKFLOW.md).

---

## 5. When Not to Use
- When requirements are already fully specified in an explicit issue or ticket with unambiguous test criteria.
- For emergency hotfixes with self-evident bug traces.

---

## 6. Prerequisites
- Read the active user prompt and any referenced files.
- Inspect [`CONTEXT.md`](../../CONTEXT.md) for existing architectural context.

---

## 7. Required Context
- Mandatory constraints in [`RULES.md`](../../RULES.md).
- Current repository state in [`CONTEXT.md`](../../CONTEXT.md).

---

## 8. Core Instructions
1. **The Three Tiers of Information**:
   - Explicitly classify all statements as **Verified** (confirmed by codebase inspection or direct prompt statement), **Inferred** (logically derived but unconfirmed), or **Unknown** (missing information requiring clarification).
2. **Acceptance Criteria Primacy**:
   - Every requirement must have at least one testable acceptance criterion. If an outcome cannot be tested or measured, it is not an acceptable requirement.
3. **Explicit Non-Goals**:
   - Every scoping exercise must define what the task will *not* do, preventing scope bloat.
4. **UI Requirement Invariants**:
   - For UI requests, explicitly capture target screen sizes, accessibility criteria (contrast, keyboard navigation), and feedback states (loading, error, empty).

---

## 9. Step-by-Step Workflow
1. **Step 1: Extract Core Intent**
   - Identify the user's primary business or technical objective.
2. **Step 2: Surface Hidden Assumptions**
   - Check error states, invalid inputs, rate limits, edge conditions, and auth requirements.
3. **Step 3: Define Scope Boundaries**
   - Author "In-Scope" and "Out-of-Scope" lists.
4. **Step 4: Formulate Acceptance Criteria**
   - Write testable criteria using the Given-When-Then syntax.
5. **Step 5: User Alignment**
   - If critical ambiguities exist, ask one focused clarifying question before executing.

---

## 10. Quality Standards
- **Clarity**: Written in simple, unambiguous technical English.
- **Completeness**: Covers happy path, boundary edge cases, and failure modes.
- **Falsifiability**: A human or automated test can definitively determine pass/fail.

---

## 11. Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Ambiguity Audit | Self-review against prompt | Zero unvalidated assumptions presented as facts |
| Testability | Criterion inspection | Every requirement maps to a potential test |

---

## 12. Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Assuming Unstated Requirements | Leads to building unwanted features | Mark as "Unknown" and ask or declare as Out-of-Scope |
| Vague Criteria ("Must be fast") | Impossible to verify objectively | Use concrete metrics ("P95 latency &lt; 200ms at 100 QPS") |

---

## 13. Restrictions
- Do NOT fabricate requirements that the user never requested.
- Do NOT relax mandatory repository constraints in [`RULES.md`](../../RULES.md).

---

## 14. Expected Deliverables
- Scoped requirements document or specification section.
- Explicit acceptance criteria matrix.

---

## 15. Documentation Requirements
- Link requirements to tasks in [`TASKS.md`](../../TASKS.md).
- Record domain learnings in [`MEMORY.md`](../../MEMORY.md).

