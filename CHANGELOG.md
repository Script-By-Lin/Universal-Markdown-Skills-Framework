# CHANGELOG.md — Release & Change Ledger
# Universal Markdown Skills Framework (UMSF)

> Canonical ledger of framework releases, architectural additions, and functional enhancements.  
> Format: Based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), adhering to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [Unreleased] — In Progress

---

## [1.2.2] — 2026-11-03

### Changed
- **Strict Relative Link Portability Across All Documents & Skills**:
  - Eliminated all machine-specific absolute paths (`file:///home/hexx/...` and `/home/hexx/...`) across all 82 files in the repository.
  - Converted 1,150+ internal file links across core governance files (`AGENTS.md`, `RULES.md`, `CONTEXT.md`, `WORKFLOW.md`, `SKILLS.md`, `TASKS.md`, `DECISIONS.md`, `MEMORY.md`, `README.md`, `CHANGELOG.md`), 370 skills, templates, and documentation to exact POSIX relative paths.
  - Resolved `AGENTS.md:L134` (`./TASKS.md`) and `skills/ui-ux-pro-max/SKILL.md:L21` (`./references/quick-reference.md`).
- **Portability Invariant Codified**:
  - Added Invariant 6 (Repository Portability & Relative Links Invariant) and anti-pattern entry to [`RULES.md`](./RULES.md).
- **Architectural Decision Record ADR-010 ([`DECISIONS.md`](./DECISIONS.md))**:
  - Ratified ADR-010: Strict Relative Paths and Repository Portability Invariant.

---

## [1.2.2] — 2026-11-03

### Changed
- **Strict Relative Link Portability Across All Documents & Skills**:
  - Eliminated all machine-specific absolute paths (`file:///home/<user>/...` and `/home/<user>/...`) across all 82 files in the repository.
  - Converted 1,150+ internal file links across core governance files (`AGENTS.md`, `RULES.md`, `CONTEXT.md`, `WORKFLOW.md`, `SKILLS.md`, `TASKS.md`, `DECISIONS.md`, `MEMORY.md`, `README.md`, `CHANGELOG.md`), 370 skills, templates, and documentation to exact POSIX relative paths.
  - Resolved `AGENTS.md:L134` (`./TASKS.md`) and `skills/ui-ux-pro-max/SKILL.md:L21` (`./references/quick-reference.md`).
- **Portability Invariant Codified**:
  - Added Invariant 6 (Repository Portability & Relative Links Invariant) and anti-pattern entry to [`RULES.md`](./RULES.md).
- **Architectural Decision Record ADR-010 ([`DECISIONS.md`](./DECISIONS.md))**:
  - Ratified ADR-010: Strict Relative Paths and Repository Portability Invariant.

---

## [1.2.1] — 2026-11-03

### Added
- **Pure Markdown Design Catalog ([`styles-and-palettes.md`](./skills/ui-ux-pro-max/references/styles-and-palettes.md))**:
  - Compiled the complete UI/UX Pro Max design intelligence into pure Markdown: 88 visual styles, 192 product color palettes, 74 font pairings, and 25 chart guides.
  - Enables any user and any AI coding agent to browse, select, and apply styles, palettes, and typography directly from Markdown without running CLI tools or interactive search.
- **Architectural Decision Record ADR-009 ([`DECISIONS.md`](./DECISIONS.md))**:
  - Ratified 100% self-contained Markdown skills architecture and elimination of interactive search CLI dependencies.

### Changed
- **UI/UX Pro Max Skill Modernization ([`skills/ui-ux-pro-max/SKILL.md`](./skills/ui-ux-pro-max/SKILL.md))**:
  - Completely rewritten to the canonical 15-section UMSF schema, removing all `${CLAUDE_PLUGIN_ROOT}` and mandatory CLI execution calls.
- **Foundational & UI Skills Decoupling**:
  - Updated [`skills/ui-ux-design/SKILL.md`](./skills/ui-ux-design/SKILL.md), [`skills/design/SKILL.md`](./skills/design/SKILL.md), and [`skills/frontend-development/SKILL.md`](./skills/frontend-development/SKILL.md) to use direct Markdown references.
- **ECC Skills Universalization**:
  - Decoupled `tdd-workflow`, `autonomous-loops`, `dmux-workflows`, `configure-ecc`, and `plan-canvas` from assumptions of external ECC checkouts or plugin roots.
- **Governance Updates**:
  - Updated [`RULES.md`](./RULES.md) (Section 2.5 and Section 14), [`WORKFLOW.md`](./WORKFLOW.md) (Stage 4), [`SKILLS.md`](./SKILLS.md), [`CONTEXT.md`](./CONTEXT.md), [`README.md`](./README.md), and [`MEMORY.md`](./MEMORY.md).

