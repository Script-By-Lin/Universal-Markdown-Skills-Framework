---
name: ui-ux-design
description: UI/UX design intelligence, design system token authoring, Swiss & Minimalism visual standards, accessibility compliance, and interaction heuristics powered by UI/UX Pro Max.
version: 1.0.0
category: design
tags: [ui, ux, design-system, tokens, accessibility, typography, styling, ui-ux-pro-max]
---

# Skill: UI/UX Design Intelligence & Design Systems

> Canonical UMSF Domain Skill Specification adhering to the standard 15-section schema and incorporating UI/UX Pro Max intelligence.

---

## 1. Metadata
- **Identifier**: `ui-ux-design`
- **Category**: Design & User Experience
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework

---

## 2. Purpose
This skill provides deep UI/UX design intelligence for digital interfaces across web, mobile, and desktop environments. It governs visual aesthetic selection, semantic token systems, typography scales, accessibility compliance (WCAG AA), interaction timing, and responsive design patterns, operationalizing the local **UI/UX Pro Max** intelligence engine.

---

## 3. Scope
- **In-Scope**:
  - Establishing design systems, color tokens, and typography pairings.
  - Applying Swiss & Minimalism design aesthetic (clean whitespace, high contrast, geometric alignment).
  - Enforcing the 10 prioritized UX rule categories from UI/UX Pro Max.
  - Authoring page-specific and master design system specifications.
  - Reviewing interfaces for accessibility, touch target sizing, and responsive fluidity.
- **Out-of-Scope**:
  - Concrete component code implementation in frameworks (delegate to [`skills/frontend-development/SKILL.md`](../frontend-development/SKILL.md)).
  - Backend API design and server data flow (delegate to [`skills/backend-development/SKILL.md`](../backend-development/SKILL.md)).

---

## 4. When to Use
- Designing a new product page, application view, or design system from scratch.
- Establishing or refactoring color palettes, typography scales, or spacing systems.
- Conducting an accessibility audit (contrast, focus indicators, keyboard interaction).
- Tuning animations and micro-interactions for perceived performance and polish.

---

## 5. When Not to Use
- For non-visual backend logic, algorithms, databases, or infrastructure tasks that do not impact user perception or interaction.

---

## 6. Prerequisites
- Target audience, product persona, and platform identified.
- Existing repository styling conventions inspected.

---

## 7. Required Context
- Mandatory constraints in [`RULES.md`](../../RULES.md) (UI/UX Pro Max Invariants).
- Core UI architecture in [`docs_agent/ARCHITECTURE.md`](../../docs_agent/ARCHITECTURE.md) Section 5.

---

## 8. Core Instructions

### 8.1 Ten Prioritized Rule Categories
Follow priority 1 to 10 when resolving design decisions:

| Priority | Category | Impact | Key Requirement | Anti-Pattern to Avoid |
|---|---|---|---|---|
| **1** | **Accessibility** | CRITICAL | Contrast ≥ 4.5:1, visible focus rings, aria-labels | Removing outline without replacement; icon buttons without labels |
| **2** | **Touch & Interaction** | CRITICAL | Min 44×44px hit size, ≥ 8px spacing, active feedback | Hover-only reliance; 0ms instant state changes without feedback |
| **3** | **Performance** | HIGH | WebP/AVIF images, reserved aspect ratio (CLS &lt; 0.1) | Layout thrashing; un-sized images shifting layout |
| **4** | **Style Selection** | HIGH | Swiss & Minimalism: functional whitespace, SVG icons | Mixing flat and skeuomorphic styles; raw emojis as icons |
| **5** | **Layout & Responsive** | HIGH | Mobile-first (375px, 768px, 1024px, 1440px), no overflow | Horizontal scrollbars; fixed pixel container widths |
| **6** | **Typography & Color** | MEDIUM | Base 16px body, 1.5 line height, semantic tokens | Text &lt; 12px; gray-on-gray low contrast; raw hex in components |
| **7** | **Animation & Motion** | MEDIUM | 150-250ms duration, transform/opacity only, reduced-motion | Uniform duration everywhere; animating width/height |
| **8** | **Forms & Feedback** | MEDIUM | Visible labels, inline errors near field, progressive disclosure | Placeholder-only labels; errors displayed only at page top |
| **9** | **Navigation** | HIGH | Predictable back behavior, bottom nav ≤ 5 items | Overloaded navigation bars; broken browser history |
| **10** | **Charts & Data** | LOW | Distinct labels, accessible tooltips, color independence | Relying on color alone to convey metrics |

### 8.2 Canonical Swiss & Minimalism Color Tokens
```css
:root {
  --color-primary: #0F172A;        /* Slate 900 - Primary brand / headings */
  --color-on-primary: #FFFFFF;
  --color-secondary: #1E293B;      /* Slate 800 - Secondary surfaces */
  --color-on-secondary: #FFFFFF;
  --color-accent: #22C55E;         /* Emerald 500 - Action CTAs / highlights */
  --color-on-accent: #0F172A;
  --color-background: #020617;     /* Slate 950 - Deep dark canvas */
  --color-foreground: #F8FAFC;     /* Slate 50 - High-contrast text */
  --color-card: #0E1223;           /* Surface container */
  --color-card-fg: #F8FAFC;
  --color-muted: #1A1E2F;          /* Subdued background */
  --color-muted-fg: #94A3B8;       /* Slate 400 - Secondary text */
  --color-border: #334155;         /* Structural borders */
  --color-destructive: #EF4444;    /* Error red */
  --color-ring: #38BDF8;           /* Focus ring sky blue */
}
```

