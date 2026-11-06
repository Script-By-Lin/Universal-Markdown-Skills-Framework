# UMSF Universal Software Engineering Skills Library

> Standardized Domain Knowledge Modules for Autonomous AI Coding Agents  
> Specification: Canonical 15-Section Universal Markdown Skills Schema  
> Total Cataloged Skills: 77 Core Domain Skills Across 16 Canonical Engineering Domains  

---

## 1. Domain Organization

The skills library is organized into 16 standardized engineering domains covering the entire Software Development Lifecycle (SDLC):

- **Domain 01 — Software Development Lifecycle (SDLC)** ([`skills/01-software-development-lifecycle/`](./01-software-development-lifecycle/)): 1 Core Skill (`planning`)
- **Domain 02 — Security Engineering & Penetration Testing** ([`skills/02-security-engineering/`](./02-security-engineering/)): 13 Core Skills (`security`, `penetration-testing`, `web-application-security`, `api-security-testing`, `vulnerability-assessment`, `security-code-review`, `threat-modeling`, `dependency-security-audit`, `authentication-security`, `authorization-security`, `vulnerability-management`, `security-remediation-and-retesting`, `security-testing`)
- **Domain 03 — Software Architecture & System Design** ([`skills/03-software-architecture-and-design/`](./03-software-architecture-and-design/)): 2 Core Skills (`software-architecture`, `architecture-decision-records`)
- **Domain 04 — Requirements & Business Analysis** ([`skills/04-requirements-and-business-analysis/`](./04-requirements-and-business-analysis/)): 1 Core Skill (`requirements-analysis`)
- **Domain 05 — Programming & Implementation** ([`skills/05-programming-and-implementation/`](./05-programming-and-implementation/)): 2 Core Skills (`debugging`, `refactoring`)
- **Domain 06 — Backend Engineering & Distributed Systems** ([`skills/06-backend-engineering/`](./06-backend-engineering/)): 3 Core Skills (`backend-development`, `api-development`, `backend-patterns`)
- **Domain 07 — Frontend Engineering & UI/UX Pro Max** ([`skills/07-frontend-engineering/`](./07-frontend-engineering/)): 1 Core Skill (`ui-ux-pro-max`)
- **Domain 08 — Database Engineering & Storage** ([`skills/08-database-engineering/`](./08-database-engineering/)): 3 Core Skills (`database-design`, `database-migrations`, `database-query-optimization`)
- **Domain 09 — Quality Assurance & Software Testing** ([`skills/09-quality-assurance-and-testing/`](./09-quality-assurance-and-testing/)): 18 Core Skills (`feature-integration-verification`, `test-driven-development`, `testing`, `unit-testing`, `integration-testing`, `system-testing`, `end-to-end-testing`, `regression-testing`, `acceptance-testing`, `exploratory-testing`, `test-automation`, `test-coverage-analysis`, `mutation-testing`, `performance-testing`, `load-and-stress-testing`, `test-strategy-and-planning`, `test-data-management`, `defect-management`)
- **Domain 10 — DevOps, Containers & Infrastructure** ([`skills/10-devops-and-infrastructure/`](./10-devops-and-infrastructure/)): 2 Core Skills (`docker-patterns`, `kubernetes-patterns`)
- **Domain 11 — Reliability & Production Operations** ([`skills/11-reliability-and-operations/`](./11-reliability-and-operations/)): 1 Core Skill (`canary-watch`)
- **Domain 12 — Code Quality, Review & Maintenance** ([`skills/12-code-quality-and-maintenance/`](./12-code-quality-and-maintenance/)): 2 Core Skills (`code-review`, `post-task-verification`)
- **Domain 13 — Performance Engineering & Profiling** ([`skills/13-performance-engineering/`](./13-performance-engineering/)): 2 Core Skills (`performance`, `benchmark-optimization-loop`)
- **Domain 14 — Project & Team Delivery Management** ([`skills/14-project-and-team-management/`](./14-project-and-team-management/)): 1 Core Skill (`counterparty-channel-discipline`)
- **Domain 15 — Documentation & Technical Writing** ([`skills/15-documentation-and-technical-communication/`](./15-documentation-and-technical-communication/)): 2 Core Skills (`documentation`, `article-writing`)
- **Domain 16 — AI Agent Engineering & Multi-Agent Systems** ([`skills/16-ai-agent-engineering/`](./16-ai-agent-engineering/)): 12 Core Skills (`agentic-engineering`, `independent-verification-subagent`, `independent-qa-agent`, `independent-security-review-agent`, `multi-agent-verification`, `adversarial-testing`, `agent-handoff-and-review`, `evidence-based-validation`, `agent-role-separation`, `autonomous-loops`, `prompt-optimizer`, `mcp-server-patterns`)

---

## 2. Tripartite Agent Roles & Subagent Verification

1. **Agent A — Primary Development Agent**: Drives TDD Red-Green-Refactor, feature implementation, and developer tests. Cannot self-approve deliverables.
2. **Agent B — Independent Verification Subagent**: Dispatched in an isolated subagent context to independently evaluate requirements, diffs, test execution (exit code 0), architecture, code quality, security coordination, and doc sync.
3. **Agent C — Independent Security Agent**: Adversarial posture, threat modeling, authorized non-destructive penetration testing, and vulnerability retesting.
4. **Mandatory Post-Task Verification**: All agents execute [`post-task-verification`](./12-code-quality-and-maintenance/post-task-verification/SKILL.md) and [`independent-verification-subagent`](./16-ai-agent-engineering/independent-verification-subagent/SKILL.md) prior to closing any task.

---

## 3. Pure Markdown UI/UX Design Intelligence

All design intelligence is self-contained in Markdown catalogs—zero CLI tools, packages, or interactive search needed:
- [`skills/ui-ux-pro-max/references/styles-and-palettes.md`](./ui-ux-pro-max/references/styles-and-palettes.md): 88 visual styles, 192 product palettes, 74 font pairings, and chart types.
- [`skills/ui-ux-pro-max/references/quick-reference.md`](./ui-ux-pro-max/references/quick-reference.md): All 10 priority rule categories and 119 UX guidelines.
- [`skills/ui-ux-pro-max/references/pro-rules.md`](./ui-ux-pro-max/references/pro-rules.md): Mobile polish rules and canonical Pre-Delivery Checklist.

---

## 4. Master Central Registry

Consult `SKILLS.md` at the repository root for complete selection matrices, role assignments, and direct clickable links to all 64 skills.
