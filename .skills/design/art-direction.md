# Art Direction

Establish an art direction before implementation — a coherent set of visual
decisions specific enough that the product could be recognized from its
appearance alone, without seeing its source code or name. Art direction is the
difference between "styled" and "authored."

This file is the vocabulary. The commitment is recorded in the direction brief
(`design/design-direction.md`); the personality selection is made from
`design/design-diversity.md`.

---

## What art direction must define

Answer all of these before writing code:

| Dimension | Question to answer |
|---|---|
| Visual concept | What is the ONE idea the visuals express? (one sentence) |
| Typography strategy | Which families, at what contrast, doing what job? |
| Color strategy | What palette, what temperature, what behavior over time? |
| Imagery strategy | Photography / illustration / video / 3D / generative — and treatment |
| Shape language | What geometry recurs (sharp planes, circles, arcs, grids)? |
| Texture language | Grain, paper, metal, glass, fabric, pixels — or deliberate smoothness |
| Lighting language | Where does light come from? Flat, soft, hard, rim, emissive? |
| Depth language | Planes, overlap rules, blur policy (`design/spatial-composition.md`) |
| Composition strategy | Centered / asymmetric / editorial / modular / full-bleed / split |
| Visual rhythm | Dense↔open alternation, section-to-section pacing |
| Motion personality | How does this product move? (mechanical, organic, snappy, cinematic, minimal) |

The coherence test: pick any two visual decisions on the page. A stranger
should be able to explain both from the same single concept. If the gradient
hero, the mono labels, and the rounded cards each seem to come from different
products, there is no art direction yet.

---

## Typography dimensions

Vocabulary options (choose deliberately; see `design/typography.md` for
families and blacklists):

- **Display vs body contrast** — extreme scale jumps (display 6–10× body)
  read as editorial confidence; narrow ranges read as utilitarian.
- **Serif/sans contrast** — serif display + sans body (heritage, editorial),
  inverse pairing (technical warmth), or single-family weight systems.
- **Variable typography** — one variable font animated across weight/width/
  optical-size axes gives expressive range with one file.
- **Oversized type** — type as image: viewport-scaled statements that compose
  with media rather than caption it.
- **Kinetic type** — type that moves (mask reveals, scroll-linked weight,
  elastic letters). Belongs to the motion grammar (`design/motion-system.md`);
  one kinetic moment per page beats five.
- **Editorial hierarchy** — kickers, standfirsts, drop caps, folios, ruled
  columns; structure borrowed from print craft.
- **Condensed/wide type** — condensed for density and urgency, extended for
  luxury and presence.
- **Typographic texture** — treating type masses (columns of small caps,
  tabular data, index lists) as visual texture in composition.

---

## Composition dimensions

- **Centered** — formal, ceremonial; powerful when rare, generic when default.
- **Asymmetric** — energy, hierarchy, modernity (`design/spatial-composition.md`).
- **Editorial** — columns, baselines, captions; content-forward credibility.
- **Modular** — visible grid units; system-like precision.
- **Spatial** — composed depth planes instead of flat stacking.
- **Full-bleed** — media edge-to-edge; immersion and scale.
- **Split-screen** — two worlds compared or paired; dialogue compositions.
- **Overlapping** — elements crop each other; physicality and layering.
- **Unconventional grid** — broken/intentionally misaligned grids; risk as
  identity. Requires strong consistency elsewhere to avoid reading as sloppy.
- **Deliberately constrained** — a strict narrow system held rigorously;
  restraint as signature.

---

## Visual material options

These are vocabulary choices, NOT mandatory ingredients. A product may use one
or two deeply rather than all shallowly.

| Material | Character | Watch out for |
|---|---|---|
| Photography | immediate reality, emotion | cliché stock poses; needs consistent treatment (grade/crop/mask) |
| Illustration | authored voice, abstraction | style must be singular; mixed illustration styles = noise |
| Video | time, motion, proof | autoplay cost; always poster + reduced-motion static frame |
| 3D | objecthood, spatial storytelling | only via `design/3d-guidelines.md` decision gate |
| Generative imagery | uniqueness per load, systems feel | must serve concept; performance cost is real |
| Texture | materiality, warmth, grit | one texture family; opacity low enough to stay behind content |
| Gradients | atmosphere, light behavior | banned defaults (`design/color.md`); requires product-specific rationale |
| Noise/grain | analog warmth, filmic quality | has become a trend tell; use only if the material story calls for it |
| Geometric forms | structural clarity, brand shapes | forms should recur from logo/shape language, not decorate randomly |
| Procedural visuals | living systems, technical credibility | budget cost (`design/motion-budget.md`) |

---

## Forbidden generic combinations

The following combos are pre-rejected regardless of execution quality — they
are the fingerprints of generated design:

- Purple/blue gradient + white floating cards
- Giant centered SaaS hero (heading + paragraph + two buttons)
- Random glassmorphism (blur panels without a layering relationship)
- Floating decorative blobs
- Excessive uniformly-rounded cards everywhere
- Arbitrary glow effects unconnected to a lighting language
- Decorative 3D objects with no conceptual purpose

See `design/anti-generic.md` and `design/ai-slop-firewall.md` for the full
detection systems.

---

## Process

1. Write the visual concept sentence first. Everything below must serve it.
2. Choose typography, color, composition from the dimensions above — driven by
   the personality selected in `design/design-diversity.md`.
3. Define the recurring visual motif (shape, texture, lighting, or typographic
   device) that will repeat across sections — the signature.
4. Decide what the product deliberately does NOT use. Restraint decisions are
   part of the direction ("no photography — the data renders are the imagery").
5. Record everything in the direction brief. Implementation may not deviate.

> **One strong idea is better than twelve decorative effects.** Every technique
> must earn its place. Use fewer techniques with stronger conceptual
> coherence.
