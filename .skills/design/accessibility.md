# Accessibility

Accessibility is a first-class design constraint, present from the first
sketch. The baseline is WCAG 2.1 AA (Level A required, AA expected).

## Structure and semantics

- Use semantic HTML: `header`, `nav`, `main`, `section`, `article`, `aside`,
  `footer`, `ul/ol`, `table` with real headers.
- One logical `<h1>` per page; heading levels descend logically and are not
  skipped for styling reasons. Headings describe the content, not the look.
- Use native elements first (`<button>`, `<a>`, `<dialog>`, `<select>`,
  `<details>`) before layering custom behavior. Custom widgets only when native
  cannot do the job — and then with full keyboard/ARIA behavior.
- ARIA only when native semantics are insufficient; prefer native over
  `role`/`aria-*` when possible.

## Keyboard

- Everything operable by keyboard alone: nav, menus, modals, carousels,
  accordions, tables with sorting, tabs, custom selects, drag-and-drop
  alternatives.
- Visible focus at all times: a clear focus indicator on every interactive
  element, never removed or invisibly styled. Focus order matches visual
  order.
- No keyboard traps (escape from modals/drawers, focus returns predictably).
- Logical tab order: primary task reachable with few tabs.

## Labels and instructions

- Every form control has a programmatic label (`<label>` or `aria-label`),
  including icon-only controls, search inputs, and filters.
- Placeholder is never the only label.
- Grouped controls (`fieldset`/`legend`) for radio groups and checkboxes.
- Instructions and error messages are associated with their fields
  (`aria-describedby`), announced, and recoverable.
- Errors: describe the problem and how to fix it, not just "invalid".

## Color and contrast

- AA contrast: 4.5:1 normal text, 3:1 large text and UI components.
- Meaning is never conveyed by color alone — pair with text, icon, or shape
  (status badges, validation, links).
- Focus indicators contrast with the surrounding surface.

## Motion

- Honor `prefers-reduced-motion: reduce` — suppress non-essential motion
  (`design/motion.md`). The reduced-motion contract in
  `design/motion-system.md` is mandatory for every product.
- No content depends on an animation to be understood.

### Immersive and high-craft products

For motion-driven experiences (`workflows/create-high-craft.md`) the reduced-
motion contract is stricter, defined per effect class before implementation:

- Remove non-essential continuous motion (ambient loops, drifting layers).
- Remove parallax; replace with static composed depth (size/overlap/shadow).
- Reduce large camera movements and excessive scale transitions to simple
  opacity changes or static states.
- Keep state feedback understandable — essential transitions may remain in a
  minimal form where they carry meaning.
- Never hide content behind motion; never require motion to understand the
  interface. Anything whose visibility depends on an animation must be visible
  under reduced motion (`design/progressive-enhancement.md`).

Keyboard navigation, focus visibility, semantic structure, contrast, screen-
reader accessibility, and responsive behavior remain fully mandatory at every
motion intensity level — including through pinned/scroll-driven sections.

## Screen readers and dynamic content

- Dynamic updates that matter are announced via `aria-live` (toasts, status
  changes, search results), not just visually.
- Modals/dialogs manage focus and restore focus on close.
- Alt text describes function and content of images; decorative images are
  hidden from assistive tech (`alt=""` or `aria-hidden`).
- `lang` attribute set; no all-caps text communicated by styling alone.

## Touch and target size

- Interactive targets ≥44×44px on touch (40px absolute minimum with adequate
  spacing).
- Adequate spacing between targets to prevent mis-taps.

## Rules

- The product works without a mouse, without color, and without motion.
- Accessibility failures are blocking findings, not polish items.
- If a design choice and accessibility conflict, the accessible version wins;
  find the elegant accessible solution instead of arguing for the other one.
