# Motion System

Motion treated as a language, not a collection of effects. This file is the
authoritative reference for **motion grammar** (roles, relationships,
choreography) and the **motion intensity scale (0–5)**. The recipes and the
interaction checklist live in `design/motion.md`; advanced techniques live in
`design/impressive-motion.md`; workload limits live in `design/motion-budget.md`.

The core discipline: every component does NOT invent its own animation
behavior. Motion across a product shares one grammar — one easing family, one
duration scale, one entrance pattern, one way things appear and leave. When
every element moves differently, the interface reads as random. When elements
move according to shared rules, the interface reads as designed.

---

## Motion roles

Every animation in a product fills exactly one of these roles. If an animation
fills none of them, it does not exist.

| Role | Job | Examples |
|---|---|---|
| **Feedback** | Confirm the user's action happened | Button press scale, hover lift, input focus ring, toggle snap |
| **State transition** | Show that something changed identity | Loading → content crossfade, tab switch, error shake, success check |
| **Navigation** | Preserve spatial orientation while moving between views | Page slide/fade, drawer open from edge, breadcrumb collapse |
| **Reveal** | Introduce content without it popping into existence | Scroll-triggered fade-up, image clip-path reveal, line-by-line text mask |
| **Narrative** | Advance a story or sequence the user is following | Scroll-driven chapter transitions, stepped process reveals |
| **Emphasis** | Direct attention to what matters right now | CTA pulse once after load, metric count-up, badge draw-in |
| **Spatial** | Express depth and physical relationships | Parallax layers, card tilt, camera-style section push |
| **Ambient** | Keep the scene alive during inactivity | Slow Ken Burns drift, status-dot pulse, gradient breathing |

Rules:

- **Feedback and state-transition motion are mandatory everywhere.** Every
  product, at every intensity level, has them.
- **Narrative, spatial, and heavy ambient motion are experiential.** They are
  justified per product, not per component. See the intensity scale below.
- **One element, one dominant role.** A scroll reveal that also parallax-drifts
  and also pulses is three animations competing for attention.

---

## Motion relationships

Motion behaves consistently *between* things, not just within them.

### Section to section
- Sections hand off with a consistent transition logic: if one section reveals
  its content upward as you enter it, all sections do.
- Rhythm is deliberate: entrance timing may vary in distance but not in easing
  character.

### Component to component
- All components of the same type animate identically. Every card lifts the
  same way. Every modal opens from the same origin logic.
- Related components share choreography: if a list item expands, sibling items
  yield smoothly rather than jumping.

### Navigation and content states
- Moving forward feels different from moving back (forward: content enters;
  back: content returns). Direction carries meaning.
- Loading → loaded uses the same resolve pattern everywhere (skeleton shimmer
  → crossfade), never a different trick per screen.

### Media and typography
- Images and text use the same reveal family as their containers. A masked
  headline and a masked image belong to the same visual system.
- Typography never animates in a style unrelated to the layout's motion
  personality (e.g., playful bounce letters on a stark editorial grid).

### User interaction
- Hover, press, focus, and disabled each have ONE defined behavior reused by
  every interactive element of the same class.
- Focus behavior is never decorative; it is always visible first, animated
  second.

---

## Choreography

Motion communicates hierarchy through sequencing.

### The hierarchy rule

> Primary element arrives first. Supporting content follows. Secondary
> decoration arrives last. Never animate everything simultaneously.

```text
Entrance sequence example (hero):
  0ms     Headline line 1 rises into view
  120ms   Headline line 2 follows
  260ms   Supporting paragraph fades up
  380ms   Primary CTA scales in
  500ms   Secondary link fades in
  600ms+  Ambient layer begins drifting (runs continuously after)
```

### Choreography inventory

Decide each of these deliberately for products at Level 2+:

- **Entrance choreography** — order, direction, distance, stagger interval.
  Stagger 30–60ms within groups; groups themselves stagger 80–150ms apart.
- **Exit choreography** — exits are faster than entrances (roughly 60–70% of
  the duration). Elements leave toward where they came from.
- **Stagger sequencing** — top-to-bottom for lists, center-out for focal
  clusters, reading-order for editorial layouts. Never random.
- **Scroll choreography** — which elements are viewport-entry triggered vs.
  scroll-position-linked. Entry-triggered plays once; scroll-linked tracks
  position both directions.
- **Text choreography** — line masks for headlines, word-level for subheads.
  Body copy never animates letter-by-letter.
- **Image/media reveals** — one reveal family per page (clip-path, scale-mask,
  blur-up). Reused, not reinvented per image.
- **Section transitions** — how one section hands to the next: hard cut,
  crossfade, pinned handoff, color shift. Chosen once, applied consistently.
- **Layout transitions** — expansion/collapse moves siblings smoothly
  (`grid-template-rows` animation or FLIP), nothing teleports.
- **State transitions** — loading/success/error each have defined motion.
- **Hover / press / focus behavior** — hover invites (lift, underline draw),
  press confirms (scale down), focus guarantees visibility (ring).
- **Loading choreography** — skeleton resolves to content; progress never
  loops forever without an escape hatch.
- **Navigation transitions** — view changes preserve context (shared header,
  sliding panels); users always know where they came from.
