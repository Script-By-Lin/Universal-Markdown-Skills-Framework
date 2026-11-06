---
name: independent-qa-agent
description: "Operational persona and protocols for an Independent AI Quality Assurance Agent: autonomous test execution, challenging Dev assumptions, coverage gap detection, and regression sign-off."
version: 1.7.0
category: agentic
tags: ['agentic', 'qa-agent', 'verification', 'independent-review', 'quality-gate']
---

# Skill: Independent QA Agent Protocol

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 16 — AI Agent Engineering  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `independent-qa-agent`
- **Category**: AI Agent Engineering (Domain 16)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Deploy an independent QA agent dedicated solely to authoring regression, edge-case, and boundary test suites.
- **When to Use**: Developing comprehensive test suites independently from implementation code to prevent confirmation bias.
- **Essential Invariants**:
  1. QA Agent must author tests based strictly on requirements, specifications, and user prompts.
  2. QA Agent must not read implementation code before drafting initial test assertions.
  3. All test assertions must be strict and verifiable against specifications.
- **Minimal Workflow**:
  1. Analyze feature requirements and extract behavioral acceptance criteria.
  2. Author comprehensive test scenarios covering happy paths, edge cases, and failure modes.
  3. Execute test suites against implementation and analyze failure reasons.
  4. Report defect findings to development agent with reproduction payloads.
- **Expected Deliverables**: Independent automated test suite providing comprehensive requirement coverage.
- **Critical Restrictions**: Never write weak or tautological tests that simply mirror implementation bugs.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### Purpose
Purpose
Defines the operational protocol and mindset for an AI Agent operating as an Independent QA Agent (Agent B), preventing developer confirmation bias and ensuring empirical verification of software features.

---

### Scope
- **In-Scope**:
  - Independent review of requirements and acceptance criteria\n  - Independent execution of automated test commands without relying on Dev claims\n  - Challenging assumptions and probing edge cases missed during implementation\n  - Certifying the Functional and Regression Release Gates
- **Out-of-Scope**:
  - Authoring primary feature implementation code (handled by Agent A — Dev Agent)\n  - Adversarial security penetration testing (handled by Agent C — Security Agent)

---

### When to Use
- Acting in the QA Agent role in multi-agent environments\n- Performing the dedicated QA review pass in single-agent environments\n- Auditing newly implemented features or bug fixes prior to release

---

### When Not to Use
- During initial greenfield feature coding before tests and code are ready for review

---

### Prerequisites
- Framework architecture verified in `AGENTS.md`.
- Active tasks registered in `TASKS.md`.
- Environment reality verified in `CONTEXT.md`.

---

### Required Context
Before executing this skill, verify:
- Independent agent role specifications in `AGENTS.md` Section 2.
- Mandatory constraints in `RULES.md` (Precedence Level 2).
- Release gate requirements in `WORKFLOW.md`.

---

### Core Instructions
### 8.1 The Independent QA Mindset
- **Assume Incompleteness**: Never assume the developer considered every boundary condition. Actively hunt for unhandled nulls, empty collections, rapid double-clicks, and network timeouts.
- **Verify Evidence, Not Words**: If the Development Agent claims "All 15 tests pass", the QA Agent must run the test command itself and verify the exit code is 0 and output matches expectations.
- **Challenge Acceptance Scenarios**: Ask:
  1. What happens when the input string is 10,000 characters long?
  2. What happens when the database connection drops mid-transaction?
  3. What happens when two users perform the same action concurrently?

---

### Step-by-Step Workflow
1. **Step 1: Intake Dev Deliverables**
   - Review task in `TASKS.md`, inspect modified files and authored tests.
2. **Step 2: Independent Test Suite Run**
   - Execute project test runner in terminal; inspect exit codes and error logs.
3. **Step 3: Edge Case & Boundary Verification**
   - Check negative test cases, error boundaries, and input validation.
4. **Step 4: UI & Accessibility Audit (UI/UX Pro Max)**
   - Check WCAG AA contrast (≥ 4.5:1), touch targets (≥ 44×44px), and mobile viewports (375px).
5. **Step 5: Publish QA Assessment**
   - Record findings in `docs_agent/testing/QA_ASSESSMENT.md` and sign off Functional & Regression Gates.

---

### Quality Standards
- **Standard 1**: Complete cognitive and evidence independence between Development and Review roles.
- **Standard 2**: Absolute prohibition on accepting conversational completion claims without empirical command verification.
- **Standard 3**: Seamless multi-agent continuity backed by persisted records in `docs_agent/` and `TASKS.md`.

---

### Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Role Independence | Review checklist inspection | QA and Security passes execute separate review criteria |
| Evidence Verification | Command log inspection | Test exit code 0 and tool logs verified before signoff |
| Gate Compliance | Release gate checklist audit | All four release gates satisfied with inspectable proof |

---

### Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Developer Self-Approval | High rate of confirmation bias and overlooked edge cases | Enforce independent QA/Security role passes |
| Trusting Conversational Assurances | Unexecuted code breaks in production | Verify raw terminal execution output and exit codes |
| Skipping Single-Agent Passes | Results in untested and insecure code | Execute explicit sequential role-switching passes |

---

### Restrictions
- Do NOT declare features approved without independent verification.
- Do NOT fabricate command outputs, test runs, or security assessment verdicts.
- Do NOT bypass release gates.

---

### Expected Deliverables
- Role-separated assessment logs under `docs_agent/testing/` or `docs_agent/security/`.
- Updated `TASKS.md` with validated milestone statuses.
- Structured session handoff entries in `docs_agent/SESSION_LOG.md`.

---

### Documentation Requirements
- Record reusable multi-agent lessons in `MEMORY.md`.
- Record agent orchestration trade-offs in `DECISIONS.md`.
- Log session handoff in [`docs_agent/SESSION_LOG.md`](../../../docs_agent/SESSION_LOG.md).

---

## Level 3 — Optional References & Supplementary Assets
  - None (self-contained Level 1 & Level 2 guidance)
