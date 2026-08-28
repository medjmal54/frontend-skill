# Visual Audit

The gate that decides whether the product looks intentionally designed and
feels alive. Run before sign-off on anything visual.

## The Three Tests (All Must Pass)

### Test 1: Soul Test (Animation)

Answer each honestly. A "No" on any = blocking finding.

- Does every interactive element animate on hover? Cards lift, buttons
  shift, links transition. If any element changes state without a visible
  transition, it's dead.
- Does every click produce feedback? Press animation, scale change,
  navigation transition. If a click does nothing visible, it's broken.
- Do lists and grids stagger in on load? If all items appear at once
  with no stagger, the entrance is lifeless.
- Do modals/drawers/toasts animate open and closed? If they just appear
  and disappear, the product has no soul.
- Are state changes (loading, toggle, tab) animated? If a skeleton
  instantly swaps to content, or a toggle just flips, it's static.
- Does the product respect reduced motion? If not, it's an accessibility
  failure.

If any answer is "No," the product is incomplete. Add the missing animation
before proceeding. Do not ship a static product.

### Test 2: Anti-Slop Test (Design Identity)

These are investigation triggers. A "No" on identity questions = redesign.
A blacklisted pattern = investigate justification, not automatic failure.

- Could a designer identify this product's industry/audience from the
  design alone, without reading the copy? If not, the design has made
  no decisions. **Blocking.**
- Does at least one design choice surprise in a good way? If every choice
  is the "safe default," the product has no identity. **Blocking.**
- Would this be confused with a generic template in a thumbnail test among
  ten similar products? If yes, redesign. **Blocking.**
- Is the typeface on the blacklist (Inter, Roboto, Arial, Space Grotesk)?
  **Investigate.** Can you articulate why this font serves THIS product?
  If yes, document justification and proceed. If no, redesign.
- Is the color scheme on the blacklist (purple/blue gradient on white,
  indigo to violet to pink, default Tailwind blue)?
  **Investigate.** Same justification test.
- Is the hero a centered heading + paragraph + two buttons?
  **Investigate.** Same justification test.
- Are features presented as a 3-column card grid?
  **Investigate.** Same justification test.
- Hero section constraints met: Header under 80px? Headline 2 lines or
  fewer? Subtext 20 words or fewer? CTA visible without wrapping? If no,
  fix before delivery. **Blocking.**
- Empty, loading, and error states present? Missing states = **blocking.**
- No transition: all? No animation on width/height/margin/top/left?
  Transform and opacity only? If no, fix. **Blocking.**
- Semantic HTML correct? Wrong headings, missing landmarks, improper role
  usage? If no, fix. **Blocking.**
- **Imagery present?** Does every section have real visual content (not
  just colored boxes)? Empty imagery = **investigate.** Justified for
  text-only tools (terminal, code editor, API client).
- **Dashboard data visualization?** If this is a dashboard, are there
  charts/graphs and sparklines on metric cards? No charts = **investigate.**
  Justified for status monitors where indicators replace charts.

Read `design/ai-slop-firewall.md` and run the full six-stage evaluation.
Additional investigation checks from the firewall:

- **Card disease?** Are features, stats, testimonials, pricing, settings,
  and users all presented as identical cards? Cards must earn their
  existence. **Investigate.**
- **Global border-radius?** Is one radius value (e.g. 16px) applied to
  cards, buttons, inputs, modals, images, sidebars? Geometry must
  communicate hierarchy. **Investigate.**
- **Random icons?** Do features get icons merely because a space looks
  empty? Icons must carry semantic weight. **Investigate.**
- **"Icon + heading + paragraph" x6?** Are features presented as 3–6
  identical icon-heading-paragraph blocks? Force composition diversity.
  **Investigate.**
- **Floating everything?** Are badges, cards, screenshots, blobs, pills
  floating independently around the hero? Elements need spatial anchors.
  **Investigate.**
- **Excessive glassmorphism?** Is backdrop-filter: blur() everywhere,
  especially dark bg + glass cards + purple glow? Glass represents
  real layering, not decoration. **Investigate.**
- **Fake depth?** Is box-shadow: 0 20px 40px on everything? Depth
  establishes hierarchy, not decoration. **Investigate.**
- **AI startup vocabulary?** Does the copy use Revolutionize, Transform,
  Supercharge, Unlock, Seamless, Powerful, etc.? Write from the user's
  actual workflow. **Investigate.**
- **Fake metrics?** Are there "10K+ Happy Customers", "99.9% Uptime"?
  Never fabricate business claims. **Blocking** (almost never justified).
- **Generic names?** John Doe, Acme Inc., Nova, Lumina? Use
  domain-specific fictional entities. **Investigate.**
- **Excessive pills?** Are status indicators always pills (Active, New,
  Premium)? Status matches semantic importance. **Investigate.**
- **Everything perfectly symmetrical?** Is every section centered with
  identical balance? Prefer meaningful asymmetry. **Investigate.**
- **Three-column law?** Are three things always in three columns? Grid
  count follows content relationships. **Investigate.**
- **Mobile = desktop squeezed?** On mobile, does the sidebar + main +
  right panel just stack vertically? Mobile reconsiders hierarchy.
  **Investigate.**

### Test 3: Layout Test (Structure)

- Is there a top navbar with navigation, search, and user avatar (for app
  and dashboard UIs)? If missing, add it. **Blocking** for app UIs.
- Is data displayed as cards, not tables? Table elements or table-like
  grid layouts for browsing data = **investigate** (justified for
  genuinely tabular data like ledgers, audit logs, changelogs).
- Is there a slide-over panel or detail view for inspecting individual
  records? If clicking a card does nothing or navigates to a new page,
  redesign. **Investigate.**
- Does the layout restructure on mobile, not just shrink? Cards should
  stack, not squish. Sidebar should collapse or become a drawer.
  **Blocking.**

## Method

1. Review every view/component at rest (no animation, default states).
2. Review the states: hover, focus, active, disabled, loading, empty, error.
3. Trigger every hover and click. Confirm animation exists and is smooth.
4. Review at the primary sizes: mobile, tablet, desktop.
5. Review the "thumbnail test": at a glance, is the intent legible?
6. Review the "identity test": could you identify this product among ten
   similar ones in a thumbnail? If not, it has no identity.
7. Check the generic-AI patterns from design/anti-generic.md.
8. Check the font and color blacklists — **investigate, don't auto-fail.**
9. Confirm staggered entrance animations on lists and grids.
10. Confirm slide-over/modal/toast animations.

## Findings Format

- **Blocking** — Failed a test with no possible justification. Product
  cannot ship. Redesign.
- **Investigate** — Blacklisted pattern detected. Can you articulate a
  product-specific justification? If yes, document it and proceed. If no,
  treat as blocking.
- **Major** — One view or component visibly violates the system. Must fix.
- **Minor** — Small inconsistencies, nits.

## Sign-off

The product ships only when all three tests pass, blocking and major
findings are resolved, investigate items have documented justifications,
and the animation checklist from SKILL.md Law 1 is fully covered.
