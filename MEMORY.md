# Persistent Memory & Knowledge Base
# Universal Markdown Skills Framework (UMSF)

> Long-Term Technical Discoveries, Pitfalls, Invariants, and Architectural Lessons  
> Status: Active Knowledge Base  
> Authority: Persistent Knowledge System  

---

## 1. Operating Conventions & Framework Invariants

### 1.1 The Markdown-Only Constraint
- **Core Lesson**: Introducing Python scripts, Node packages, or shell daemons into the framework governance layer creates fragile environment dependencies and breaks portability across different coding agents.
- **Convention**: All framework logic, instruction discovery, and session handoffs must be expressed purely through structured Markdown files (`.md`).
- **Discovery**: AI coding agents naturally follow structured YAML frontmatter, Markdown tables, and Mermaid flowcharts when presented clearly at standard entry points (`AGENTS.md`).

### 1.2 Multi-Agent Precedence Discipline
- **Core Lesson**: When multiple instructions apply, coding agents can suffer from "instruction conflict paralysis" unless an unambiguous tie-breaking hierarchy exists.
- **Convention**: The 7-tier precedence hierarchy in `AGENTS.md` and `RULES.md` is absolute. Explicit user prompts always win unless they violate mandatory safety constraints in `RULES.md` (Level 2).

### 1.3 Context Economy (Dynamic Context-Aware Skill Loading)
- **Core Lesson**: Ingesting the entire `skills/` library into an agent's context window degrades reasoning performance, triggers hallucination, and wastes token budgets. Conversely, a rigid 2-skill limit restricts complex multi-disciplinary tasks.
- **Convention**: Agents must load all relevant domain skills required by a task dynamically, guided by active context window economy rather than an arbitrary fixed limit, unloading them once that stage concludes.

---

## 2. UI/UX Pro Max Architectural Lessons & Invariants

### 2.1 Swiss & Minimalism Design Persona
- **Lesson**: High-density developer and documentation tools benefit most from clean geometric typography, structured grid alignment, and functional whitespace. Decorative gradients and inconsistent border radii add visual fatigue.
- **Tokens**: Always bind UI components to semantic CSS variables (`--color-primary: #0F172A`, `--color-accent: #22C55E`, `--color-background: #020617`, `--color-card: #0E1223`, `--color-border: #334155`). Never write hardcoded hex values into components.

### 2.2 Accessibility Invariants (WCAG AA Compliance)
- **Contrast**: Body text contrast must never drop below **4.5:1** against rendered backgrounds. Low-contrast gray-on-gray text is strictly rejected.
- **Touch Targets**: Minimum **44×44px** hit area with at least **8px** gap spacing. Small icon buttons without padding fail on mobile and touch devices.
- **Focus Rings**: Never remove focus rings (`outline: none` without replacement is a critical accessibility failure). Always supply `--color-ring` (`#38BDF8`).
- **Iconography**: Never use raw emojis as UI icons (e.g. 🔍, ⚙️, ❌). Raw emojis render inconsistently across operating systems and lack accessibility labels. Use accessible SVGs (Lucide / Heroicons) with `aria-hidden="true"`.

### 2.3 Mobile-First Breakpoints
- **Standard Scale**: Mobile `375px` -> Tablet `768px` -> Desktop `1024px` -> Wide `1440px`.
- **Pitfall**: Designing desktop-first almost always results in accidental horizontal scrollbars on mobile viewports. Layouts must be built mobile-first.

### 2.4 Self-Contained Markdown Intelligence (No Interactive Search CLI Reliance)
- **Core Lesson**: Assuming the user has upstream repositories (`ECC/`, `ui-ux-pro-max-skill/`) or external plugins installed breaks when users adopt UMSF into their own projects. Users cannot and will not use interactive search tools.
- **Convention**: All 370 skills must be 100% self-contained Markdown skills. All design styles, product palettes, font pairings, UX guidelines, and checklists must reside directly in Markdown files (`references/styles-and-palettes.md`, `references/quick-reference.md`, `references/pro-rules.md`). Any AI coding agent can read and use them directly without executing Python scripts or external tools.

