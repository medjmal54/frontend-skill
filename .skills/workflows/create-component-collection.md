# Workflow — Create a Component Collection

For a set of related components that share a system: a form system, a
navigation system, a data-visualization collection, an animation/interaction
collection, or any family of components that must work together as one product.

A collection is a *product*, not a pile of parts. Its value comes from
cohesion, coverage of real use cases, and a shared design system.

## 1. Product framing

Answer before designing anything:

- What is the collection, concretely, and what real task does it cover end to
  end? (Example: "a multi-step form system" not "some inputs"; "a chart
  collection for monitoring dashboards" not "three graphs".)
- Who is the buyer and who is the end user?
- What is the primary goal the collection is bought to accomplish?
- What makes this collection differentiated (depth, density, a specific
  workflow, a distinct visual language)?

If the framing is generic ("SaaS components"), narrow it to a real problem with
a real audience.

## 2. Design direction

Read `design/design-direction.md` and establish the design system first:
typography, color, spacing, grid, radii, borders, elevation, motion, responsive
and accessibility philosophy. Read the supporting **design/** modules. Every
component inherits from this system — the collection must feel like ONE product.

## 3. Inventory and scope

List the components in the collection and why each exists. For each component,
define the anatomy (states, variants, content variation, edge cases) per
`workflows/create-component.md` steps 3–4. Include coverage of the full task
flow, not just the happy path — collections get judged on how much of a real
workflow they solve.

Meaningful variation rule: variants must reflect different use cases, not
different colors. An "error state", a "compact variant", a "destructive action"
are legitimate variants; "blue version / green version" is not.

## 4. Shared architecture

- **Technology:** Plain HTML + CSS + JS. Component packs are framework-agnostic.
  Each component is a standalone file that can be dropped into any project.
  No React, no Vue, no build step required.
- One token set for the whole collection (no per-component magic values).
- Consistent naming across components.
- Consistent file structure and export conventions.
- Shared primitives reused by composites (e.g., one field primitive powering
  text, select, and textarea).
- Documented component boundaries: what is shared, what is owned by each
  component.

## 4b. Chart/Graph components (for dashboard collections)

If the collection targets dashboards or data-heavy UIs, it MUST include
data visualization components:

- **Sparkline** — inline trend line for metric cards (SVG path, animated)
- **Bar chart** — vertical or horizontal bars (SVG rects, animated grow)
- **Line chart** — trend over time (SVG path, animated draw)
- **Donut/Pie chart** — proportional data (SVG circles, animated fill)
- **Area chart** — filled line chart (SVG path, animated draw)

All charts must:
- Be SVG-based (no external charting library dependency)
- Animate on load (bars grow, lines draw, donuts fill)
- Be responsive (viewBox-based scaling)
- Use the shared token system for colors
- Include accessible labels and ARIA attributes

## 5. Implement core → composite

Implement the primitives first, then the composites built on them. Keep each
component's states and edge cases working with realistic content. Do not add
dependencies a simple implementation could avoid.

**Code Commenting Requirements:**
- Every function must have JSDoc comments explaining purpose, parameters, returns.
- Complex logic blocks must have inline comments explaining the "why".
- Public APIs must be documented with usage examples.
- Accessibility considerations must be noted in comments where relevant.

## 6. Interactions

For interactive components, apply `design/motion.md` and the interaction rules
in `design/design-direction.md`: behavior must be predictable, keyboard- and
touch-operable, with feedback for loading/error/empty states where relevant.

## 7. Responsive

Apply `design/responsive.md` at the collection level. Restructuring must be
coherent across components (e.g., forms reflow, tables restructure, navigation
transforms consistently).

## 8. Accessibility

Apply `design/accessibility.md` to every component, not just the showcase ones.
Consistent focus, labels, keyboard behavior, contrast, and reduced-motion
handling across the collection.

## 9. Demo surface

Build a demo view that shows the collection in realistic use — a working
composite example (a complete form flow, a dashboard fragment, a nav scenario)
plus a gallery of components and states. The demo is the product's storefront.

## 10. Documentation and QA

Write the collection documentation (overview, installation, shared
tokens/architecture, per-component reference — see
`marketplace/documentation.md`). Run `quality/code-audit.md`,
`quality/accessibility-audit.md`, `quality/visual-audit.md`, and
`quality/responsive-audit.md`. Fix findings.

## Deliverables

- The component collection with shared tokens and architecture.
- Working composite demo + component gallery.
- Documentation covering the collection and every component.
- Confirmation of passed audits.