### 8.3 Typography Hierarchy
- **Body & Display**: **IBM Plex Sans** (Weights: 400 Regular, 500 Medium, 600 SemiBold)
- **Code & Numeric Tokens**: **JetBrains Mono** (Weights: 400 Regular, 500 Medium)
- Base sizing: Body 16px (`1rem`), line-height 1.5. Minimum caption size: 12px (`0.75rem`).

### 8.4 Self-Contained UI/UX Pro Max Design Intelligence System
This skill operates with **100% self-contained Markdown intelligence**, requiring zero interactive CLI tools or external package installations:
- **Design Reference Catalogs**:
  - [`skills/ui-ux-pro-max/references/styles-and-palettes.md`](../ui-ux-pro-max/references/styles-and-palettes.md) — 88 visual styles, 192 product palettes, 74 font pairings, and chart types.
  - [`skills/ui-ux-pro-max/references/quick-reference.md`](../ui-ux-pro-max/references/quick-reference.md) — All 10 priority rule categories and 119 UX guidelines.
  - [`skills/ui-ux-pro-max/references/pro-rules.md`](../ui-ux-pro-max/references/pro-rules.md) — Mobile/app polish rules and the canonical Pre-Delivery Checklist.

#### Companion UI Suite Skills
Coordinate with complementary skills in the design suite:
- [`skills/ui-ux-pro-max/SKILL.md`](../ui-ux-pro-max/SKILL.md) — Flagship design intelligence and dial tuning.
- [`skills/design-system/SKILL.md`](../design-system/SKILL.md) — 3-tier token architecture, component specs, and 10-dimension consistency audits.
- [`skills/ui-styling/SKILL.md`](../ui-styling/SKILL.md) — Canvas font rendering and advanced CSS layouts.
- [`skills/brand/SKILL.md`](../brand/SKILL.md) — Brand identity, voice, tone, and brand token specifications.
- [`skills/banner-design/SKILL.md`](../banner-design/SKILL.md) — Promotional banner and hero section layouts.
- [`skills/slides/SKILL.md`](../slides/SKILL.md) — Strategic presentations and pitch decks.

---

## 9. Step-by-Step Workflow
1. **Step 1: Consult UI/UX Pro Max Markdown Catalogs**
   - Read [`skills/ui-ux-pro-max/references/styles-and-palettes.md`](../ui-ux-pro-max/references/styles-and-palettes.md) to select the aesthetic style (e.g. *Minimalism & Swiss Style*, *Bento Grid*, *Dashboard*) and tailored product color palette.
   - Review UX rules in [`skills/ui-ux-pro-max/references/quick-reference.md`](../ui-ux-pro-max/references/quick-reference.md) for domain-specific interaction patterns.
2. **Step 2: Persona & Product Classification**
   - Classify product: SaaS, Developer Tool, Dashboard, E-Commerce, or Documentation.
   - Confirm aesthetic style: Minimalism & Swiss Style.
3. **Step 3: Design Token Definition**
   - Establish semantic CSS variable definitions for colors, typography, and spacing scale (`8px`, `16px`, `24px`, `32px`, `48px`, `64px`).
4. **Step 4: Component Layout Wireframing**
   - Map mobile-first wireframes across `375px`, `768px`, `1024px`, and `1440px`.
5. **Step 5: Interaction & Accessibility Review**
   - Verify touch targets measure at least 44×44px.
   - Verify contrast ratio exceeds 4.5:1.
   - Define focus ring states and hover micro-interactions (150–250ms).
6. **Step 6: Pre-Delivery Audit**
   - [ ] No raw emojis used as UI icons (use SVG only).
   - [ ] All clickable elements display `cursor: pointer`.
   - [ ] Contrast meets 4.5:1 on light and dark surfaces.
   - [ ] Visible focus rings on all interactive elements.
   - [ ] Mobile viewport renders zero horizontal scroll.
   - [ ] `@media (prefers-reduced-motion)` is supported.

---

## 10. Quality Standards
- **Aesthetic Cohesion**: Visual rhythm is consistent across all pages and components.
- **Accessibility Certification**: Strict WCAG AA compliance across text contrast and focus indicators.
- **Responsive Purity**: Flawless layout reflow without horizontal scrolling across 375px–1440px.

---

## 11. Validation
| Check | Verification Method | Expected Outcome |
|---|---|---|
| Contrast Ratio | Color analysis tool | ≥ 4.5:1 for standard text; ≥ 3.0:1 for large text |
| Touch Target Dimensions | Bounding box inspection | Every interactive target ≥ 44×44px |
| Focus Ring Visibility | Keyboard tab navigation | Visible `--color-ring` displayed on active element |
| Responsive Reflow | Viewport resize testing | Zero horizontal scrollbars at 375px mobile |

---

## 12. Common Mistakes
| Mistake / Anti-Pattern | Why It Fails | Correct Alternative |
|---|---|---|
| Using Emojis as UI Icons | Renders inconsistently across OSs and lacks proper screen-reader labels | Use vectorized SVGs (Lucide / Heroicons) with aria-labels |
| Gray-on-Gray Text | Fails WCAG AA contrast; unreadable in sunlight or on low-quality screens | Ensure foreground achieves 4.5:1 against background |
| Instant State Changes (0ms) | Feels abrupt and disjointed to the user | Add smooth 150-250ms CSS ease-out transitions |

---

## 13. Restrictions
- Do NOT use emojis as UI icons.
- Do NOT remove keyboard focus rings without providing an accessible alternative.
- Do NOT hardcode non-semantic raw hex values inside components.

---

## 14. Expected Deliverables
- Design system specification or CSS design token definitions.
- Responsive layout guidelines and component wireframes.
- UI/UX audit report against the Pre-Delivery Checklist.

---

## 15. Documentation Requirements
- Record design system decisions in [`DECISIONS.md`](../../DECISIONS.md).
- Update [`TASKS.md`](../../TASKS.md) with task completion.

