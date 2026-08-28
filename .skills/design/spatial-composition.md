# Spatial Composition

How to design the z-axis and the viewport as a composed space rather than a
stacked column of sections. Spatial composition is what separates an
art-directed experience from "cards stacked vertically with parallax added."

Depth, overlap, scale, and negative space are compositional materials — same
rank as typography and color. They carry meaning: hierarchy, relationships,
narrative order, focus.

---

## The depth model

Every spatial composition defines three planes and assigns content to them
deliberately:

```text
FOREGROUND  — interactive content, primary CTAs, focal media.
              Moves most (or is fixed while others move).
MIDGROUND   — supporting content, cards, secondary imagery.
              Moves with scroll or slightly slower.
BACKGROUND  — atmosphere, environment, texture, ambient type.
              Moves slowest or stays anchored.
```

Rules:

- Every element belongs to exactly one plane. Ambiguous depth reads as broken
  layering, not richness.
- The plane assignment must serve meaning: the product's most important object
  sits closest (largest, sharpest, fastest) unless the concept deliberately
  inverts this (e.g., the brand recedes to make space for the user's content).
- Depth is communicated by at least two simultaneous cues: size difference +
  speed difference, or overlap + shadow/blur difference. A single cue alone
  reads as flat.

## Z-axis hierarchy

- Define a small, explicit layer system as tokens (`--z-background`,
  `--z-content`, `--z-raised`, `--z-overlay`, `--z-navigation`) instead of
  arbitrary z-index values scattered through CSS.
- Overlaps are intentional compositions, not accidents: an image may crop a
  headline; a card may straddle two sections; a sticky anchor may pin while
  siblings pass over it. Each overlap should be explainable ("the spec sheet
  physically sits on top of the machine photo because inspection is the job").
- Elevation (shadow/blur) supports the layer story established by position;
  it never contradicts it.

---

## Compositional tools

### Negative space
Empty regions are load-bearing. Negative space directs the eye, creates
tension around a focal point, and gives dense moments their punch. Decide
where the page breathes and where it compresses — do not distribute padding
uniformly (see `design/spacing.md`).

### Focal points
Each viewport-height unit has one dominant element. Scale, contrast, motion,
and isolation all point at it. Two competing focal points in one viewport =
no focal point.

### Asymmetric composition
Asymmetry creates energy: offset columns, elements breaking the grid edge,
unequal splits (7/5, 8/4), text wrapped around media masses. Asymmetry serves
hierarchy and identity (see `design/design-direction.md`) — it is never random
jitter.

### Viewport composition
Compose per viewport, not per document. At any scroll position, what is on
screen should look like a deliberate frame: balanced masses, a clear entry
point for the eye, no orphaned fragments cut awkwardly by the fold. Check the
page at multiple scroll positions during review, not just top and bottom.

### Sticky spatial anchors
`position: sticky` pins create stage-like scenes: one element holds position
while others move across or past it. Use for narrative handoffs, comparison
moments, and progress-anchored stories. Never stack so many sticky layers that
scrolling feels hijacked.

### Parallax depth
Parallax is ONE tool of many, not the definition of spatial design. When used:
one coherent parallax system per section (2–3 layers with distinct speed
multipliers), disabled under reduced motion, reduced or removed on mobile
(`design/responsive.md`). Scroll-linked movement always tracks both directions
smoothly.

### Scale relationships
Contrast in scale — an oversized numeral beside small annotations, a full-bleed
image followed by a narrow text column — creates rhythm and drama. Establish a
scale ratio between planes (e.g., foreground type ≈ 3× midground) and keep it
consistent.

### Visual pacing
Alternate density and openness across the page: dense data moment → open
breath → intimate detail → wide statement. Pacing applies vertically (section
sequence) and within viewports (spatial distribution). Uniform pacing reads as
a template.

### Section-to-section spatial continuity
Sections should share spatial logic: a background plane that persists across
sections, a horizon line that carries through, objects that travel from one
section into the next. Continuity makes a page feel like one world rather than
ten posters stacked.

---

## Anti-patterns

| Anti-pattern | Why it fails | Instead |
|---|---|---|
| Vertical card stack + parallax bolted on | Parallax decorates structure that has no spatial idea | Define planes and their meaning first |
| Everything floats independently | No anchors = no relationships | Anchor every element to another element or an edge/grid line |
| Random overlaps | Reads as rendering bugs | Every overlap states a relationship |
| Equal spacing everywhere | Rhythm without thought | Deliberate compression and release |
| Multiple parallax systems per page | Competing depths cancel out | One system, several layers |
| Sticky-everything navigation + pinned sections | Scroll feels hijacked | Pin only where the narrative benefits |
| Depth on mobile identical to desktop | Jank and unreadable overlap | Reduce planes/speeds per breakpoint |

---

## Responsive transformation

Spatial composition transforms across breakpoints; it does not merely shrink:

- **Mobile:** reduce to two planes where possible (content / atmosphere),
  lower speed differences, replace hover-revealed depth with tap or
  scroll-triggered equivalents, keep one clear focal point per viewport.
- **Tablet:** intermediate treatment — keep the strongest depth moment,
  simplify the rest.
- **Desktop / large desktop:** full plane system; large screens earn wider
  negative-space sweeps and bigger scale contrasts.

Mobile is intentionally art-directed, not degraded desktop. See
`design/responsive.md`.

---

## Self-check

- Can I name what each plane contains and why?
- Does every overlap express a relationship?
- Is there exactly one focal point per viewport?
- Does the page have pacing (dense/open rhythm), or uniform density?
- Does spatial logic persist from section to section?
- Under reduced motion, does the composition still read (static depth via
  size/overlap/shadow)?
- On mobile, is the composition re-authored rather than squeezed?
