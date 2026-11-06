---
name: requirements-analysis
description: Structured intake, disambiguation, scoping, and acceptance criteria authoring for engineering requests.
version: 1.7.0
category: requirements
tags: [requirements, scoping, intake, acceptance-criteria, user-stories]
---

# Skill: Requirements Engineering & Analysis

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 04 — Requirements & Business Analysis  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `requirements-analysis`
- **Category**: Requirements & Business Analysis (Domain 04)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Analyze user prompts, extract ambiguous constraints, and translate product goals into deterministic acceptance criteria.
- **When to Use**: Parsing raw feature requests, clarifying edge cases before development, or drafting user story criteria.
- **Essential Invariants**:
  1. Requirements must be testable with unambiguous pass/fail criteria.
  2. Explicitly document both happy paths and edge/error cases.
  3. Identify and resolve assumptions before writing production code.
- **Minimal Workflow**:
  1. Parse user prompt and extract core objectives and implicit expectations.
  2. Formulate Given-When-Then acceptance criteria for each functional scenario.
  3. Identify boundary conditions, failure modes, and platform constraints.
  4. Document verified criteria in TASKS.md or feature specification.
- **Expected Deliverables**: Structured requirements specification with unambiguous acceptance criteria.
- **Critical Restrictions**: Never proceed with ambiguous requirements when behavior could break existing system invariants.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
This skill establishes a systematic protocol for analyzing user prompts, resolving ambiguous or underspecified requirements, defining explicit technical scopes, and establishing unequivocal acceptance criteria prior to design or code changes.

---

### Scope
- **In-Scope**:
  - Deconstructing user prompts into functional requirements and non-functional requirements.
  - Identifying edge cases, security boundaries, and performance constraints.
  - Formulating unambiguous acceptance criteria in Given-When-Then format.
  - Explicitly bounding the scope to prevent feature creep.
- **Out-of-Scope**:
  - Architectural blueprinting and tech stack selection (delegate to [`skills/software-architecture/SKILL.md`](../../software-architecture/SKILL.md)).
  - Implementation task breakdown (delegate to [`skills/planning/SKILL.md`](../../planning/SKILL.md)).

---

### When to Use
- Whenever a user request presents broad, vague, or complex objectives (e.g. "Add user billing").
- When a prompt contains conflicting requirements or missing boundary conditions.
- At Stage 2 of the canonical engineering lifecycle defined in `WORKFLOW.md`.

---

### When Not to Use
- When requirements are already fully specified in an explicit issue or ticket with unambiguous test criteria.
- For emergency hotfixes with self-evident bug traces.

---

### Prerequisites
- Read the active user prompt and any referenced files.
- Inspect `CONTEXT.md` for existing architectural context.

---

### Required Context
- Mandatory constraints in `RULES.md`.
- Current repository state in `CONTEXT.md`.

---

### Core Instructions
1. **The Three Tiers of Information**:
   - Explicitly classify all statements as **Verified** (confirmed by codebase inspection or direct prompt statement), **Inferred** (logically derived but unconfirmed), or **Unknown** (missing information requiring clarification).
2. **Acceptance Criteria Primacy**:
   - Every requirement must have at least one testable acceptance criterion. If an outcome cannot be tested or measured, it is not an acceptable requirement.
3. **Explicit Non-Goals**:
   - Every scoping exercise must define what the task will *not* do, preventing scope bloat.
4. **UI Requirement Invariants**:
   - For UI requests, explicitly capture target screen sizes, accessibility criteria (contrast, keyboard navigation), and feedback states (loading, error, empty).

---

### Step-by-Step Workflow
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

### Quality Standards
- **Clarity**: Written in simple, unambiguous technical English.
- **Completeness**: Covers happy path, boundary edge cases, and failure modes.
- **Falsifiability**: A human or automated test can definitively determine pass/fail.

---

### Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Ambiguity Audit | Self-review against prompt | Zero unvalidated assumptions presented as facts |
| Testability | Criterion inspection | Every requirement maps to a potential test |

---

### Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Assuming Unstated Requirements | Leads to building unwanted features | Mark as "Unknown" and ask or declare as Out-of-Scope |
| Vague Criteria ("Must be fast") | Impossible to verify objectively | Use concrete metrics ("P95 latency &lt; 200ms at 100 QPS") |

---

### Restrictions
- Do NOT fabricate requirements that the user never requested.
- Do NOT relax mandatory repository constraints in `RULES.md`.

---

### Expected Deliverables
- Scoped requirements document or specification section.
- Explicit acceptance criteria matrix.

---

### Documentation Requirements
- Link requirements to tasks in `TASKS.md`.
- Record domain learnings in `MEMORY.md`.

---

## Level 3 — Optional References & Supplementary Assets
  - None (self-contained Level 1 & Level 2 guidance)