---

## 3. Known Technical Pitfalls & Workarounds

| Component / Subsystem | Known Pitfall | Root Cause | Verified Remediation / Workaround |
|---|---|---|---|
| **Agent Discovery** | Agent misses instructions in subfolders | Agents often read only workspace root files | Maintain `AGENTS.md` at repository root as the single canonical entry point |
| **CSS Animations** | UI stutter and layout thrashing | Animating `width`, `height`, `margin`, or `top` | Animate exclusively GPU-composited properties: `transform` and `opacity` |
| **CSS Motion** | Nausea / disorientation for users with vestibular disorders | Unchecked infinite or aggressive motion | Always wrap keyframe animations in `@media (prefers-reduced-motion: no-preference)` |
| **Markdown Links** | Broken relative navigation | Inconsistent paths between nested docs and root | Always use absolute file links with the `file://` scheme or verified relative links |
| **Database ORM** | N+1 query performance collapse | Looping over parent records and querying children individually | Enforce eager loading with explicit joins or batching |
| **API Errors** | Ambiguous client failures | Returning HTTP 200 with `{ "error": true }` payload | Strictly use standard HTTP status codes (4xx/5xx) and RFC 7807 error schema |
| **Interactive Tool Assumption** | Agent attempts to run interactive search CLI that fails | Skills instructing agent to run `python3 search.py` or `${CLAUDE_PLUGIN_ROOT}` | Provide self-contained Markdown catalogs (`styles-and-palettes.md`, `quick-reference.md`) |
| **Large Skill Catalogs** | Context dilution & token exhaustion | Indiscriminately loading dozens of skills into context | Enforce Dynamic Context-Aware Skill Loading (ADR-011); use `SKILLS.md` categorized index |
| **Visual Inconsistency & AI Slop** | Generic low-contrast designs, purple gradients, bad spacing | Unconstrained generative styling without token systems | Consult `styles-and-palettes.md` and apply the 10-dimension visual audit in `design-system` |
| **TDD Confirmation Bias** | Authoring tests after code to match existing bugs | Developer testing only happy paths post-hoc | Enforce RED phase: write tests first and confirm failure before implementing code |
| **Destructive Security Probing** | Accidental data loss or service degradation during pen-tests | Using aggressive or unconstrained exploitation payloads | Mandate explicit authorization boundaries and non-destructive PoCs only |
| **Developer Self-Approval** | Overlooking vulnerabilities and missing prompt requirements in own code | Cognitive confirmation bias and assumptions of correctness | Enforce Independent Verification Subagent (Agent B) audit; prohibit Agent A self-approval |
| **Compilation-Only False Assurance** | Code compiles without error but crashes on input or fails logic | Assuming compilation equals verification | Enforce Compilation Inadequacy Invariant: automated test execution and exit code 0 mandatory |
| **Unbounded Agent Ping-Pong** | Agent A and B trapped in endless minor remediation loops | Absence of termination bounds on remediation cycles | Enforce `MAX_VERIFICATION_ITERATIONS = 3`; halt and report unresolved blockers honestly |
| **Attribution Simulation** | Falsely claiming subagent verification in single-agent CLI | Simulating multi-agent redundancy | Mandate explicit declaration that verification was sequential self-review |
| **Machine-Specific Path Leakage** | Links breaking across machines or users | Authoring absolute `file:///home/...` paths in repository files | Always use relative POSIX paths (`./TASKS.md`, `../../RULES.md`) in repository files |

---

## 4. Reusable Implementation Patterns

### Pattern 4.1: The Minimal Failing Reproduction First
- **Context**: Debugging any defect.
- **Pattern**:
  1. Author a unit test or scratch script demonstrating the failure.
  2. Run the test and verify that it fails (Red).
  3. Apply the targeted surgical fix to source code.
  4. Run the test and verify that it passes (Green).
  5. Permanently keep the test in the regression suite.