- **Cursor interactions** — only when they serve the concept (Level 3+),
  pointer-fine devices only, always with a touch/no-motion fallback.

### Anti-choreography

- Everything animating at once on load = no hierarchy.
- Every element having a unique easing/direction = no grammar.
- Decoration animating before content = inverted priorities.
- Re-triggering entrance animations on scroll-back-up (unless the narrative
  explicitly calls for it) = novelty wearing off into annoyance.

---

## Motion intensity levels (canonical scale)

This 0–5 scale replaces the earlier 1–3 scale. Choose the **lowest level**
capable of achieving the desired experience. Do not raise the level merely
because the product is a marketing site.

### Level 0 — Static
No motion beyond default browser behavior. Deliberate choice for utility
contexts (print previews, extreme-performance targets, embedded views).
Content is fully readable and usable without any transition.

### Level 1 — Micro-interaction
Small feedback transitions and state changes only: hover, press, focus,
toggles, modals, toasts, tab indicators. Durations 80–250ms. No scroll-driven
motion, no ambient loops. Typical: dashboards, admin panels, forms, data tools.

### Level 2 — Expressive
Strong component-level motion and coordinated entrances: page-load staggers,
scroll-triggered reveals, text/image reveals on key sections, one or two
ambient elements. Durations up to ~1000ms with stagger. Typical: standard
landing pages, templates, marketing sites, portfolios.

### Level 3 — Choreographed
Scroll-driven sequences, narrative transitions, sophisticated sequencing:
pinned sections, multi-step scroll stories, coordinated section handoffs,
cursor-responsive moments where justified. Requires a motion budget (see
`design/motion-budget.md`). Typical: premium brand sites, campaign pages,
editorial experiences, high-end portfolios.

### Level 4 — Immersive
Complex spatial movement, canvas experiences, advanced transitions:
full-viewport canvas scenes, WebGL-enhanced sections, camera-like depth
movement, custom navigation paradigms. Requires motion budget, progressive
enhancement architecture (`design/progressive-enhancement.md`), and explicit
mobile/reduced-motion strategies. Typical: immersive product launches,
brand worlds, cinematic presentations.

### Level 5 — Experimental
Highly art-directed experiences where motion IS part of the product concept:
interactive generative systems, physics-driven interfaces, unconventional
navigation. Justification required in the direction brief; the experience must
remain completable and comprehensible. Fallback path is mandatory.

Rules:

- Levels are cumulative downward, not upward: L4 includes everything allowed
  at L2, plus more — but more is not required. An L4 product can still have
  quiet sections.
- Interaction feedback (L1 behaviors) exists at every level including L5.
- The level is chosen once per product (per major surface at most), recorded
  in the direction brief, and drives the motion budget.

---

## Interaction feedback vs. experiential motion

These two categories are governed by different rules:

### Interaction feedback — essential, always present
Hover, press, focus, state changes, loading, success/error feedback. These are
required at every intensity level for every product category. They are part of
usability, not decoration.

### Experiential motion — optional, justified per product
Scroll choreography, parallax, cinematic transitions, 3D, canvas, shaders,
custom cursors, complex morphing. These exist when the art direction calls for
them and the budget allows. Being absent is a valid decision.

> Accessibility overrides decorative motion. Under `prefers-reduced-motion`,
> experiential motion is removed or replaced with static equivalents; essential
> feedback remains understandable (see `design/accessibility.md`).

---

## Technology selection ladder

Choose the least complex implementation capable of achieving the desired
experience. Walk down this ladder only as far as needed:

```text
CSS (transitions, keyframes, @property)
        ↓  only when CSS cannot express it
CSS + native browser APIs (IntersectionObserver, Web Animations API,
     View Transitions, scroll-driven animations)
        ↓  only when native APIs fall short
Existing project animation library (if the stack already has one)
        ↓  only when none exists and complexity demands it
Motion / Framer Motion or equivalent (component orchestration, React)
        ↓  only when timeline sequencing is core to the experience
GSAP or equivalent timeline system (complex scroll narratives, pinning)
        ↓  only for procedural/pixel work
Canvas / WebGL (particles, shaders, generative scenes)
        ↓  only when real spatial/interactive objects are justified
Three.js / React Three Fiber
```

Rules:

- This is guidance, not a mandate — respect the project's existing stack. If
  the project already uses GSAP, use GSAP; do not add Motion alongside it.
- Never introduce a new animation or 3D dependency into a marketplace product
  unless the experience genuinely requires it, and document why in the
  customization guide.
- Before installing anything: can CSS do it? Can one small helper function do
  it? Can an existing dependency do it?
- 3D-specific decisions follow `design/3d-guidelines.md`.
- Performance cost is part of the decision: see `design/motion-budget.md`.

---

## Reduced motion contract

Every level above L0 defines its reduced-motion behavior up front:

- Remove non-essential continuous motion (ambient, parallax, idle loops).
- Replace scroll-linked movement with static composition.
- Reduce large camera/scale movements to simple opacity changes.
- Keep feedback instant and non-kinetic where possible; keep state meaning
  intact.
- Content must never be hidden behind motion: anything whose visibility
  depends on an animation must be visible under reduced motion.
- Never require motion to understand the interface.

Full accessibility rules: `design/accessibility.md`. Layering strategy:
`design/progressive-enhancement.md`.
