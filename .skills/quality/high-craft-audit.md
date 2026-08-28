# High-Craft Audit

Dedicated audit for products built via `workflows/create-high-craft.md` —
immersive, art-directed, motion-driven, spatial, or 3D-enhanced experiences.
Run IN ADDITION to the standard audits (`quality/visual-audit.md`,
`quality/accessibility-audit.md`, `quality/responsive-audit.md`,
`quality/code-audit.md`, `quality/ux-audit.md`), not instead of them.

A failure in **originality**, **accessibility**, or **basic usability** is a
redesign trigger — not a patch item.

---

## 1. Art Direction

- Is the visual identity specific to this product (not a genre costume)?
- Does it feel authored — could a designer put their name on it?
- Is the concept coherent: can any two visual decisions be explained by the
  same single idea (`design/art-direction.md` coherence test)?
- Is there a recognizable signature/motif recurring across sections?
- Does the composition support the product's message and hierarchy?
- Are any forbidden generic combinations present (purple/blue gradient +
  white cards, centered SaaS hero + two buttons, random glassmorphism,
  floating blobs, arbitrary glows, purpose-free decorative 3D)? Any = Blocking.

## 2. Motion

- Does motion follow one consistent grammar across sections, components,
  navigation, and states (`design/motion-system.md`)?
- Is every animation's role nameable (feedback / state / navigation / reveal /
  narrative / emphasis / spatial / ambient)?
- Are entrances choreographed by hierarchy (primary first, decoration last) —
  or does everything animate simultaneously? Simultaneity at scale = Major.
- Is the chosen intensity level (0–5) appropriate — and is it the LOWEST level
  achieving the experience objective?
- Are there unnecessary animations? Anything animating without a role is
  removed, not defended.
- Do exits run faster than entrances? Is stagger rhythmic rather than random?

## 3. Spatial Design

- Are depth planes defined and does content occupy them deliberately
  (`design/spatial-composition.md`)?
- Is hierarchy clear from position/scale/overlap alone?
- Does composition create visual rhythm (dense/open pacing), or is spacing
  uniform?
- Is spatial movement (parallax/sticky/camera-style transitions) coherent —
  one system per section, both-direction smooth, meaningful?
- Every overlap expressible as a relationship? Unexplained overlaps = Major.

## 4. 3D (only if present)

- Is it justified by the 8-question gate (`design/3d-guidelines.md`)? If the
  written answers don't exist or are weak → remove or demote the implementation
  level.
- Is it performant (DPR cap, lazy init, disposed on unmount, paused offscreen)?
- Does it communicate something product-native (concept-driven test)?
- Is there a designed static fallback that preserves composition?
- Does it work on mobile (reduced scene or fallback) and under reduced motion
  (static/frozen/hidden per rules)?

## 5. Performance

- Does the page become interactive quickly (base experience usable before
  enhancement layers load)?
- Are heavy assets deferred (images lazy, video poster+metadata, WebGL scenes
  initialized on intersection/intent)?
- Is the motion budget (`design/motion-budget.md`) respected — continuous
  element count, scroll-linked count, blur usage, one shared rAF loop?
- Are animations GPU-friendly (transform/opacity only; no layout properties;
  no `transition: all`)?
- Is unnecessary continuous animation avoided/paused offscreen?
- Mobile tier reductions actually implemented (not just documented)?
- Measured jank on a low-end profile with budget violations = Blocking;
  violations without measured jank = Major.

## 6. Accessibility

- Is `prefers-reduced-motion` respected everywhere: non-essential continuous
  motion removed, parallax removed, large camera/scale movements reduced,
  content never hidden behind motion, feedback still understandable?
- Is all content accessible without motion (nothing requires animation to be
  read or understood)?
- Is keyboard navigation functional through the ENTIRE experience — including
  pinned/scroll-driven sections (keyboard advances the story)?
- Is focus visible over every background state the experience passes through?
- Is contrast adequate at every scroll position (over media, gradients,
  canvas frames)?
- Screen reader walkthrough sensible (order, labels, announced state changes)?

Any accessibility failure = Blocking. Accessibility overrides experiential
motion every time.

## 7. Originality

- Does the work have its own identity, or is it executing a recognizable trend
  recipe? Run the anti-recipe check: dark background + giant white type +
  glowing gradient + grain + glass cards + custom cursor + Three.js sphere +
  particles + magnetic buttons + Lenis-style smoothing + parallax + marquee
  ALL PRESENT AT ONCE = generic "high-craft AI aesthetic" = redesign.
  Fewer techniques, stronger conceptual coherence.
- Could the result be confused with a specific existing website, studio
  portfolio piece, or marketplace template? If yes → redesign.
- Were references transformed into principles and techniques (scroll-driven
  storytelling, kinetic typography, spatial composition…) rather than copied
  as arrangements, palettes, or identities? See the Originality Firewall in
  `design/ai-slop-firewall.md`.
- Is the Originality Rationale from the workflow present and honest?

---

## Verdict format

Report per section: Pass / Conditional / Fail, with findings classified
Blocking / Major / Minor and file/line references where possible.

**Ship rule:** the product ships only when every Blocking finding is resolved
by redesign (where required), all standard audits also pass, and the base
experience contract (`design/progressive-enhancement.md` failure contract) is
verified under JS-off, WebGL-off, reduced-motion, and throttled-network
conditions.
