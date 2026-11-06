# Independent Verification Audit Checklists & Triage Rubrics (Level 3 Reference)
# Universal Markdown Skills Framework (UMSF)

> Version: 1.7.0  
> Authority: Level 3 Optional Reference Asset for `independent-verification-subagent`  
> Domain: 16 — AI Agent Engineering  

---

## 1. Overview
Comprehensive 7-dimensional audit checklists, defect severity rubrics, and handoff verification templates used by Agent B (Independent Verification Subagent) during post-task verification passes. Load this reference only when conducting complex multi-file verification audits.

---

## 2. Seven-Dimensional Verification Checklist

### Dimension 1: Requirements Audit
- [ ] Every functional requirement in user prompt mapped to verified code.
- [ ] All specified edge cases, boundary values, and negative test paths verified.
- [ ] No unrequested features or unauthorized scope creep introduced.

### Dimension 2: Change Inventory & Diff Audit
- [ ] `git status -s` inspected; no unintended untracked files or leftover debug logs.
- [ ] `git diff` audited line-by-line; zero syntax regressions or commented-out debris.
- [ ] All imports verified; no circular dependencies or broken relative paths.

### Dimension 3: Architecture & Invariant Conformance
- [ ] Strict compliance with precedence hierarchy in `AGENTS.md` and `RULES.md`.
- [ ] Architectural decisions in `DECISIONS.md` respected and upheld.
- [ ] Modularity preserved; layer boundaries cleanly maintained.

### Dimension 4: Code Quality & Maintenance
- [ ] Clean, self-documenting code; no magic literals or undocumented hacky workarounds.
- [ ] Existing comments and docstrings preserved unless intentionally modified.
- [ ] Error handling explicit; exceptions caught and handled gracefully.

### Dimension 5: Independent Test Execution
- [ ] Test runner executed independently by Agent B (never trusting Agent A logs).
- [ ] Command exit code inspected (`0` vs non-zero).
- [ ] Raw test output audited for actual assertions, not skipped or dummy suites.

### Dimension 6: Security & Threat Review
- [ ] Zero secrets, tokens, or private keys committed in plaintext.
- [ ] Input validation and parameter sanitization verified.
- [ ] Security boundaries in `RULES.md` Section 2 strictly intact.

### Dimension 7: Documentation Synchronisation
- [ ] `CONTEXT.md` updated with accurate current project reality.
- [ ] `TASKS.md` updated with empirical verification evidence before transitioning to Completed.
- [ ] `CHANGELOG.md` and `MEMORY.md` updated if meaningful lessons or milestones occurred.

