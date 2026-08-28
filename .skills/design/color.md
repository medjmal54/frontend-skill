# Color

Color is a meaning system, not a decoration system. Every color in the product
should be able to answer "what is it for?"

## The color blacklist (never use without explicit justification)

These color choices are the fingerprints of generic AI output. Using them
without a specific, defensible reason tied to the product is a blocking
finding:

- **Purple/blue gradients on white** — the single most common AI-slop pattern.
  Reads as "I asked an AI to make it look modern." Unless the product is
  literally a Linear/Stripe competitor, avoid.
- **Indigo → violet → pink gradients** — the overused "tech startup" gradient.
  No longer reads as modern; reads as derivative.
- **Blue as a default primary** — blue is the most overused brand color on the
  web. Only use it if the product's domain genuinely calls for trust/calm
  (finance, healthcare, government) AND the blue is distinctive (not
  Tailwind's `blue-500`).
- **Gray-on-white everything** — reads as "no color decision was made."
  Restraint is a feature, but "no color" is not restraint — it's avoidance.
- **Tailwind default palette used as-is** — `blue-500`, `purple-600`, etc.
  without modification reads as "I didn't design a palette."

**Why:** These color schemes appear in the vast majority of AI-generated
products. A designer seeing them immediately thinks "generic." The goal is a
product with a palette that feels chosen for this specific product.

## Strategy rules

- **Start from brand and environment, not from "modern".** The palette follows
  the personality chosen in `design/design-direction.md`. If the audience is a
  bank, a loud palette fails before any pixel renders.
- **Restrain the palette, but make it distinctive.** Typically: one primary
  (brand/action), a neutral scale (texts, surfaces, borders), and at most one
  or two accents used for meaning. More than that reads as unedited. But
  "restrained" does not mean "generic" — the primary should feel chosen for
  this product, not defaulted to blue.
- **Make at least one unexpected color choice** that ties to the product's
  identity. An oxblood red for a law firm, a warm amber for a logistics
  dashboard, a deep teal for a healthcare product — choices that a generic
  template would never make.
- **Semantic colors must be distinguishable by more than hue.** Success,
  warning, error, and info states differ in contrast and pairing; never rely on
  hue alone for users with color-vision deficiencies. Always pair color with
  text, shape, or icon.
- **Gradients only where they communicate** (energy, direction, depth, brand
  light). Random gradients to look "modern" are the signature of generic
  output. The purple/blue gradient on white is the most common AI-slop pattern.
- **Dark surfaces are choices too.** If a dark theme ships, it gets its own
  token set and contrast testing — not a naive inversion.

## Token structure

- Name tokens semantically, not cosmetically: `--color-primary`,
  `--color-surface`, `--color-border-subtle`, `--color-text-muted`,
  `--color-status-error` — not `--blue-500`.
- Keep surfaces layered (e.g., surface, surface-raised, overlay) so elevation
  is expressed through tokens.
- Use OKLCH color space for light and dark mode. OKLCH provides better
  perceptual uniformity across hues and makes tinted neutrals and dark mode
  easier to control.
- Tint neutral colors toward the brand hue in both light and dark modes for
  cohesion.
- Avoid pure black (#000) and pure white (#fff) — use off-black and off-white
  for warmth.
- No hardcoded hex values scattered in components. Magic colors are a code
  quality finding (`quality/code-audit.md`).

## Contrast

- WCAG AA is the baseline: 4.5:1 for normal text, 3:1 for large text and UI
  component boundaries.
- Test interactive states too: hover/focus states must still pass, and focus
  indicators must be visible against the surface.
- Light-on-dark pairs need the same rigor as dark-on-light.

## Use

- Use color to guide attention: the single most important element on a view may
  carry the primary color; everything else stays neutral.
- Color carries *status, state, emphasis, and hierarchy* — not decoration.
- If you are adding color and cannot state its job, remove it.
