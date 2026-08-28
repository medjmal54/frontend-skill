# Responsive Audit

Verifies the product restructures correctly across devices — it does not
"shrink". See `design/responsive.md` for the philosophy behind the checks.

## Test matrix

Test at minimum: a phone (~360–430px), a tablet (~768–834px), a laptop
(~1280–1440px), and a large desktop (≥1536px) if the product targets wide
screens. Test in portrait and landscape where layout differs.

## Checklist

- **Navigation** — transforms to a touch-operable pattern; no hover-only
  menus; menu state is accessible (button + expanded state announced).
- **Typography** — legible at every size; no unreadable body text; headings
  wrap well; no orphaned single words ruining headings.
- **Grid reflow** — columns collapse sensibly; nothing becomes a single-column
  straggler with absurd proportions; gutters follow the scale.
- **Touch targets** — ≥44×44px (40px minimum with spacing) for all
  interactive elements; adequate tap spacing.
- **Dashboard Canvases** — Viewport height constraints (`100vh`) adapt cleanly to mobile; split-pane grids collapse to vertical tabbed views or linear lists without breaking the layout.
- **Tables and Data** — Flat tables are blocked on mobile; horizontal scrolling containers are forbidden for primary dashboard workflows. Instead, convert card-strips to block-level data cards, and collapse details into full-screen drawers.
- **Forms & Inline CRUD** — Inline actions, edit fields, and drawers expand to fill the screen on mobile devices (`width: 100vw`); touch buttons and active areas are easy to interact with.
- **Overflow** — No horizontal page scroll; long words, URLs, and code wrap or truncate gracefully.
- **Images and media** — correct art direction and cropping at each size;
  responsive sources in use.
- **Spacing** — rhythm preserved while tightening; no cramping at one
  breakpoint and ballooning at the next.
- **Interaction changes** — hover interactions have tap alternatives; sticky
  elements don't cover content or controls.
- **Content priority** — the primary task stays reachable with minimal
  scrolling on mobile.

## Sign-off

Blocking: unusable at any tested size (broken nav, clipped content, impossible
touch targets, unreadable text). Major: layouts that merely shrink, tables that
break, spaced inconsistently at a breakpoint. Fix before ship.
