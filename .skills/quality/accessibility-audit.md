# Accessibility Audit

Verifies the product against the requirements in `design/accessibility.md`.
Accessibility failures are blocking findings, never polish items.

## Structure and semantics

- Semantic landmarks used correctly (`header`, `nav`, `main`, `footer`).
- One logical `<h1>`; heading levels descend without skips.
- Native elements preferred; custom widgets only where necessary.
- `lang` attribute set on the document.
- No heading-like text that is not a heading; no heading that is styled as
  body text and expected to be found.

## Keyboard

- Full keyboard operability: tab through the whole product, operate every
  interactive control (menus, modals, tabs, accordions, carousels, sortable
  tables, custom selects).
- Visible focus on every interactive element; focus indicators never removed.
- No keyboard traps; modals capture and restore focus correctly.
- Focus order matches visual order; primary tasks are reachable quickly.

## Labels and forms

- Every control has a programmatic label; icon-only controls are labeled.
- Placeholders are not the only labels.
- Fieldset/legend for grouped controls.
- Errors are associated with fields, described, and recoverable.
- Validation doesn't rely on color alone.

## Color and contrast

- AA: 4.5:1 normal text, 3:1 large text and UI component boundaries.
- State and meaning communicated beyond color (status badges, icons, text).
- Focus indicators contrast with surfaces.

## Motion and media

- `prefers-reduced-motion` honored for non-essential motion.
- No information conveyed only via animation.
- Images have appropriate alt text; decorative images hidden.
- Video/audio (if any) has captions or alternatives.

## Dynamic content

- Live regions (`aria-live`) announce important dynamic updates (toasts,
  results, status changes).
- Screen-reader announcements match what is visually happening.

## Touch

- Targets ≥44×44px (40px minimum with spacing) on touch interfaces.

## Sign-off

Report Pass / Conditional / Fail per category. Blocking: any failure that stops
keyboard-only, screen-reader, or low-vision users from completing a task. Fix
blocking before ship and re-verify.