---

## [1.2.0] — 2026-11-03

### Added
- **16 Canonical Engineering Domains & Architecture**:
  - Structured the entire skills library into 16 canonical numbered domain directories under `skills/`:
    - `skills/01-software-development-lifecycle/`
    - `skills/02-security-engineering/`
    - `skills/03-software-architecture-and-design/`
    - `skills/04-requirements-and-business-analysis/`
    - `skills/05-programming-and-implementation/`
    - `skills/06-backend-engineering/`
    - `skills/07-frontend-engineering/`
    - `skills/08-database-engineering/`
    - `skills/09-quality-assurance-and-testing/`
    - `skills/10-devops-and-infrastructure/`
    - `skills/11-reliability-and-operations/`
    - `skills/12-code-quality-and-maintenance/`
    - `skills/13-performance-engineering/`
    - `skills/14-project-and-team-management/`
    - `skills/15-documentation-and-technical-communication/`
    - `skills/16-ai-agent-engineering/`
  - Dual-path backward compatibility: all skills accessible both via hierarchical domain paths and root symlinks.
- **35 New Advanced Testing, Security & AI Agent Skills**:
  - Added 12 Security Engineering Skills in Category 02: `security-testing`, `penetration-testing`, `web-application-security`, `api-security-testing`, `vulnerability-assessment`, `security-code-review`, `threat-modeling`, `dependency-security-audit`, `authentication-security`, `authorization-security`, `vulnerability-management`, `security-remediation-and-retesting`.
  - Added 16 Quality Assurance & Testing Skills in Category 09: `test-driven-development`, `unit-testing`, `integration-testing`, `system-testing`, `end-to-end-testing`, `regression-testing`, `acceptance-testing`, `exploratory-testing`, `test-automation`, `test-coverage-analysis`, `mutation-testing`, `performance-testing`, `load-and-stress-testing`, `test-strategy-and-planning`, `test-data-management`, `defect-management`.
  - Added 7 AI Agent Engineering Skills in Category 16: `independent-qa-agent`, `independent-security-review-agent`, `multi-agent-verification`, `adversarial-testing`, `agent-handoff-and-review`, `evidence-based-validation`, `agent-role-separation`.
  - All 35 skills authored in full 15-section UMSF schema with actionable workflows, checklists, and acceptance criteria.
  - Total catalog expanded to **370 skills**.
- **Mandatory Test-Driven Development (TDD) Red-Green-Refactor Protocol**:
  - Formalized in [`RULES.md`](./RULES.md) (Section 7) and [`WORKFLOW.md`](./WORKFLOW.md) (Stage 5).
  - Absolute prohibitions against post-hoc test authoring, test relaxation, or claiming unverified passes.
- **Tripartite Agent Architecture & Execution Modes**:
  - Formalized Agent A (Development), Agent B (Independent QA), and Agent C (Independent Security) in [`AGENTS.md`](./AGENTS.md) (Section 2) and [`RULES.md`](./RULES.md) (Section 8).
  - Enforced Mode 1 (concurrent subagent verification) and Mode 2 (sequential single-agent role-switching passes).
  - Absolute ban on developer self-approval.
- **Authorized Penetration Testing & Vulnerability Lifecycle**:
  - Codified strict authorization scope, non-destructive tools, and zero data exfiltration invariants in [`RULES.md`](./RULES.md) (Section 9) and [`WORKFLOW.md`](./WORKFLOW.md) (Stage 7).
  - Defined 10-stage Vulnerability Management Lifecycle with 5-tier risk severity classification.
  - Enforced mandatory independent security retesting before closing any vulnerability.
- **Four-Tier Release Gates**:
  - Codified in [`RULES.md`](./RULES.md) (Section 10) and [`WORKFLOW.md`](./WORKFLOW.md) (Stage 8): Functional, Regression, Security, and Documentation Gates.
- **11 Project Testing & Security Scaffolding Templates**:
  - Added 11 standardized templates to [`templates/`](./templates/): `TEST_STRATEGY.template.md`, `TDD_LOG.template.md`, `TEST_RESULTS.md`, `REGRESSION_REPORT.md`, `QA_ASSESSMENT.md`, `SECURITY_TEST_PLAN.md`, `THREAT_MODEL.md`, `SECURITY_ASSESSMENT.md`, `VULNERABILITY_REGISTER.md`, `PENETRATION_TEST_REPORT.md`, `RETEST_REPORT.md`.
  - Preserved the empty user-project `/docs_agent/` initialization invariant.
- **Architectural Decision Record ADR-008**:
  - Ratified in [`DECISIONS.md`](./DECISIONS.md): Comprehensive Testing, Test-Driven Development (TDD), and AI Security Engineering Architecture.
