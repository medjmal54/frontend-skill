# Code Audit

Assesses maintainability, organization, and technical quality. A product that
only looks good in a screenshot is not a product.

## Structure and maintainability

- Clear file organization; components divided at sensible boundaries.
- Consistent naming conventions across files, components, classes, and tokens.
- No duplicated components that do the same job.
- No dead code, commented-out blocks, or unused imports/exports.
- Components are reusable, not copy-paste specializations.

## Design-system integrity

- Design tokens used instead of magic values (no scattered hex codes, spacing
  numbers, font sizes).
- One token source per property; no conflicting values for the same role.
- State and variant patterns implemented consistently across components.

## Dependencies

- No unnecessary frameworks or libraries. A simple implementation that suffices
  is preferred (`SKILL.md`, technical quality).
- **Technology stack compliance:** Component packs must be plain HTML + CSS + JS
  (no React/Vue dependency). Static sites and dashboards must use React.
  Mismatched stacks are a blocking finding.
- Third-party dependencies are justified, maintained, and their licenses are
  acceptable for distribution (see `marketplace/compliance.md`).
- No vendored code without license attribution.

## Performance

- No obvious render loops or layout-thrashing animation properties.
- Motion uses `transform`/`opacity` (`design/motion.md`).
- Images/typography loaded without waste; no unused fonts or icon sets.
- No blocking scripts where defer/async applies.
- Large lists/datasets rendered responsibly (virtualization or pagination when
  warranted).

## HTML/CSS validity

- Valid, well-nested markup; correct elements for the job (`<button>` for
  actions, `<a>` for navigation).
- No inline styles where tokens/classes should be used.
- No duplicated CSS rules; specificity stays flat.
- IDs used only where genuinely needed (form controls, ARIA wiring).

## JavaScript quality

- Clear state management; no undocumented global mutation.
- Event handling avoids leaks (proper cleanup where listeners are added).
- Errors handled; async paths don't silently fail.
- Code is well-commented: JSDoc for functions, inline comments for complex logic.
- Magic numbers have explanatory comments or are converted to tokens.

## React-specific quality (if applicable)

- **Keys are stable and unique.** Keys must not depend on array index (causes
  re-mounting on reorder). Use database IDs or stable identifiers. Unstable
  keys are a blocking finding.
- **Empty, loading, and error states are present.** Every async operation must
  have a visible state for loading, success, and failure. Missing states are a
  blocking finding.
- **No missing dependencies.** ESLint `exhaustive-deps` warnings indicate
  missing dependencies or incorrect cleanup. Fix before ship.

## Findings

Classify as Blocking (broken builds, duplicate systems, licensing problems,
magic-value chaos), Major (reusability failures, inconsistent conventions, dead
code), or Minor (naming nits). Fix before ship.
