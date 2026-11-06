---
name: software-architecture
description: Principles and workflows for high-level system design, layer separation, modularity, and Architectural Decision Records (ADRs).
version: 1.7.0
category: architecture
tags: [architecture, system-design, modularity, clean-architecture, adr]
---

# Skill: Software Architecture & System Design

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 03 — Software Architecture & Design  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `software-architecture`
- **Category**: Software Architecture & Design (Domain 03)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Design scalable, maintainable, loosely coupled software architectures adhering to clean boundaries and SOLID principles.
- **When to Use**: Structuring new services, establishing module boundaries, decomposing monoliths, or designing distributed systems.
- **Essential Invariants**:
  1. Enforce strict unidirectional dependency flows; high-level policies must not depend on low-level details.
  2. Explicit interfaces are mandatory between system boundaries and third-party dependencies.
  3. Architecture diagrams and boundary specifications must reflect actual repository filesystem reality.
- **Minimal Workflow**:
  1. Define system boundaries, domain contexts, and external integration points.
  2. Design modular package/directory hierarchy with clean separation of concerns.
  3. Author architectural overview and dependency graphs in ARCHITECTURE.md.
  4. Verify that code imports strictly obey defined boundary layers.
- **Expected Deliverables**: Architectural blueprint and boundary specifications with zero circular dependencies.
- **Critical Restrictions**: Prohibit circular module dependencies; avoid premature distributed microservice fragmentation.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
This skill governs system architecture, modular decomposition, dependency management, boundary enforcement, and the formal drafting of Architectural Decision Records (ADRs) to ensure long-term codebase maintainability and prevent technical debt.

---

### Scope
- **In-Scope**:
  - Defining structural module boundaries and dependency directions.
  - Applying Clean Architecture and Ports-and-Adapters patterns.
  - Evaluating technical trade-offs between architectural alternatives.
  - Formulating immutable Architectural Decision Records (ADRs) in [`DECISIONS.md`](../../../DECISIONS.md).
- **Out-of-Scope**:
  - Low-level component styling and UI widgets (delegate to [`skills/ui-ux-pro-max/SKILL.md`](../../ui-ux-pro-max/SKILL.md)).
  - Detailed database index tuning (delegate to [`skills/database-design/SKILL.md`](../../database-design/SKILL.md)).

---

### When to Use
- When introducing a new service, subsystem, library, or core data pipeline.
- When an existing architecture faces scaling, decoupling, or testability bottlenecks.
- Before committing to significant technology choices or non-trivial refactoring.

---

### When Not to Use
- For isolated bug fixes within established module boundaries.
- For minor documentation or configuration updates.

---

### Prerequisites
- Verified understanding of existing architecture via [`CONTEXT.md`](../../../CONTEXT.md).
- Settled decisions reviewed in [`DECISIONS.md`](../../../DECISIONS.md).

---

### Required Context
- Architectural invariants in [`docs_agent/ARCHITECTURE.md`](../../../docs_agent/ARCHITECTURE.md).
- Repository rules in [`RULES.md`](../../../RULES.md).

---

### Core Instructions
1. **Unidirectional Dependency Flow**:
   - Dependencies must always point inward toward the core domain.
   - Core domain models must have zero dependencies on frameworks, databases, or UI layers.
2. **Interface-Based Decoupling**:
   - High-level policy must never depend on low-level implementation details. Both must depend on abstractions (interfaces / protocols).
3. **Immutability of Settled ADRs**:
   - Never silently alter historical decisions in `DECISIONS.md`.
   - If an architectural shift is required, create a new ADR that explicitly supersedes the older one.
4. **Zero Accidental Complexity**:
   - Choose the simplest architecture that completely fulfills the requirements and allows testing. Avoid microservice sprawl or speculative layers.

---

### Step-by-Step Workflow
1. **Step 1: Analyze Constraints & Requirements**
   - Review business requirements and system load/latency expectations.
2. **Step 2: Identify Component Boundaries**
   - Map domain entities, use cases, and external interfaces.
3. **Step 3: Evaluate Alternatives**
   - Compare at least two viable architectural approaches, evaluating trade-offs, complexity, and failure modes.
4. **Step 4: Draft Architectural Decision Record (ADR)**
   - Format: Title, Context, Options Considered, Decision, Consequences, Status.
5. **Step 5: Record in DECISIONS.md**
   - Commit the new ADR to [`DECISIONS.md`](../../../DECISIONS.md).

---

### Quality Standards
- **Modularity**: Components can be replaced or mocked without modifying domain logic.
- **Traceability**: Every architectural decision has a clear, documented rationale.
- **Resilience**: Fault domains are isolated; failures in external services do not crash the core application.

---

### Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Dependency Inspection | Import / dependency graph analysis | Zero circular imports; zero outward dependencies from core domain |
| ADR Completeness | Review against ADR schema | Context, alternatives, decision, and consequences documented |

---

### Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Leaking Database Logic to Domain | Couples business rules to specific SQL/NoSQL tech | Use Repository interfaces with domain entity returns |
| Silent Architecture Reversal | Inconsistencies emerge between past and present code | Author superseding ADR explaining the pivot |

---

### Restrictions
- Do NOT introduce circular dependencies between modules.
- Do NOT introduce external frameworks without ADR documentation and justification.

---

### Expected Deliverables
- Architectural specification or module diagram.
- Recorded ADR in [`DECISIONS.md`](../../../DECISIONS.md).

---

### Documentation Requirements
- Update system architecture in [`CONTEXT.md`](../../../CONTEXT.md).
- Record architectural lessons learned in [`MEMORY.md`](../../../MEMORY.md).

---

## Level 3 — Optional References & Supplementary Assets
  - None (self-contained Level 1 & Level 2 guidance)
