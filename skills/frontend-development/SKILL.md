---
name: frontend-development
description: Standards and actionable workflows for building accessible, responsive, high-performance UI components and client state architectures.
version: 1.0.0
category: development
tags: [frontend, ui, components, responsive, accessibility, state, ui-ux-pro-max]
---

# Skill: Frontend Development & UI Engineering

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema and incorporating UI/UX Pro Max intelligence.

---

## 1. Metadata
- **Identifier**: `frontend-development`
- **Category**: Engineering & UI
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
This skill governs client-side user interface engineering, component hierarchy design, reactive state management, responsive layout implementation, and accessibility enforcement. It directly operationalizes the design intelligence from the **UI/UX Pro Max** framework.

---

## 3. Scope
- **In-Scope**:
  - Authoring accessible, responsive frontend components (React, Vue, Svelte, Angular, Vanilla HTML/CSS).
  - Implementing semantic CSS design tokens and Swiss/Minimalist aesthetic standards.
  - Client-side routing, optimistic UI updates, and error boundary management.
  - Enforcing WCAG AA compliance (4.5:1 contrast, keyboard navigation, focus management).
- **Out-of-Scope**:
  - High-level design system token discovery and palette reasoning (delegate to [`skills/ui-ux-design/SKILL.md`](../ui-ux-design/SKILL.md)).
  - Server-side business logic and database persistence (delegate to [`skills/backend-development/SKILL.md`](../backend-development/SKILL.md)).

---

## 4. When to Use
- When creating, refactoring, or testing web pages, client views, or UI components.
- When resolving responsive layout bugs, overflow issues, or keyboard accessibility gaps.
- When binding frontend views to backend API endpoints.

---

## 5. When Not to Use
- For pure backend logic, database migrations, or non-visual CLI tooling.

---

## 6. Prerequisites
- UI/UX design tokens and layout structure identified or referenced from [`skills/ui-ux-design/SKILL.md`](../ui-ux-design/SKILL.md).
- Frontend stack identified from repository files (e.g. Next.js, React, Tailwind, Vue).

---

## 7. Required Context
- Mandatory constraints in [`RULES.md`](../../RULES.md) (UI/UX Pro Max Invariants).
- System architecture in [`docs_agent/ARCHITECTURE.md`](../../docs_agent/ARCHITECTURE.md).
- Design intelligence system in [`skills/ui-ux-pro-max/SKILL.md`](../ui-ux-pro-max/SKILL.md) and catalogs in [`skills/ui-ux-pro-max/references/styles-and-palettes.md`](../ui-ux-pro-max/references/styles-and-palettes.md).
- Token architecture and component specifications in [`skills/design-system/SKILL.md`](../design-system/SKILL.md).
- Advanced canvas and visual styling in [`skills/ui-styling/SKILL.md`](../ui-styling/SKILL.md).

---

## 8. Core Instructions

### 8.1 UI/UX Pro Max Engineering Rules
1. **Semantic Token Invariant**:
   - Never write raw hex codes (`#0f172a`, `#22c55e`) inside component styles.
   - Always bind styles to semantic CSS tokens:
     ```css
     background-color: var(--color-background);
     color: var(--color-foreground);
     border-color: var(--color-border);
     ```
2. **Accessibility (WCAG AA 4.5:1 Minimum)**:
   - Verify that text foreground achieves at least **4.5:1** contrast against its rendered background container.
   - Every interactive element (buttons, links, inputs) must display a visible focus ring (`--color-ring`) when navigated via keyboard.
   - Every icon button without text must specify an explicit `aria-label`.
   - Never use raw emojis as UI icons. Use accessible SVGs (e.g., Lucide, Heroicons) with `aria-hidden="true"`.
3. **Touch Targets & Spacing**:
   - Interactive targets must measure at least **44×44px** in hit area.
   - Maintain at least **8px** gap between adjacent interactive targets.
4. **Mobile-First Responsive Breakpoints**:
   - Layouts must be built mobile-first across:
     - Mobile: `375px` (Single column, no horizontal scroll)
     - Tablet: `768px` (2 columns or responsive drawer)
     - Desktop: `1024px` (Persistent navigation, multi-column grid)
     - Wide: `1440px` (Max container width capped with auto-margins)
5. **Animation & Motion**:
   - Keep transition durations between **150ms and 250ms**.
   - Animate only `transform` and `opacity`. Never animate `width`, `height`, or `margin`.
   - Always honor `@media (prefers-reduced-motion: reduce)`.

---

## 9. Step-by-Step Workflow
1. **Step 1: Inspect Design Tokens & Context**
   - Check available CSS variables in the project or load from [`skills/ui-ux-design/SKILL.md`](../ui-ux-design/SKILL.md).
2. **Step 2: Component Architecture & Scaffolding**
   - Decompose view into atomic components: Header, Navigation, Content Card, Footer.
   - Scaffolding semantic HTML tags (`<main>`, `<nav>`, `<header>`, `<section>`, `<button>`).
3. **Step 3: Responsive Layout Styling**
   - Implement mobile-first CSS grid or flexbox layout.
   - Verify layout integrity at 375px, 768px, 1024px, 1440px.
4. **Step 4: Interactive States & Accessibility Wiring**
   - Implement `:hover`, `:focus-visible`, `:active`, and disabled states.
   - Add loading indicators and error banners.
5. **Step 5: Pre-Delivery Checklist Verification**
   - [ ] No emojis as icons (SVG only).
   - [ ] `cursor: pointer` on all clickable elements.
   - [ ] Minimum 44×44px touch targets.
   - [ ] Contrast ratio ≥ 4.5:1.
   - [ ] Zero horizontal scrollbars at 375px.
   - [ ] `prefers-reduced-motion` respected.

---

## 10. Quality Standards
- **Zero Console Errors**: No unhandled promise rejections, hydration mismatches, or missing key warnings.
- **Accessibility**: 100% pass on automated a11y audits (axe / Lighthouse Accessibility ≥ 95).
- **Responsive Fluidity**: Zero horizontal overflow across all four breakpoints.

---

## 11. Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Contrast Verification | Color ratio check | ≥ 4.5:1 for body text; ≥ 3.0:1 for large text |
| Touch Target Audit | DOM element measurement | All interactive elements ≥ 44×44px |
| Responsive Check | Viewport resizing (375px - 1440px) | Zero horizontal overflow; clean reflow |
| Keyboard Navigation | Tab key inspection | Visible focus indicator on every interactive control |

---

## 12. Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Suppressing Outline (`outline: none`) | Breaks navigation for keyboard and screen-reader users | Provide visible `--color-ring` focus indicator |
| Raw Hex in Components | Makes theming and dark mode refactoring fragile | Reference semantic tokens (`var(--color-primary)`) |
| Animating `width`/`height` | Causes CPU layout thrashing and stutter | Animate `transform: scale()` or `opacity` |

---

## 13. Restrictions
- Do NOT use emojis as UI icons.
- Do NOT introduce un-scoped global styles that leak across components.
- Do NOT disable user viewport zooming (`user-scalable=no`).

---

## 14. Expected Deliverables
- Clean, modular frontend component files.
- Associated styles adhering to semantic tokens.
- Unit/component test files verifying rendering and interaction.

---

## 15. Documentation Requirements
- Record reusable UI component patterns in [`MEMORY.md`](../../MEMORY.md).
- Update task state in [`TASKS.md`](../../TASKS.md).