- **Central Registries & Memory Updates**:
  - Completely updated [`SKILLS.md`](./SKILLS.md) to index all 370 skills across 16 domains with role mappings.
  - Updated [`MEMORY.md`](./MEMORY.md) with critical lessons on TDD confirmation bias, destructive security probing, and single-agent self-approval avoidance.

---

## [1.1.0] — 2026-11-03

### Added
- **UI/UX Pro Max Design Intelligence Suite Integration**:
  - Fully integrated the flagship design intelligence system into `skills/ui-ux-pro-max/`:
    - Zero-dependency BM25 CLI search tool (`skills/ui-ux-pro-max/scripts/search.py`) querying styles, palettes, typography, guidelines, icons, charts, and platform stacks.
    - 20+ CSV and JSON datasets (`skills/ui-ux-pro-max/data/`): 79 visual styles, 192 product palettes, 74 font pairings, 119 UX guidelines, 105 SVG icons, 25 chart guides, and 16 framework stacks.
    - 24 platform configurations and base templates (`skills/ui-ux-pro-max/templates/`).
    - Reference manuals (`skills/ui-ux-pro-max/references/`): `pro-rules.md` and `quick-reference.md`.
  - Integrated 6 specialized companion UI skills from `ui-ux-pro-max-skill`:
    - `banner-design`: Hero layouts, social cards, marketing banners.
    - `brand`: Brand strategy, voice, tone, and brand compliance.
    - `design`: General visual hierarchy, spatial layout, composition.
    - `design-system`: 3-layer token architecture, component specs, slide generator, and visual consistency audit.
    - `slides`: Executive presentation decks, pitch templates, visual storytelling.
    - `ui-styling`: Canvas font rendering (22 bundled OFL fonts) and advanced CSS layouts.
- **313 Specialized Domain Skills Integration (from Everything Claude Code / ECC)**:
  - Integrated 313 modular domain skills into `skills/`, expanding framework capabilities across 8 disciplines:
    - Agentic AI, Autonomous Loops & LLM Systems (103 skills)
    - Architecture, Governance, Workflows & Developer Operations (85 skills)
    - Frontend Engineering, UI Frameworks & Mobile (37 skills)
    - Testing, QA, Penetration Testing & Security (24 skills)
    - Backend Engineering, Distributed Systems & Microservices (23 skills)
    - Database Systems, Storage & Data Pipelines (21 skills)
    - Language Patterns & Core Runtimes (11 skills)
    - Cloud, Infrastructure, Containers & DevOps (9 skills)
- **Central Registry Expansion ([`SKILLS.md`](./SKILLS.md))**:
  - Upgraded registry to index all 335 active skills with direct file links and concise summaries.
  - Documented Three-Tier Architecture (Tier 1 Foundational, Tier 2 UI/UX Pro Max, Tier 3 Domain Specialties).
  - Documented CLI search commands and multi-skill pairing recommendations.
- **Foundational Skill Synergy**:
  - Enhanced [`skills/ui-ux-design/SKILL.md`](./skills/ui-ux-design/SKILL.md) to directly command `search.py` CLI and reference datasets.
  - Enhanced [`skills/frontend-development/SKILL.md`](./skills/frontend-development/SKILL.md) to cross-reference design system tokens and audit tools.
- **Architectural Decision Record ADR-007 ([`DECISIONS.md`](./DECISIONS.md))**:
  - Ratified three-tier skills architecture and local-first search CLI integration.

---

## [1.0.0-phase4] — 2026-11-03

### Added
- **Project Context System ([`CONTEXT.md`](./CONTEXT.md))**:
  - Verified snapshot of repository reality: technology stack, directory layout, 15 canonical skills, preserved assets, and boundaries.
- **Persistent Knowledge Base ([`MEMORY.md`](./MEMORY.md))**:
  - Long-term organizational memory preserving zero-dependency conventions, UI/UX Pro Max invariants (Swiss style, WCAG AA 4.5:1, 44px hit size, no emojis), common technical pitfalls, and reusable reproduction patterns.
- **Architectural Decision Records ([`DECISIONS.md`](./DECISIONS.md))**:
  - Immutable ADR ledger formalizing ADRs 001 through 006:
    - ADR-001: Zero-Dependency, Markdown-Only Core Architecture
    - ADR-002: Adoption of UI/UX Pro Max as Canonical Design Intelligence Standard
    - ADR-003: Explicit 7-Tier Precedence Hierarchy and Conflict Resolution Matrix
    - ADR-004: Standardized 15-Section Canonical Schema for Domain Skills
    - ADR-005: Maximum Two-Skill Loading Protocol for Context Conservation
    - ADR-006: Tripartite Separation of Reality, Memory, and Decisions
