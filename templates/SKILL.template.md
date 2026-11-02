---
name: skill-name
description: A clear, single-sentence summary of this skill's capability and primary objective.
version: 1.0.0
category: planning | requirements | architecture | development | design | quality | operations | documentation
tags: [tag1, tag2, tag3]
---

# Skill: [Skill Display Name]

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema.

---

## 1. Metadata
- **Identifier**: `[skill-name]`
- **Category**: `[Category Name]`
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
[Describe what this skill accomplishes, the fundamental engineering problem it solves, and why it exists in the framework.]

---

## 3. Scope
- **In-Scope**:
  - [Specific responsibility 1]
  - [Specific responsibility 2]
  - [Specific responsibility 3]
- **Out-of-Scope**:
  - [Excluded responsibility 1 — delegate to `skills/other-skill/SKILL.md`]
  - [Excluded responsibility 2]

---

## 4. When to Use
- [Trigger condition 1: When user asks for X]
- [Trigger condition 2: When lifecycle phase enters Y]
- [Trigger condition 3: When codebase signals need for Z]

---

## 5. When Not to Use
- [Condition 1: Use `skills/alternative-skill/SKILL.md` instead if...]
- [Condition 2: Do not use for non-visual/pure backend tasks if...]

---

## 6. Prerequisites
- [Prerequisite 1: Verified file or context required before starting]
- [Prerequisite 2: Task registered in `TASKS.md`]

---

## 7. Required Context
Before executing this skill, ensure the following project context has been verified:
- Current state in [`CONTEXT.md`](../CONTEXT.md).
- Mandatory constraints in [`RULES.md`](../RULES.md).
- Settled decisions in [`DECISIONS.md`](../DECISIONS.md).

---

## 8. Core Instructions
[Provide deep, actionable, domain-specific engineering principles. Avoid generic platitudes. Include specific patterns, architecture conventions, and concrete technical rules.]

---

## 9. Step-by-Step Workflow
1. **Step 1: [Phase Name]**
   - [Actionable instruction]
   - [Verification check]
2. **Step 2: [Phase Name]**
   - [Actionable instruction]
3. **Step 3: [Phase Name]**
   - [Actionable instruction]
4. **Step 4: [Phase Name]**
   - [Actionable instruction]

---

## 10. Quality Standards
- **Standard 1**: [Concrete measurable standard, e.g. test coverage, typing completeness]
- **Standard 2**: [Clean code & DRY criteria]
- **Standard 3**: [Maintainability & documentation criteria]

---

## 11. Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| [Check 1] | [Command or inspection] | [Measurable pass criteria] |
| [Check 2] | [Command or inspection] | [Measurable pass criteria] |

---

## 12. Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| [Mistake 1] | [Technical reason] | [Preferred pattern] |
| [Mistake 2] | [Technical reason] | [Preferred pattern] |

---

## 13. Restrictions
- Do NOT introduce external executable dependencies or runtime engines.
- Do NOT bypass security checks, sandboxes, or mandatory rules in [`RULES.md`](../RULES.md).
- Do NOT fabricate unverified file paths or test results.

---

## 14. Expected Deliverables
- [Deliverable 1: Target code files, schemas, or configs]
- [Deliverable 2: Accompanying tests]
- [Deliverable 3: Updated documentation in `docs_agent/` or `CONTEXT.md`]

---

## 15. Documentation Requirements
- Record technical discoveries and lessons learned in [`MEMORY.md`](../MEMORY.md).
- Record architectural trade-offs in [`DECISIONS.md`](../DECISIONS.md).
- Update task state in [`TASKS.md`](../TASKS.md) and log session in [`docs_agent/SESSION_LOG.md`](../docs_agent/SESSION_LOG.md).

