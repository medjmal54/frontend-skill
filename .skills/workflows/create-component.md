# Workflow — Create a Component

For a single, focused, reusable component (button, modal, dropdown, tooltip,
data table, form field, chart, navigation bar, etc.) built to commercial
quality. A component is not "some markup that renders" — it is a system with
states, variants, content tolerance, and documented behavior.

## 1. Frame the component

Answer in one or two lines before designing anything:

- What is this component, concretely, and what problem does it solve?
- Who uses it (developer? end user?) and in what context?
- What information or task is it responsible for?
- What would make this component worth buying instead of free alternatives?

If the requested component is too generic ("a card"), differentiate it: a
*Metric Card for Operations Dashboards*, a *Document Status Card for Legal
Workflows*, not "Card 1, Card 2, Card 3".

## 2. Establish design direction

Read `design/design-direction.md` plus whichever of `design/typography.md`,
`design/color.md`, `design/spacing.md`, `design/motion.md`,
`design/responsive.md`, `design/accessibility.md` apply. Select a visual
language deliberately (see `design/design-diversity.md`). The component must be
designed in the context of a system, even if only the component ships — tokens
and patterns must be reusable.

## 3. Define the component anatomy

For every component, enumerate before coding:

- **Default state** — the reference state, designed first.
- **Interactive states** — hover, active/focus, disabled. Decide *how each is
  communicated* (color alone is never sufficient; combine color with shape,
  weight, or motion).
- **Data states** — loading, error, empty, success (where the data allows).
- **Content variation** — long labels, short labels, numbers, empty strings,
  very long strings, many items, one item, zero items. It must remain usable,
  not merely "look good in a screenshot."
- **Edge cases** — overflow, truncation, wrapping, mixed content, unusual
  characters, extreme lengths.

## 4. Define the API or class contract

- Framework component: clean props, sensible defaults, no prop explosion.
  Every prop must have a reason to exist.
- Plain CSS/HTML: consistent, documented class structure (prefixed to avoid
  collisions), BEM-style naming or the project's convention.
- Expose the meaningful variants as options, never as copy-paste custom CSS.

## 5. Design tokens

Extract colors, spacing, radii, borders, shadows, and typography values into
named tokens rather than hardcoded magic numbers. Reuse them across states and
variants. See `design/color.md`, `design/spacing.md`, `design/typography.md`.

## 6. Implement

Write the component. Keep it dependency-free where a simple implementation
suffices — do not pull in a library to render a dropdown. Semantics first:
use the correct native element (`<button>`, `<dialog>`, `<select>` where
appropriate) before layering custom behavior.

**Code Commenting Requirements:**
- Every function must have a JSDoc comment explaining its purpose, parameters,
  and return value.
- Complex logic blocks must have inline comments explaining the "why".
- Public APIs must be documented with usage examples.
- Accessibility considerations must be noted in comments where relevant.
- Magic numbers must be explained with comments (or converted to tokens).

**Caching Note:**
If this is an iterative edit to an existing component, check the cache first.
Read `caching/scope-narrowing.md` to determine which audits can be skipped.

## 7. Accessibility pass

Apply `design/accessibility.md`:

- Semantic structure and logical heading/label hierarchy.
- Keyboard: the component is fully operable with the keyboard; focus is visible
  and moves predictably.
- ARIA only where native semantics are insufficient.
- Contrast passes AA at minimum.
- `prefers-reduced-motion` respected if any motion is used.
- Live regions or `aria-live` for dynamic content that matters.

## 8. Responsive pass

Apply `design/responsive.md`. Even a single component must be defined at the
sizes it will actually appear in: small screens, touch targets, and container
widths. Decide how it *restructures*, not just shrinks.

## 9. Document

Create the component reference entry (see `marketplace/documentation.md`):
purpose, anatomy, states, variants with names and use cases, code example,
customization surface, accessibility notes.

## 10. QA and sign-off

Run the applicable audits in **quality/**: at minimum `code-audit.md` and
`accessibility-audit.md`, plus `visual-audit.md` if the component is
visually substantial. Fix findings. Do not report-and-move-on.

## Deliverables

- The component implementation (styles + script where needed).
- A demonstration of every state and variant (a demo/story view or section).
- A usage example with realistic content.
- The component reference entry.
- Confirmation of which audits passed.