- **Scaffolding Templates**:
  - Added [`templates/CONTEXT.template.md`](./templates/CONTEXT.template.md).
  - Added [`templates/MEMORY.template.md`](./templates/MEMORY.template.md).
  - Added [`templates/DECISIONS.template.md`](./templates/DECISIONS.template.md).
- **Phase 4 Report ([`docs_agent/phases/PHASE_04_CONTEXT_MEMORY.md`](./docs_agent/phases/PHASE_04_CONTEXT_MEMORY.md))**.

---

## [1.0.0-phase3] — 2026-11-03

### Added
- **Central Skill Registry ([`SKILLS.md`](./SKILLS.md))**:
  - Published discovery flowchart, pairing rules, and new skill authoring guidelines.
- **Skill Scaffolding Template ([`templates/SKILL.template.md`](./templates/SKILL.template.md))**:
  - Canonical 15-section UMSF template.
- **Skill Library Index ([`skills/README.md`](./skills/README.md))**:
  - Catalog of 15 modular canonical domain skills.
- **Canonical Skill Library (`skills/*/SKILL.md`)**:
  - Created 15 complete domain skills strictly adhering to the 15-section schema:
    - Strategy: [`planning`](./skills/planning/SKILL.md), [`requirements-analysis`](./skills/requirements-analysis/SKILL.md)
    - Architecture: [`software-architecture`](./skills/software-architecture/SKILL.md)
    - Development: [`backend-development`](./skills/backend-development/SKILL.md), [`frontend-development`](./skills/frontend-development/SKILL.md), [`database-design`](./skills/database-design/SKILL.md), [`api-development`](./skills/api-development/SKILL.md)
    - UI/UX: [`ui-ux-design`](./skills/ui-ux-design/SKILL.md) (UI/UX Pro Max intelligence, Swiss style, contrast ≥ 4.5:1, 44px hit targets)
    - Quality: [`testing`](./skills/testing/SKILL.md), [`code-review`](./skills/code-review/SKILL.md), [`performance`](./skills/performance/SKILL.md)
    - Diagnostics: [`debugging`](./skills/debugging/SKILL.md)
    - Modernization: [`refactoring`](./skills/refactoring/SKILL.md)
    - Continuity: [`documentation`](./skills/documentation/SKILL.md)
- **Phase 3 Report ([`docs_agent/phases/PHASE_03_SKILLS.md`](./docs_agent/phases/PHASE_03_SKILLS.md))**.

---

## [1.0.0-phase2] — 2026-11-02

### Added
- **Mandatory Constraints ([`RULES.md`](./RULES.md))**:
  - Framework invariants, clean code, security standards, anti-pattern blacklist.
  - **UI/UX Pro Max Invariants** elevated to Precedence Level 2.
- **Engineering Lifecycle ([`WORKFLOW.md`](./WORKFLOW.md))**:
  - 9-stage engineering lifecycle with gates and category adaptations.
- **Phase 2 Report ([`docs_agent/phases/PHASE_02_INSTRUCTIONS.md`](./docs_agent/phases/PHASE_02_INSTRUCTIONS.md))**.

### Changed
- **Universal Entry Point ([`AGENTS.md`](./AGENTS.md))**:
  - Upgraded to version `1.0.0-phase2` with 7-tier Precedence Hierarchy, Conflict Resolution Matrix, and Cross-Agent Adapters.

---

## [1.0.0-phase1] — 2026-11-02

### Added
- **Repository Architecture**: Initialized canonical UMSF directory hierarchy: `skills/` (15 subdirectories), `templates/`, `docs_agent/phases/`.
- **Framework Entry Point**: Created initial [`AGENTS.md`](./AGENTS.md).
- **Documentation & Tracking System**:
  - [`README.md`](./README.md), [`LICENSE`](./LICENSE), [`docs_agent/ARCHITECTURE.md`](./docs_agent/ARCHITECTURE.md), [`docs_agent/IMPLEMENTATION_STATUS.md`](./docs_agent/IMPLEMENTATION_STATUS.md), [`docs_agent/PHASE_HISTORY.md`](./docs_agent/PHASE_HISTORY.md), [`docs_agent/DEVELOPMENT_LOG.md`](./docs_agent/DEVELOPMENT_LOG.md), [`docs_agent/CHANGE_HISTORY.md`](./docs_agent/CHANGE_HISTORY.md), [`docs_agent/SESSION_LOG.md`](./docs_agent/SESSION_LOG.md), [`docs_agent/phases/PHASE_01_FOUNDATION.md`](./docs_agent/phases/PHASE_01_FOUNDATION.md).