- **Rule**: If you cannot reproduce the bug, you do not understand the bug.

### Pattern 4.2: Atomic File Edits
- **Context**: AI agents editing large source files.
- **Pattern**: Perform targeted string replacements on contiguous blocks rather than rewriting entire 500-line files. Full-file rewrites often accidentally discard pre-existing comments, edge-case handlers, or license notices.

---

## 5. Chronological Historical Discoveries

- **2026-11-02**: Evaluated local `search.py` design intelligence tool in `ui-ux-pro-max-skill`. Verified that querying `--design-system` produces deterministic, production-grade Swiss & Minimalism color palettes, typography pairings (IBM Plex Sans + JetBrains Mono), and accessibility checklists.
- **2026-11-02**: Confirmed that establishing an explicit 7-tier precedence model in `AGENTS.md` prevents conflict loops between general agent tendencies and strict repository security rules.
- **2026-11-03**: Verified that enforcing a canonical 15-section schema across all 15 skills enables any compatible AI coding agent to quickly locate prerequisites, workflows, and anti-patterns without reading the entire file.
- **2026-11-03**: Successfully integrated 313 ECC specialized engineering skills and the 7-skill UI/UX Pro Max intelligence suite into `skills/` (335 skills total). Verified zero collisions with foundational skills, zero external runtime dependencies (Python standard library only for `search.py`), and 100% compliance with local-first CommonMark standards.
- **2026-11-03**: Formally codified ADR-008 and deployed the 16 Canonical Engineering Domains with 35 new advanced skills across Security Engineering, QA/TDD, and AI Agent Engineering (370 total skills). Established the Tripartite Logical Agent Architecture (Dev, QA, Security), Single-Agent Fallback, 4-Tier Release Gates, and isolated user `/docs_agent/` protocols.
- **2026-11-03**: Transitioned all 370 skills to 100% self-contained Markdown skills. Removed all mandatory requirements for interactive search CLI (`search.py`) and external plugin environments (`${CLAUDE_PLUGIN_ROOT}`). Compiled the complete design catalog (88 styles, 192 product palettes, 74 font pairings, 25 chart guides) into pure Markdown (`references/styles-and-palettes.md`). All skills are immediately usable by any user or AI coding agent without installing external tools.
- **2026-11-03**: Resolved machine-specific absolute path leakage (`file:///home/<user>/...`). Converted 1,150+ internal links across 82 files to strict relative POSIX links. Ratified ADR-010 and codified Invariant 6 in `RULES.md` to guarantee 100% repository portability across any user path or clone environment.
- **2026-11-03**: Conducted comprehensive framework audit and contradiction resolution. Authored `post-task-verification` skill, expanding library to 371 skills. Codified 12-stage Canonical Lifecycle with mandatory diff sweeps and requirement completeness analysis. Superseded ADR-005 with ADR-011, establishing Dynamic Context-Aware Skill Loading and Risk-Proportionate Release Gates.
- **2026-11-03**: Implemented the Independent Verification Subagent Architecture. Authored canonical 15-section skill `skills/16-ai-agent-engineering/independent-verification-subagent/SKILL.md` (372 skills total). Ratified ADR-012. Codified the 7-dimensional independent audit protocol (Requirements, Complete Diff Sweep, Architecture, Code Quality, Independent Test Execution, Security Coordination with Agent C, and Documentation Audit), standardized the 11-field defect schema, bounded remediation loops to `MAX_VERIFICATION_ITERATIONS = 3`, established the Compilation Inadequacy Invariant, and codified tri-state acceptance verdicts (`VERIFIED`, `NEEDS REMEDIATION`, `BLOCKED / NOT VERIFIED`) with mandatory honest attribution in single-agent fallback modes.

