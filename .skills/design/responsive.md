# Responsive

Responsive design is not "desktop but smaller." Layouts restructure,
re-prioritize, and re-shape for the device.

## Philosophy

- **Mobile-first thinking, even when designing desktop-first.** Decide the
  content priority first, then how each breakpoint reorders it.
- **Restructure, don't shrink.** Navbar becomes a menu or transforms; table
  becomes cards or scrolls; multi-column grids collapse; forms reflow;
  sidebars move or hide with accessible alternatives.
- **Content priority drives layout.** On small screens, the user's primary
  task comes first. Secondary content moves down or behind progressive
  disclosure — it does not just get smaller.

## What to check per breakpoint

- **Navigation transformation** — the nav must become touch-operable, with a
  visible, accessible menu pattern (not hover-only).
- **Typography scaling** — fluid type via `clamp()` where it helps; never
  shrink everything to unreadable sizes. Body text never below ~16px on mobile.
- **Grid changes** — columns reflow to 1–2 columns; gutters narrow
  consistently.
- **Touch targets** — interactive elements at least 44×44px (40px absolute
  minimum with adequate spacing). No hover-only affordances.
- **Dashboard Viewports & Canvases** — Ensure that `100vh` layouts on desktop scale down to linear streams without horizontal overflow. Replace split grids with a mobile tabbed navigation panel or card deck.
- **Tables & Data Lists** — Flat raw tables are prohibited on mobile devices. Collapse data lists into visual card-strips, and open full-screen slide-over drawers for record editing or inspection.
- **Forms & Actions** — Inputs must expand to full width (`100%`); slide-over overlays or action drawers must capture focus and expand to `100vw` with touch targets optimized for mobile keyboards.
- **Overflow** — nothing clips important content; long content wraps or
  truncates intentionally.
- **Images and media** — responsive sources or correct object-fit/cropping so
  art direction holds on small screens.
- **Spacing** — the spacing scale still applies; sections tighten coherently
  rather than losing rhythm.
- **Interaction changes** — hover-dependent interactions get tap alternatives;
  sticky elements don't eat the viewport.

## Breakpoints

- Define breakpoints as tokens and use them consistently (e.g., ~640 / 768 /
  1024 / 1280). Test at real device widths, not just the breakpoint boundaries.
- Use container queries where a component lives in varying-width contexts and
  its layout should respond to its container, not the viewport.

## Immersive experiences across breakpoints

Immersive/high-craft products (`workflows/create-high-craft.md`) do not
shrink desktop experiences. Each breakpoint is an intentional re-direction of
the same concept:

- **Reduce depth** — fewer planes, smaller speed differences between layers;
  on mobile collapse to two planes (content / atmosphere) where possible.
- **Simplify animation** — halve continuous-animation counts, keep at most one
  ambient element, drop scroll-parallax in favor of simple entry reveals.
- **Remove or reduce 3D** — replace canvas/WebGL scenes with static renders
  or poster media unless the scene IS the product (`design/3d-guidelines.md`).
- **Fewer simultaneous elements** — one focal point per viewport; entrance
  staggers shortened.
- **Change composition** — sections may reorder, merge, or transform
  (pinned scenes become stacked reveals; split compositions become sequences).
- **Change interaction models** — hover-dependent depth/reveal interactions
  get tap/scroll equivalents; custom cursors disappear on touch.
- **Reduce scroll complexity** — long pinned sequences compress; horizontal
  scroll sections become vertical stacks or swipe rails with clear affordance.
- **Performance tiering** — lower DPR caps, reduced particle counts, video
  swapped for posters on constrained devices.

Mobile is intentionally art-directed: author the mobile composition as its own
decision (what leads, what breathes, what one moment carries the brand), not
as a degraded desktop. Verify at every breakpoint that the base-experience
contract still holds (`design/progressive-enhancement.md`).

## Rules

- Every component is defined at the sizes it actually appears in.
- Primary task reachable within one tap/scroll on mobile.
- No content requires hover to be discovered.
- No horizontal page scroll on any breakpoint (except intentional, accessible
  scroll containers).
