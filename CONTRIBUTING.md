# Contributing to the Universal Markdown Skills Framework (UMSF)

> Version: 1.0.0  
> Authority: Open Source Contribution Guidelines  

---

## 1. Principles & Welcome

Thank you for contributing to the **Universal Markdown Skills Framework (UMSF)**! UMSF is an open, provider-independent, zero-dependency, local-first framework designed to empower AI coding agents with structured memory, reusable domain skills, and session continuity.

Before submitting a pull request, please review these guidelines to ensure consistency, quality, and strict adherence to framework invariants.

---

## 2. Framework Invariants (Non-Negotiable)

Every contribution must honor the non-negotiable rules established in [`RULES.md`](./RULES.md) and [`DECISIONS.md`](./DECISIONS.md):

1. **Zero External Dependencies**:
   - The framework core is implemented strictly in Markdown (`.md`).
   - Do NOT introduce `package.json`, `requirements.txt`, compiled binaries, or background daemons.
2. **Local-First & Sovereign**:
   - All knowledge, skills, and memory reside locally inside the git repository. No cloud memory sync or proprietary API dependencies.
3. **Canonical 15-Section Schema**:
   - Any new or modified skill in `skills/` must strictly implement all 15 required sections in [`templates/SKILL.template.md`](./templates/SKILL.template.md).
4. **UI/UX Pro Max Invariants**:
   - All user interface components, tokens, and visual standards must conform to the Swiss & Minimalism aesthetic, WCAG AA 4.5:1 text contrast minimum, 44×44px minimum touch targets, mobile-first breakpoints (375px/768px/1024px/1440px), and SVG-only iconography (no raw emojis as icons).
5. **No Fabricated Information**:
   - Never commit speculative, unverified facts or non-existent file references.

---

## 3. How to Contribute a New Skill

To contribute a new reusable domain skill:
1. **Check Existing Registry**: Consult [`SKILLS.md`](./SKILLS.md) to confirm that the domain is not already covered by an existing skill.
2. **Create Skill Directory**: Create `skills/<skill-name>/`.
3. **Scaffold from Template**: Copy [`templates/SKILL.template.md`](./templates/SKILL.template.md) to `skills/<skill-name>/SKILL.md`.
4. **Complete All 15 Sections**:
   - 1. Metadata (YAML frontmatter: `name`, `description`, `version`, `category`, `tags`)
   - 2. Purpose
   - 3. Scope (In-Scope and Out-of-Scope boundaries)
   - 4. When to Use
   - 5. When Not to Use
   - 6. Prerequisites
   - 7. Required Context
   - 8. Core Instructions
   - 9. Step-by-Step Workflow
   - 10. Quality Standards
   - 11. Validation
   - 12. Common Mistakes
   - 13. Restrictions
   - 14. Expected Deliverables
   - 15. Documentation Requirements
5. **Register the Skill**: Add your new skill to [`SKILLS.md`](./SKILLS.md) and [`skills/README.md`](./skills/README.md).

---

## 4. Git Hygiene & Commit Standards

- **Conventional Commits**: Format commit messages according to the Conventional Commits specification:
  - `feat: add docker-deployment domain skill`
  - `fix: correct responsive breakpoint table in ui-ux-design`
  - `docs: update cross-agent compatibility notes in COMPATIBILITY.md`
  - `refactor: streamline step-by-step workflow in testing skill`
- **Atomic Commits**: Keep commits focused on a single change. Do not bundle unrelated refactoring with feature additions.
- **No Secrets**: Never commit `.env` files, API keys, or private tokens.

---

## 5. Pull Request Verification Checklist

Before submitting your PR, ensure:
- [ ] Post-task verification executed via [`post-task-verification`](./skills/12-code-quality-and-maintenance/post-task-verification/SKILL.md) before submitting.
- [ ] Every internal Markdown link is strictly relative (POSIX `./...`, `../...`) with zero hardcoded machine paths.
- [ ] All new skills contain complete YAML frontmatter and all 15 sections.
- [ ] No external dependencies or package manifests were introduced.
- [ ] Registered in [`SKILLS.md`](./SKILLS.md) and [`skills/README.md`](./skills/README.md).
- [ ] `CHANGELOG.md` has been updated with a description of your changes under `[Unreleased]`.
- [ ] All UI modifications comply with the **UI/UX Pro Max** standards in `RULES.md`.

