# Architectural Decision Records (ADRs)
# Universal Markdown Skills Framework (UMSF)

> Immutable Ledger of System Design Decisions, Trade-Offs, and Consequences  
> Authority: Precedence Level 3 (System Invariants & Historical ADRs)  

---

## ADR Index

| Decision ID | Date | Title | Status | Superseded By |
|---|---|---|---|---|
| [`ADR-001`](#adr-001-zero-dependency-markdown-only-core-architecture) | 2026-11-02 | Zero-Dependency, Markdown-Only Core Architecture | **Accepted** | — |
| [`ADR-002`](#adr-002-adoption-of-uiux-pro-max-as-canonical-design-intelligence) | 2026-11-02 | Adoption of UI/UX Pro Max as Canonical Design Intelligence | **Accepted** | — |
| [`ADR-003`](#adr-003-explicit-7-tier-precedence-hierarchy-and-conflict-resolution) | 2026-11-02 | Explicit 7-Tier Precedence Hierarchy and Conflict Resolution | **Accepted** | — |
| [`ADR-004`](#adr-004-standardized-15-section-canonical-schema-for-domain-skills) | 2026-11-03 | Standardized 15-Section Canonical Schema for Domain Skills | **Accepted** | — |
| [`ADR-005`](#adr-005-maximum-two-skill-loading-protocol-for-context-conservation) | 2026-11-03 | Maximum Two-Skill Loading Protocol for Context Conservation | **Superseded** | [`ADR-011`](#adr-011-post-task-verification-gate-dynamic-context-aware-skill-loading--risk-proportionate-delivery) |
| [`ADR-006`](#adr-006-tripartite-separation-of-reality-memory-and-decisions) | 2026-11-03 | Tripartite Separation of Reality, Memory, and Decisions | **Accepted** | — |
| [`ADR-007`](#adr-007-three-tier-hierarchical-skills-library-and-local-search-cli) | 2026-11-03 | Three-Tier Hierarchical Skills Library & Local Search CLI | **Accepted** | — |
| [`ADR-008`](#adr-008-comprehensive-testing-test-driven-development-tdd-and-ai-security-engineering-architecture) | 2026-11-03 | Comprehensive Testing, TDD, and AI Security Engineering | **Accepted** | — |
| [`ADR-009`](#adr-009-self-contained-markdown-skills-and-zero-search-cli-dependency) | 2026-11-03 | Self-Contained Markdown Skills & Zero Search CLI Dependency | **Accepted** | — |
| [`ADR-010`](#adr-010-strict-relative-paths-and-repository-portability-invariant) | 2026-11-03 | Strict Relative Paths and Repository Portability Invariant | **Accepted** | — |
| [`ADR-011`](#adr-011-post-task-verification-gate-dynamic-context-aware-skill-loading--risk-proportionate-delivery) | 2026-11-03 | Post-Task Verification Gate, Dynamic Skill Loading & Risk-Proportionate Delivery | **Accepted** | — |
| [`ADR-012`](#adr-012-independent-verification-subagent-architecture--structured-tripartite-delegation-protocol) | 2026-11-03 | Independent Verification Subagent Architecture & Structured Tripartite Delegation Protocol | **Accepted** | — |

---

## ADR-001: Zero-Dependency, Markdown-Only Core Architecture

- **Date**: 2026-11-02
- **Status**: Accepted
- **Deciders**: Principal Software Architect & AI Agent Systems Architect
- **Supersedes**: None

### 1. Context & Problem Statement
AI coding frameworks often introduce proprietary binaries, Node.js packages, Python skill runners, or remote vector databases. This creates brittle dependency manifests (`package.json`, `requirements.txt`), limits cross-agent portability, introduces supply-chain risks, and forces users to install specific runtime environments.

### 2. Alternatives Considered
1. **Option A: Python CLI / Skill Engine**: A local Python CLI package executing skills and managing context vectors.
2. **Option B: Node.js / NPM Plugin Package**: A TypeScript CLI daemon with SQLite memory storage.
3. **Option C: Pure Markdown Specification**: A zero-dependency, local-first repository structure of standard Markdown (`.md`) files interpreted natively by LLM agents.

### 3. Decision Outcome
**Selected Option**: **Option C: Pure Markdown Specification**  
UMSF operates strictly through structured Markdown documentation, YAML frontmatter metadata, and native agent reasoning. No package manifests, runtimes, or database engines are permitted in the framework core.

### 4. Consequences & Trade-offs
- **Positive Impacts**:
  - Zero installation friction: Developers can drop UMSF into any repository instantly.
  - Universal agent compatibility across Claude Code, Cursor, Antigravity, Windsurf, Codex, Gemini CLI, and Copilot.
  - 100% sovereign, local-first security without network leakage.
- **Negative Impacts / Known Trade-offs**:
  - Enforcement depends on the AI agent's prompt compliance rather than strict compiler-enforced types.
  - Mitigated by explicit 10-step initialization procedures in [`AGENTS.md`](./AGENTS.md) and strict constraints in [`RULES.md`](./RULES.md).

---

## ADR-002: Adoption of UI/UX Pro Max as Canonical Design Intelligence

- **Date**: 2026-11-02
- **Status**: Accepted
- **Deciders**: Principal Software Architect & AI Agent Systems Architect
- **Supersedes**: None

### 1. Context & Problem Statement
AI coding agents frequently generate low-quality, inconsistent user interfaces featuring arbitrary colors, low text contrast, broken mobile layouts, missing focus indicators, and raw emojis as buttons. The framework required an authoritative, production-grade design intelligence standard.

### 2. Alternatives Considered
1. **Option A: Generic Accessibility Bullet Points**: Relying on brief ad-hoc text prompts.
2. **Option B: Full UI/UX Pro Max Integration**: Embedding the design intelligence, semantic token systems, Swiss & Minimalism visual standard, and 10 prioritized rule categories from `ui-ux-pro-max-skill`.

### 3. Decision Outcome
**Selected Option**: **Option B: Full UI/UX Pro Max Integration**  
Elevate UI/UX Pro Max standards to Precedence Level 2 (`RULES.md`) and author dedicated design skills (`skills/ui-ux-design/SKILL.md` and `skills/frontend-development/SKILL.md`).

### 4. Consequences & Trade-offs
- **Positive Impacts**:
  - Deterministic visual quality: Swiss & Minimalism style, primary `#0F172A`, accent `#22C55E`, background `#020617`.
  - Guaranteed WCAG AA 4.5:1 text contrast and 44×44px minimum touch targets.
  - Strict prohibition against using raw emojis as UI icons.
  - Mobile-first responsiveness across 375px, 768px, 1024px, and 1440px breakpoints.
- **Negative Impacts / Known Trade-offs**:
  - Agents must enforce tokenized styling instead of writing quick inline hex styles. This is an intentional quality constraint.

---

## ADR-003: Explicit 7-Tier Precedence Hierarchy and Conflict Resolution

- **Date**: 2026-11-02
- **Status**: Accepted
- **Deciders**: Principal Software Architect & AI Agent Systems Architect
- **Supersedes**: None

### 1. Context & Problem Statement
When multiple instruction files exist (`AGENTS.md`, `RULES.md`, `CONTEXT.md`, `SKILL.md`, user prompts), agents can encounter conflicting directions, leading to unpredictable behavior or silent safety bypasses.

### 2. Alternatives Considered
1. **Option A: Flat Priority**: Treat all instructions equally and rely on the model to resolve conflicts.
2. **Option B: Explicit Seven-Tier Hierarchy**: Codify strict ranking: User Prompt (L1) -> `RULES.md` (L2) -> `ARCHITECTURE.md` & `DECISIONS.md` (L3) -> `CONTEXT.md` (L4) -> `WORKFLOW.md` (L5) -> `skills/*/SKILL.md` (L6) -> `AGENTS.md` (L7), paired with a deterministic conflict resolution matrix.

### 3. Decision Outcome
**Selected Option**: **Option B: Explicit Seven-Tier Hierarchy**  
Mandate the 7-tier model across all agent entry points and documentation.

### 4. Consequences & Trade-offs
- **Positive Impacts**:
  - Deterministic tie-breaking: `RULES.md` strictly overrides user prompt if a forbidden pattern (e.g. skipping security checks) is requested.
  - Verified filesystem code strictly overrides outdated documentation in `CONTEXT.md`.
- **Negative Impacts / Known Trade-offs**:
  - Agents must spend initial turns evaluating precedence when conflicts occur.

---

## ADR-004: Standardized 15-Section Canonical Schema for Domain Skills

- **Date**: 2026-11-03
- **Status**: Accepted
- **Deciders**: Principal Software Architect & AI Agent Systems Architect
- **Supersedes**: None

### 1. Context & Problem Statement
Ad-hoc skill files with varying structures make it difficult for agents to locate actionable workflows, preconditions, or quality standards reliably.

### 2. Alternatives Considered
1. **Option A: Free-form Markdown Documentation**: Allow each skill author to structure documents as desired.
2. **Option B: Canonical 15-Section Schema**: Enforce identical 15 sections across every skill (Metadata, Purpose, Scope, When to Use, When Not to Use, Prerequisites, Required Context, Core Instructions, Step-by-Step Workflow, Quality Standards, Validation, Common Mistakes, Restrictions, Expected Deliverables, Documentation Requirements).

### 3. Decision Outcome
**Selected Option**: **Option B: Canonical 15-Section Schema**  
All 15 canonical skills in `skills/` and future custom skills must implement all 15 sections.

### 4. Consequences & Trade-offs
- **Positive Impacts**:
  - Predictable navigation: An agent can jump directly to Section 9 (Workflow) or Section 12 (Mistakes) with high semantic precision.
  - Prevents omission of critical constraints or validation rubrics.
- **Negative Impacts / Known Trade-offs**:
  - Slightly higher initial authoring overhead. Managed by providing [`templates/SKILL.template.md`](./templates/SKILL.template.md).

---

## ADR-005: Maximum Two-Skill Loading Protocol for Context Conservation

- **Date**: 2026-11-03
- **Status**: Accepted
- **Deciders**: Principal Software Architect & AI Agent Systems Architect
- **Supersedes**: None

### 1. Context & Problem Statement
Loading all 15 domain skills into an agent's context window consumes 30,000+ tokens, diluting attention and causing hallucination or rule confusion.

### 2. Alternatives Considered
1. **Option A: Monolithic Context Injection**: Load all skills at session startup.
2. **Option B: Selective Two-Skill Maximum Protocol**: Agents consult [`SKILLS.md`](./SKILLS.md) and load at most one primary skill and one complementary skill matching the immediate task.

### 3. Decision Outcome
**Selected Option**: **Option B: Selective Two-Skill Maximum Protocol**  
Agents must load only relevant skills and unload them when lifecycle phases advance.

### 4. Consequences & Trade-offs
- **Positive Impacts**:
  - Maximum context window retained for actual code analysis and editing.
  - Eliminates conflicting workflows between unrelated domain playbooks.
- **Negative Impacts / Known Trade-offs**:
  - Agent must perform one discovery read of `SKILLS.md` at task startup.

---

## ADR-006: Tripartite Separation of Reality, Memory, and Decisions

- **Date**: 2026-11-03
- **Status**: Accepted
- **Deciders**: Principal Software Architect & AI Agent Systems Architect
- **Supersedes**: None

### 1. Context & Problem Statement
Merging current code state, historical lessons, and architectural decisions into a single documentation file results in unwieldy documents where transient realities obscure permanent architectural law.

### 2. Alternatives Considered
1. **Option A: Monolithic Architecture Document**: Keep state, lessons, and decisions in one file.
2. **Option B: Tripartite Separation**:
   - `CONTEXT.md`: Current verified state of the codebase (mutable snapshot).
   - `MEMORY.md`: Long-term technical lessons, pitfalls, and conventions (accumulating knowledge).
   - `DECISIONS.md`: Immutable Architectural Decision Records with context and consequences (historical law).

### 3. Decision Outcome
**Selected Option**: **Option B: Tripartite Separation**  
Separates project reality, organizational memory, and architectural history into dedicated files.

### 4. Consequences & Trade-offs
- **Positive Impacts**:
  - Clear file responsibilities: Updating current dependencies in `CONTEXT.md` never risks deleting historical ADRs in `DECISIONS.md`.
  - Agents can selectively read only the specific dimension of context required for their task.
- **Negative Impacts / Known Trade-offs**:
  - Requires agents to update two files when a decision changes both architecture and memory.

---

## ADR-007: Three-Tier Skills Architecture & UI/UX Pro Max Engine Integration

- **Date**: 2026-11-03
- **Status**: Accepted
- **Deciders**: Principal Software Architect & AI Agent Systems Architect
- **Supersedes**: None

### 1. Context & Problem Statement
Following the completion of the 15 canonical foundational skills in Phase 3, real-world development workflows required specialized domain depth across diverse languages, runtimes, cloud platforms, agentic AI architectures, and deep UI design heuristics. Upstream repositories [`ui-ux-pro-max-skill/`](./ui-ux-pro-max-skill/) (UI/UX Pro Max system) and [`ECC/`](./ECC/) (314 domain skills) provided comprehensive intelligence. The challenge was integrating these capabilities into UMSF while strictly preserving the zero-dependency, local-first, CommonMark-only invariants without causing namespace collisions or context window bloat.

### 2. Alternatives Considered
1. **Option A: External Pointers Only**: Leave skills in `ECC/` and `ui-ux-pro-max-skill/` and require agents to traverse external paths.
2. **Option B: Unchecked Monolithic Import**: Copy all skills indiscriminately, overwriting foundational skills and dumping 330+ directories without taxonomy or registry.
3. **Option C: Three-Tier Hierarchical Integration**:
   - **Tier 1 (Canonical Lifecycle)**: Preserve our 15 foundational UMSF skills authored in the full 15-section schema.
   - **Tier 2 (UI/UX Pro Max Engine)**: Integrate the 7-skill UI/UX suite (`ui-ux-pro-max`, `banner-design`, `brand`, `design`, `design-system`, `slides`, `ui-styling`), copying the BM25 search CLI (`scripts/search.py`), 20+ CSV/JSON design datasets (`data/`), and 24 platform configurations (`templates/`). Harmonize `design-system` by merging ECC's 10-dimension audit and visual consistency scoring into the token specification engine.
   - **Tier 3 (Specialized Domain Skills)**: Integrate 313 modular domain skills from ECC, categorized into 8 functional disciplines.
   - Enforce the **Selective Two-Skill Maximum Protocol** and document the local Python CLI search engine.

### 3. Decision Outcome
**Selected Option**: **Option C: Three-Tier Hierarchical Integration**  
Successfully expanded the skill library to 335 total skills without external runtime dependencies (Python standard library only).

### 4. Consequences & Trade-offs
- **Positive Impacts**:
  - 100% local-first and zero-dependency: The BM25 search CLI executes with standard Python 3.
  - Zero namespace collisions: Canonical foundational skills maintained their 15-section schema while ECC's specialized skills provide deep coverage across 8 disciplines.
  - Comprehensive design intelligence: Agents can instantly query 79 visual styles, 192 product palettes, and 119 UX guidelines via `python3 skills/ui-ux-pro-max/scripts/search.py`.
  - Strict context preservation: The 2-skill maximum rule prevents context window dilution.
- **Negative Impacts / Known Trade-offs**:
  - Skill directory contains 335 subdirectories, necessitating structured discovery via `SKILLS.md` and CLI search commands rather than raw directory scans.

---

## ADR-008: Comprehensive Testing, Test-Driven Development (TDD), and AI Security Engineering Architecture

- **Date**: 2026-11-03
- **Status**: Accepted
- **Deciders**: Principal Software Architect, Senior QA Engineer, Security Architect, AI Agent Systems Architect
- **Supersedes**: None

### 1. Context & Problem Statement
Software engineering performed by autonomous AI agents frequently suffers from developer self-confirmation bias (agents authoring tests after code to match existing implementation), superficial security verification, lack of independent adversarial review, and premature release claims. UMSF required integrating a comprehensive testing lifecycle, strict Test-Driven Development (TDD: Red-Green-Refactor), independent QA and Security verification roles, authorized penetration testing guardrails, a 10-stage vulnerability lifecycle, and 16 standardized engineering domains with 35 new advanced skills—all while strictly maintaining zero external runtime dependencies and local-first Markdown architecture.

### 2. Alternatives Considered
1. **Option A: Monolithic Unseparated Agent Execution**: Single agent writes code, writes tests after the fact, and declares its own work approved. Rejected due to severe confirmation bias and security blind spots.
2. **Option B: Heavyweight External SaaS Integration**: Requiring cloud-based security scanners, external CI daemons, and proprietary frameworks. Rejected because it violates UMSF's local-first, zero-dependency, and provider-independent invariants.
3. **Option C: Tripartite Logical Agent Architecture with Single-Agent Fallback, 16 Numbered Domains, and 4-Tier Release Gates**:
   - **Tripartite Roles**: Agent A (Development / TDD), Agent B (Independent QA), Agent C (Independent Security).
   - **Mode 1 & Mode 2 Execution**: Concurrent subagents in multi-agent harnesses; sequential role-switching passes with fresh checklists in single-agent harnesses.
   - **16 Numbered Engineering Domains**: Structuring all skills under numbered domain directories (`skills/01-...` through `skills/16-...`).
   - **Four-Tier Release Gates**: Functional, Regression, Security, and Documentation gates backed by inspectable empirical evidence.
   - **Strict Penetration Testing Guardrails**: Explicit authorization boundaries, non-destructive PoCs, zero sensitive data exfiltration, zero uncontrolled DoS.

### 3. Decision Outcome
**Selected Option**: **Option C: Tripartite Logical Agent Architecture with 16 Numbered Domains and Release Gates**  
Formally codified into [`RULES.md`](./RULES.md) (Level 2), [`WORKFLOW.md`](./WORKFLOW.md) (Level 5), [`AGENTS.md`](./AGENTS.md) (Level 7), and [`SKILLS.md`](./SKILLS.md) (Level 6).

### 4. Consequences & Trade-offs
- **Positive Impacts**:
  - Eliminates confirmation bias: Dev cannot approve its own work; independent QA and Security audits required.
  - TDD Red-Green-Refactor enforces behavioral invariance and catches regressions before code merges.
  - Explicit authorization boundaries prevent unauthorized or destructive security probing.
  - Zero-dependency invariant preserved: all test logging, threat models, and vulnerability registers are standard Markdown under the user's project `/docs_agent/` directory (initially empty).
  - 100% link resolution: numbered domain directories and root symlinks coexist with zero broken references.
- **Negative Impacts / Known Trade-offs**:
  - In single-agent environments, agents must spend extra turns executing explicit role-switch passes (Dev -> QA -> Security) rather than declaring instant completion. This overhead is a deliberate design trade-off for software correctness and security.

---

## ADR-009: Self-Contained Markdown Skills & Zero Search CLI Dependency

- **Date**: 2026-11-03
- **Status**: Accepted
- **Deciders**: Principal Software Architect & AI Agent Systems Architect
- **Supersedes**: ADR-007 (partially, replacing mandatory search CLI usage with self-contained Markdown catalogs)

### 1. Context & Problem Statement
When developers and AI coding agents adopt UMSF into real-world codebases, upstream source directories (`ECC/`, `ui-ux-pro-max-skill/`) are not available, and users will not install external toolchains or run interactive search CLIs (such as `search.py`). Previously, several skills assumed the presence of interactive search tools, Python scripts, or `${CLAUDE_PLUGIN_ROOT}`, causing execution failure when those external harnesses were absent. All skills in UMSF needed to be 100% self-contained in Markdown so that any user and any AI agent can directly use all 370 skills without installing external tools or running interactive search.

### 2. Alternatives Considered
1. **Option A: Require User Installation**: Mandate that users clone `ECC/` and `ui-ux-pro-max-skill/` or install Python/npm search CLI dependencies. Rejected because it violates UMSF's zero-dependency, local-first, zero-install architecture.
2. **Option B: Strip Out Design Intelligence**: Remove UI/UX Pro Max intelligence and rely only on generic instructions. Rejected because high-quality Swiss & Minimalism design tokens, 88 styles, 192 product palettes, and 119 UX guidelines are critical for elite UI engineering.
3. **Option C: Pure Markdown Catalog Compilation**:
   - Compile all 88 visual styles, 192 product palettes, 74 font pairings, 25 chart guides, and 119 UX guidelines into structured, self-contained Markdown reference files (`references/styles-and-palettes.md`, `references/quick-reference.md`, `references/pro-rules.md`).
   - Rewrite `skills/ui-ux-pro-max/SKILL.md`, `skills/ui-ux-design/SKILL.md`, `skills/design/SKILL.md`, and ECC skills to be 100% self-contained Markdown instructions.
   - Retain all 370 skills natively inside `skills/` with zero requirement for interactive search or external installations.

### 3. Decision Outcome
**Selected Option**: **Option C: Pure Markdown Catalog Compilation & Self-Contained Skills**  
All 370 skills operate purely as standard Markdown documentation. All design catalogs, rules, checklists, and technical patterns are directly readable and actionable by any AI coding agent without running scripts or installing external packages.

### 4. Consequences & Trade-offs
- **Positive Impacts**:
  - 100% usable out of the box: Any user copying `skills/` into any project can immediately use all 370 skills.
  - Zero execution failures: No broken calls to `${CLAUDE_PLUGIN_ROOT}` or interactive CLI search tools.
  - Full preservation of UI/UX Pro Max design intelligence: All 88 styles, 192 palettes, 74 font pairings, and 119 guidelines are directly browsable in Markdown.
  - Strict zero-dependency invariant preserved across the entire framework.
- **Negative Impacts / Known Trade-offs**:
  - Browsing palettes and styles requires reading Markdown tables rather than executing automated BM25 ranking via terminal CLI. However, LLMs naturally excel at scanning structured Markdown tables and selecting optimal matches.

---

## ADR-010: Strict Relative Paths and Repository Portability Invariant

- **Date**: 2026-11-03
- **Status**: Accepted
- **Deciders**: Principal Software Architect & AI Agent Systems Architect
- **Supersedes**: None

### 1. Context & Problem Statement
During framework authoring, absolute paths containing specific host environments (e.g. `file:///home/<user>/Projects/AgenticSkill/...`) inadvertently leaked into repository markdown documents, skills, and templates. When other users or agents clone, fork, or copy the repository to different paths or operating systems (e.g. `/home/user/`, `/Users/...`, `C:\...`), these hardcoded host paths break navigation, link resolution, and documentation integrity. All internal file references, cross-skill links, and asset paths must be strictly relative to ensure 100% portability.

### 2. Alternatives Considered
1. **Option A: Absolute File URI Scheme (`file:///...`)**: Format links using absolute machine paths. Rejected because it breaks cross-user and cross-machine portability.
2. **Option B: Root-Absolute Web Scheme (`/skills/...`)**: Use leading slashes assuming a static web server root. Rejected because offline Markdown previewers, IDEs, and local agent file tools fail to resolve local files from system root `/`.
3. **Option C: POSIX Strict Relative Paths (`./...`, `../...`)**: Compute exact relative paths from the referencing file's directory to the target file.

### 3. Decision Outcome
**Selected Option**: **Option C: POSIX Strict Relative Paths**  
- All 1,150+ internal links across all 82 files converted to exact relative POSIX paths (e.g. `./TASKS.md` at root, `./references/quick-reference.md` in skills, `../../RULES.md` from nested skills).
- Host system paths (`/home/...`, `file:///...`) are strictly prohibited in tracked repository files.
- Codified as Invariant 6 in [`RULES.md`](./RULES.md) and added to the Section 14 Anti-Pattern Blacklist.

### 4. Consequences & Trade-offs
- **Positive Impacts**:
  - 100% repository portability: The repository and all its skills work identically regardless of clone location, username, or operating system.
  - Zero broken links in local IDEs, GitHub, and agent harnesses.
  - Full adherence to zero-dependency, local-first UMSF principles.
- **Negative Impacts / Known Trade-offs**:
  - Deeply nested skills require multiple `../` steps to reference root governance documents (e.g. `../../../RULES.md`), requiring rigorous link integrity verification during skill authoring.

---

## ADR-011: Post-Task Verification Gate, Dynamic Context-Aware Skill Loading & Risk-Proportionate Delivery

- **Date**: 2026-11-03
- **Status**: Accepted
- **Deciders**: Principal Software Architect, Senior QA Engineer, AI Systems Architect
- **Supersedes**: ADR-005 (replaces the arbitrary fixed two-skill maximum with dynamic context-aware skill loading)

### 1. Context & Problem Statement
A comprehensive framework audit identified three architectural contradictions across `AGENTS.md`, `RULES.md`, `SKILLS.md`, and `WORKFLOW.md`:
1. **Arbitrary Two-Skill Maximum (ADR-005)**: The fixed two-skill limit restricted complex tasks that naturally span multiple domains (e.g. architecture + TDD + UI + API) even when the context window had ample headroom.
2. **Release Gate Applicability & Risk Disproportionality**: Blanket requirements for adversarial security penetration tests and full regression sweeps created unnecessary overhead for low-risk changes (e.g. documentation typos, comments, standalone CSS tweaks).
3. **Premature Task Closure & Confirmation Bias**: Autonomous agents frequently marked tasks `Completed` without verifying line-level git diffs, checking all original acceptance criteria, or revalidating remediated issues.

### 2. Alternatives Considered
1. **Option A: Retain Fixed Limits & Blanket Gates**: Keep rigid 2-skill limit and mandate full penetration tests for all changes. Rejected because it impairs productivity on low-risk edits while throttling complex multi-domain workflows.
2. **Option B: Relax All Gates**: Remove release gates and rely on user manual inspection. Rejected because it destroys UMSF's core quality and security guarantees.
3. **Option C: Unified 12-Stage Lifecycle, Post-Task Verification Skill & Risk-Proportionate Gating**:
   - Author [`post-task-verification`](./skills/12-code-quality-and-maintenance/post-task-verification/SKILL.md) covering diff sweeps, acceptance criteria checks, quality/security audits, and revalidation loops.
   - Upgrade `WORKFLOW.md` to the 12-stage Canonical Engineering Lifecycle.
   - Replace the fixed 2-skill limit with dynamic context-aware loading guided by token economy.
   - Scope release gates proportionally to risk (Low, Medium, High).
   - Enforce the Evidence-Based Task Completion Invariant: never mark a task `Completed` without empirical evidence; report unresolved blockers honestly as `In Progress` or `Blocked`.

### 3. Decision Outcome
**Selected Option**: **Option C: Unified 12-Stage Lifecycle, Post-Task Verification Skill & Risk-Proportionate Gating**  
- Codified into [`RULES.md`](./RULES.md), [`WORKFLOW.md`](./WORKFLOW.md), [`AGENTS.md`](./AGENTS.md), and [`SKILLS.md`](./SKILLS.md).
- Authored canonical 15-section skill `skills/12-code-quality-and-maintenance/post-task-verification/SKILL.md` (371 skills total).

### 4. Consequences & Trade-offs
- **Positive Impacts**:
  - Eliminates premature completion: Tasks require line-level diff reviews and verified acceptance criteria.
  - Risk-proportionate efficiency: Low-risk documentation or styling changes are not bottlenecked by irrelevant penetration tests.
  - Workflow flexibility: Agents load necessary domain skills dynamically without arbitrary two-skill constraints while respecting context budgets.
  - Transparent reporting: Unresolved issues are reported honestly without false success claims.
- **Negative Impacts / Known Trade-offs**:
  - Requires agents to perform disciplined diff inspections and evidence gathering before closing tasks, adding conversational diligence for reliability.

---

## ADR-012: Independent Verification Subagent Architecture & Structured Tripartite Delegation Protocol

- **Date**: 2026-11-03
- **Status**: Accepted
- **Deciders**: Principal Software Architect, Senior QA Engineer, AI Systems Architect
- **Supersedes**: None (extends and operationalizes ADR-008 and ADR-011)

### 1. Context & Problem Statement
While ADR-011 established the post-task verification methodology and 12-stage engineering lifecycle, development agents still suffered from inherent confirmation bias when operating without explicit subagent role delegation. Specific failure modes included:
1. **Developer Self-Approval**: Primary development agents (Agent A) naturally tended to validate only their own expected code paths, overlooking missing prompt requirements, boundary failures, or uninspected side effects.
2. **Unverified Test Claims**: Development agents frequently claimed tests passed without running them, or relied on tests that merely mirrored already-written implementations.
3. **Unbounded Ping-Pong Loops**: Without a defined remediation lifecycle and strict iteration limits, agents entered endless minor refactoring loops.
4. **Attribution Ambiguity**: In single-agent environments, agents sometimes simulated or falsely claimed independent subagent redundancy when actually running sequential self-evaluations.

### 2. Alternatives Considered
1. **Option A: Retain Developer Self-Verification**: Let Agent A self-verify using post-task verification checklists. Rejected because cognitive confirmation bias cannot be reliably eliminated within the same implementation context.
2. **Option B: External Compiler / CI Gating Only**: Rely entirely on automated external build pipelines. Rejected because UMSF is a zero-dependency, local-first framework that must give agents sovereign, self-contained auditing capabilities inside the local IDE or CLI workspace.
3. **Option C: Independent Verification Subagent Architecture & Tripartite Delegation Protocol**:
   - Establish Agent B as a formal **Independent Verification Subagent** dispatched in an isolated subagent context (or fresh sequential pass).
   - Standardize an explicit 7-dimensional audit: Requirements, Diff Sweep, Architecture, Code Quality, Independent Test Execution, Security Coordination, and Documentation.
   - Standardize an 11-field defect schema across 7 severity tiers.
   - Bound remediation cycles to `MAX_VERIFICATION_ITERATIONS = 3` to prevent infinite loops.
   - Mandate honest attribution: in single-agent environments, explicitly record that verification was sequential self-review, never claiming fake independent subagents.
   - Enforce tri-state acceptance verdicts (`VERIFIED`, `NEEDS REMEDIATION`, `BLOCKED / NOT VERIFIED`), codifying that compilation alone is never sufficient.

### 3. Decision Outcome
**Selected Option**: **Option C: Independent Verification Subagent Architecture & Tripartite Delegation Protocol**
- Authored canonical 15-section domain skill [`skills/16-ai-agent-engineering/independent-verification-subagent/SKILL.md`](./skills/16-ai-agent-engineering/independent-verification-subagent/SKILL.md) and dual-path root symlink `skills/independent-verification-subagent` (advancing total physical skills to 372).
- Formalized Agent A (Primary Development Agent), Agent B (Independent Verification Subagent), and Agent C (Independent Security Agent) in [`AGENTS.md`](./AGENTS.md) Section 2 and [`RULES.md`](./RULES.md) Section 8.
- Upgraded Stages 7 through 12 in [`WORKFLOW.md`](./WORKFLOW.md) to govern subagent handoffs, finding classification, bounded remediation, and tri-state acceptance decisions.

### 4. Consequences & Trade-offs
- **Positive Impacts**:
  - Complete cognitive independence: Agent B inspects raw prompts and actual diffs with zero deference to Agent A's claims.
  - Elimination of false claims: Tests must be executed directly with raw exit codes inspected.
  - Finite execution guarantees: Max 3 remediation iterations prevent infinite loops; unresolved blockers are reported honestly.
  - Transparent attribution: Clear distinction between real multi-agent execution (Mode 1) and sequential fallback (Mode 2).
  - 100% zero-dependency, local-first Markdown architecture preserved.
- **Negative Impacts / Known Trade-offs**:
  - Dispatching an isolated subagent or running a sequential verification pass consumes additional agent turns and tokens, which is an intentional, high-value investment in reliability.






