# Spacing and Grid

Spacing is the invisible skeleton of a product. Inconsistent spacing is the
fastest giveaway of low-quality output.

## Spacing philosophy

- **One scale, used consistently.** Build a spacing scale (typically 4px-based:
  `4 / 8 / 12 / 16 / 24 / 32 / 48 / 64 / 96`) as tokens. Snap spacing values to
  the scale rather than inventing new ones per component.
- **Density is a product decision.** Comfortable spacing for general
  audiences; tight, high-density spacing for professional/B2B tools where
  information volume is high. Choose per audience and apply consistently.
- **Whitespace is a design tool.** It creates hierarchy, separates ideas, and
  gives the eye rest. Generous space around a key element is prominence; don't
  fill every gap.
- **Rhythm, not identical padding.** Sections use a deliberate vertical rhythm
  (consistent section spacing, tighter internal spacing) rather than uniform
  padding on everything.

## Grid philosophy

- **Define the grid** in the design direction: container width (fluid with a
  max, e.g., `1120–1440px`), column count (typically 12), gutters, and vertical
  rhythm.
- **Align to the grid**; misalignment within a view reads as carelessness.
- **Break the grid deliberately, once.** An intentional offset or full-bleed
  moment is powerful; accidental misalignment is not.
- **Component-level grids** (card grids, feature rows) use the same column
  logic so everything feels like one system.

## Asymmetric composition (Bento grids)

When using grids for feature sections, pricing, or highlights:

- **Composition, not symmetry.** Use CSS Grid with intentional areas: one
  dominant cell, mix large/medium/compact cells, no empty cells.
- **Grid areas over generic cells.** Define `grid-template-areas` with named
  regions so the layout is explicit, not emergent from repetition.
- **Preserve hierarchy on mobile.** The composition should reflow logically,
  not collapse into a vertical stack that loses emphasis.
- **One visual anchor per section.** The dominant cell is the reading entry
  point; everything else supports it.
- **Content count matches grid cells.** Never leave empty cells or add filler.
- The result feels **premium, editorial, intentionally composed** — not
  assembled.

## Card and surface discipline

- Not every block needs to be a card. Alternate surfaces, borders, and plain
  layouts (`design/anti-generic.md`).
- When cards are used, their internal padding, corner radius, and border come
  from tokens — identical treatment across the system.
- Avoid "every section is three equal cards". Vary the information
  architecture while keeping the system consistent.

## Rules

- No magic spacing values outside the scale.
- Consistent horizontal alignment across columns and components.
- Vertical rhythm consistent between sections of the same rank.
- Density chosen for the audience and applied everywhere.
