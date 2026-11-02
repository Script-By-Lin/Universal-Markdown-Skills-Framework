---
name: software-architecture
description: Principles and workflows for high-level system design, layer separation, modularity, and Architectural Decision Records (ADRs).
version: 1.0.0
category: architecture
tags: [architecture, system-design, modularity, clean-architecture, adr]
---

# Skill: Software Architecture & System Design

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.

---

## 1. Metadata
- **Identifier**: `software-architecture`
- **Category**: Architecture & Design
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
This skill governs system architecture, modular decomposition, dependency management, boundary enforcement, and the formal drafting of Architectural Decision Records (ADRs) to ensure long-term codebase maintainability and prevent technical debt.

---

## 3. Scope
- **In-Scope**:
  - Defining structural module boundaries and dependency directions.
  - Applying Clean Architecture and Ports-and-Adapters patterns.
  - Evaluating technical trade-offs between architectural alternatives.
  - Formulating immutable Architectural Decision Records (ADRs) in [`DECISIONS.md`](../../DECISIONS.md).
- **Out-of-Scope**:
  - Low-level component styling and UI widgets (delegate to [`skills/ui-ux-design/SKILL.md`](../ui-ux-design/SKILL.md)).
  - Detailed database index tuning (delegate to [`skills/database-design/SKILL.md`](../database-design/SKILL.md)).

---

## 4. When to Use
- When introducing a new service, subsystem, library, or core data pipeline.
- When an existing architecture faces scaling, decoupling, or testability bottlenecks.
- Before committing to significant technology choices or non-trivial refactoring.

---

## 5. When Not to Use
- For isolated bug fixes within established module boundaries.
- For minor documentation or configuration updates.

---

## 6. Prerequisites
- Verified understanding of existing architecture via [`CONTEXT.md`](../../CONTEXT.md).
- Settled decisions reviewed in [`DECISIONS.md`](../../DECISIONS.md).

---

## 7. Required Context
- Architectural invariants in [`docs_agent/ARCHITECTURE.md`](../../docs_agent/ARCHITECTURE.md).
- Repository rules in [`RULES.md`](../../RULES.md).

---

## 8. Core Instructions
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

## 9. Step-by-Step Workflow
1. **Step 1: Analyze Constraints & Requirements**
   - Review business requirements and system load/latency expectations.
2. **Step 2: Identify Component Boundaries**
   - Map domain entities, use cases, and external interfaces.
3. **Step 3: Evaluate Alternatives**
   - Compare at least two viable architectural approaches, evaluating trade-offs, complexity, and failure modes.
4. **Step 4: Draft Architectural Decision Record (ADR)**
   - Format: Title, Context, Options Considered, Decision, Consequences, Status.
5. **Step 5: Record in DECISIONS.md**
   - Commit the new ADR to [`DECISIONS.md`](../../DECISIONS.md).

---

## 10. Quality Standards
- **Modularity**: Components can be replaced or mocked without modifying domain logic.
- **Traceability**: Every architectural decision has a clear, documented rationale.
- **Resilience**: Fault domains are isolated; failures in external services do not crash the core application.

---

## 11. Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Dependency Inspection | Import / dependency graph analysis | Zero circular imports; zero outward dependencies from core domain |
| ADR Completeness | Review against ADR schema | Context, alternatives, decision, and consequences documented |

---

## 12. Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Leaking Database Logic to Domain | Couples business rules to specific SQL/NoSQL tech | Use Repository interfaces with domain entity returns |
| Silent Architecture Reversal | Inconsistencies emerge between past and present code | Author superseding ADR explaining the pivot |

---

## 13. Restrictions
- Do NOT introduce circular dependencies between modules.
- Do NOT introduce external frameworks without ADR documentation and justification.

---

## 14. Expected Deliverables
- Architectural specification or module diagram.
- Recorded ADR in [`DECISIONS.md`](../../DECISIONS.md).

---

## 15. Documentation Requirements
- Update system architecture in [`CONTEXT.md`](../../CONTEXT.md).
- Record architectural lessons learned in [`MEMORY.md`](../../MEMORY.md).

