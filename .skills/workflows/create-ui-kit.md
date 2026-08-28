# Workflow — Create a UI Kit / Design System

For UI kits, design systems, SaaS UI systems, admin/dashboard UI kits, and any
complete component-and-pattern product. This is the largest workflow: the
deliverable is a coherent system, not a component list.

## 1. Product framing and differentiation

- What is the system, concretely, and what class of product does it serve?
  (Dashboard for logistics teams, high-density analytics for B2B SaaS, clinic
  records UI for healthcare admin, etc.)
- Who is the buyer (product teams, agencies, freelancers) and who is the end
  user?
- What real workflow does the system cover end to end?
- What is its reason to exist? If it is "Modern SaaS UI Kit", narrow it until
  it has a specific problem, audience, or point of view. A kit with a strong
  point of view beats a generic one on every commercial dimension.
- Decide scope: number of components, demo views/pages, depth of states and
  variants, animation level. Make decisions; do not ask the user for every one.

## 2. Design direction

Read `design/design-direction.md`. Produce the full direction before any code:

- Design concept and visual personality (choose deliberately from
  `design/design-diversity.md` — the audience and use case drive the choice).
- Typography strategy (`design/typography.md`).
- Color strategy, including semantic colors and contrast (`design/color.md`).
- Spacing and grid philosophy (`design/spacing.md`).
- Shape language, border strategy, elevation strategy.
- Component philosophy, interaction philosophy, motion philosophy
  (`design/motion.md`), responsive philosophy (`design/responsive.md`),
  accessibility philosophy (`design/accessibility.md`).

Every value must have a reason. No arbitrary values.

## 3. Design tokens (the system core)

Define and name tokens before components:

- Color: primary palette, neutrals, semantic (success/warning/error/info),
  surface/background layers.
- Typography: type scale, weights, line heights, letter spacing, font usage.
- Spacing scale, radii scale, border widths, elevation/shadows.
- Breakpoints and container widths.
- Motion durations and easings.

Name tokens semantically (what they are for), not cosmetically (their value).
Consistency here is what makes the kit feel like one product.

## 4. Component architecture

- Define component boundaries: which are primitives, which are composites.
- Define naming conventions and file structure up front.
- Define state conventions across all components (hover/active/focus/disabled,
  loading/error/empty) so they are consistent everywhere.
- **Technology:** React (Next.js or Vite + React). UI kits and dashboards
  benefit from component composition, state management, and modern patterns.
- Choose CSS approach deliberately (CSS modules, Tailwind, or vanilla CSS
  with tokens). No unnecessary dependencies.

## 5. Core components

Implement primitives first with full anatomy: buttons, inputs/fields, typography
elements, icons (if any), badges, tooltips, etc. States and edge cases per
`workflows/create-component.md`. Use realistic content, not placeholder text.

**Code Commenting Requirements:**
- Every function must have JSDoc comments explaining purpose, parameters, returns.
- Complex logic blocks must have inline comments explaining the "why".
- Public APIs must be documented with usage examples.
- Accessibility considerations must be noted in comments where relevant.

## 6. Composite components

Build composites on the primitives: navigation, tables, cards, modals, forms,
filters, pagination, dashboard widgets, etc. Ensure they compose and share
Build composites on the primitives: navigation, dashboard components, cards, slide-over drawers, modals, forms, filters, and charts.
- **Anti-Table Design**: Dashboard views must not default to raw flat tables. Create visual card-strips, Kanban pipelines, or split panels.
- **Data Visualizations**: Implement responsive SVG sparklines and interactive chart tooltips using shared tokens.
- **Frictionless CRUD**: Integrate sliding drawers and in-context details panels to avoid navigation redirections.
- **Dial Compliance**: Ensure components respect the active **`DESIGN_VARIANCE`**, **`MOTION_INTENSITY`**, and **`VISUAL_DENSITY`** parameters defined in the brief.

## 7. Demo views

Build demo views that prove the system coheres: the actual screens the kit targets (e.g. single-screen Operations Canvas, split-screen Analytics hub, Settings drawer). These are the product's storefront and the strongest signal of quality. Every demo view must also be responsive, viewport-constrained, and fully accessible.

**Dashboard demo views MUST include:**
- Metric cards WITH sparklines showing trend data
- At least one full chart (line, bar, or donut) with animated data
- Data that animates on load (numbers count up, bars grow, lines draw)
- Realistic demo data (not random numbers — meaningful trends and patterns)

## 8. Interactions and motion

Apply `design/motion.md`: motion for hierarchy, feedback, transitions,
orientation, state changes, progressive disclosure. No decorative idle
animation. Interactions must be keyboard- and touch-operable.

## 9. Responsive implementation

Apply `design/responsive.md` at the system level: navigation transformation,
density changes, table restructuring, reflow of forms and grids. Layouts should
fundamentally change on small screens, not merely shrink.

## 10. Accessibility

Apply `design/accessibility.md` system-wide: semantic HTML, keyboard flows,
focus visibility, labels, ARIA only when needed, AA contrast, reduced motion,
touch targets, logical heading hierarchy, form errors.

## 11. Documentation

Per `marketplace/documentation.md`: getting started, installation, token
reference, component reference (purpose/anatomy/states/variants/example/
customization/a11y), customization guide, demo/setup instructions.

## 12. QA and packaging

Run `quality/visual-audit.md`, `quality/ux-audit.md`, `quality/responsive-audit.md`,
`quality/accessibility-audit.md`, `quality/code-audit.md`. Fix findings. Then,
if the kit is for distribution, complete the **marketplace/** modules
(packaging, screenshots, compliance).

## Deliverables

- Complete design system: tokens, components, demo views.
- Documentation set.
- QA results with fixes applied.
- Marketplace package where requested.
