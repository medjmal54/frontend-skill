# Design Direction

How to establish the coherent design direction required before any code.

## Why this exists

Design decisions without reasons produce generic products. The direction below
forces each decision to be made deliberately, in context, and to be defensible.

## Process

Work through these in order. Each step constrains the next.

0. **Interface mode** — Is this a brand-first interface (marketing, storytelling,
   expressive) or a product-first interface (efficiency, clarity, utilitarian)?
   This question shapes every design choice that follows. A landing page is
   brand-first; an admin dashboard is product-first. Both are valid; they are
   not better or worse — they are *different*.
   - **Brand-first:** Expressive typography, bolder color, motion for delight,
     composition can be asymmetric, decoration is intentional.
   - **Product-first:** Restrained typography, subtle color, motion for feedback,
     composition is predictable, decoration is avoided.
   - **High-craft extension:** When the product demands an art-directed,
     immersive, or motion-driven experience (`workflows/create-high-craft.md`),
     brand-first intensifies into a full experience direction: spatial model,
     motion grammar, 3D decision, performance and reduced-motion strategies
     become first-class brief fields (see the extended brief fields below).
     High-craft is a commitment to coherence, not to effects.
1. **Design concept** — one or two sentences capturing the idea of the product
   in design terms (not feature terms). Example: "A high-density operations
   console where calm typography and ruled grids communicate precision, and
   data is the decoration."
2. **Visual personality** — the character of the product in 3–5 words (from
   `design/design-diversity.md`): e.g. technical, restrained, exacting;
   warm, editorial, human; industrial, blunt, confident. Everything else
   follows from this.
3. **Typography strategy** — one or two families chosen for the personality
   and content density. See `design/typography.md`.
4. **Color strategy** — a restrained palette chosen for meaning and
   environment, not decoration. See `design/color.md`.
5. **Spacing philosophy** — the rhythm of the product: comfortable vs dense,
   the spacing scale, how whitespace is used. See `design/spacing.md`.
6. **Grid philosophy** — columns, gutters, container width, and how strictly
   the grid is followed. See `design/spacing.md`.
7. **Shape language** — radius and shape decisions and why (sharp = exacting,
   soft = approachable), applied consistently.
8. **Border strategy** — when borders carry structure (rules, separators,
   tables) versus when they are avoided. Borders should carry meaning.
9. **Elevation strategy** — a small, purposeful set of shadows or surface
   layers; elevation marks *hierarchy and layering*, never decoration.
10. **Component philosophy** — how components are composed: primitives,
    composites, state conventions, naming.
11. **Interaction philosophy** — what interactions exist and what behavior
    rules they follow (predictable, keyboard/touch-operable, with feedback).
12. **Motion philosophy** — what motion is for and what it never does. See
    `design/motion.md` for recipes and `design/motion-system.md` for the
    authoritative intensity scale: Level 0 (static), 1 (micro-interaction),
    2 (expressive), 3 (choreographed), 4 (immersive), 5 (experimental).
    Choose the lowest level achieving the experience; record it in the brief.
13. **Imagery philosophy** — how images are used and treated:
    - Photography, illustration, icons, or gradients?
    - Image treatments: overlays, clip-path reveals, parallax, Ken Burns?
    - Placeholder strategy for templates (unsplash/pexels, not empty boxes)
    - Every section must have visual content — no empty colored backgrounds
14. **Technology stack** — framework and CSS approach:
    - Component packs → Plain HTML + CSS + JS (framework-agnostic)
    - Static sites / templates / landing pages → React (Next.js or Vite)
    - UI kits / dashboards → React (Next.js or Vite)
    - CSS approach: vanilla CSS with tokens, Tailwind, or CSS modules
15. **Responsive philosophy** — how layouts restructure, not shrink. See
    `design/responsive.md`.
16. **Accessibility philosophy** — a11y as a design constraint from the start,
    not a fix-up. See `design/accessibility.md`.

## Rules

- **No arbitrary values.** Every type size, color, radius, shadow, spacing
  choice has a stated reason tied to the concept or to usability.
- **Consistency over cleverness.** The design system is what makes many parts
  feel like one product.
- **Restraint is a feature.** Decide what is intentionally minimal and what is
  intentionally prominent. Not everything can be prominent.
- **The same category must be able to produce different outcomes.** A landing
  page kit for a law firm and one for a game studio share no automatic style.
- **Make at least one bold, unexpected choice.** The product must feel
  tailored to this exact project — not like a template that could belong to
  anyone. See `design/anti-generic.md` for the cookie-cutter anti-pattern.
- **No blacklisted fonts or colors.** See `design/typography.md` and
  `design/color.md` for the blacklists. Using them without explicit
  justification is a blocking finding.

## OpenCode & Taste Briefing Protocol

Before coding, every project brief must define its OpenCode context and **three taste dials** (Scale 1–10). This establishes the structural envelope before any HTML/CSS/JS is outputted.

- **`DESIGN_VARIANCE` (1–10)**: Controls layout risk. Lower scales (1-4) enforce standard vertical-stack grids; higher scales (7-10) require asymmetric, layered, and grid-breaking layouts.
- **`MOTION_INTENSITY` (1–10)**: Controls transition complexity. Lower scales (1-4) restrict to simple hover/active classes; higher scales (7-10) deploy spring curves and staggered multi-stage enter sequences.
- **`VISUAL_DENSITY` (1–10)**: Controls spatial rhythm. Lower scales (1-4) expand whitespace for luxury/editorial feels; higher scales (7-10) condense sizing for data-rich dashboards.

## One-shot prompts (when the user gives a single sentence)

When the user provides a brief prompt like "Build me a cold-chain monitoring
dashboard" without specifying design preferences, the agent should:

1. **Identify the domain** from the prompt.
2. **Look up the domain defaults** below.
3. **Fill the direction brief** using those defaults — no questions asked.
4. **Implement** using the defaults as the design direction.
5. **Note the defaults used** in the output so the user can override any
   decision.

The user can always override any default. The agent should present the
completed brief in one line before coding: "Using cold-chain defaults:
industrial/restrained, JetBrains Mono + IBM Plex Sans, slate/amber palette,
density 8/10. Proceeding."

If the domain doesn't match any entry below, the agent makes confident
decisions based on the product type (dashboard → product-first, landing
page → brand-first) and the user's prompt context. Never stall asking for
design direction on simple prompts — decide and state what you decided.

## Domain design defaults

Pre-filled direction briefs for common domains. These are starting points,
not cages. Override any value the user's prompt contradicts.

### Cold chain / Logistics / Supply chain

```
Mode:         product-first
Concept:      A high-density operations console where calm typography and
              ruled grids communicate precision, and temperature data is
              the primary visual language.
Personality:  industrial, restrained, exacting, data-rich, trustworthy
Dials:        DESIGN_VARIANCE=3 | MOTION_INTENSITY=2 | VISUAL_DENSITY=8
Typography:   JetBrains Mono (data/IDs) + IBM Plex Sans (UI/body)
Color:        slate-900 surfaces, amber/orange for alerts, cool-gray
              neutrals, green for compliant, red for excursion
Spacing:      dense, 4px base scale, tight card padding
Grid:         12-column, 16px gutter, full-bleed data panels
Shape:        sharp corners (0–2px), no rounded cards
Borders:      1px rules everywhere — data is structured by lines
Elevation:    flat — borders and tonal contrast, no shadows
Motion:       Level 1 — instant feedback, no delight animation
Data:         Shipments, sensors, incidents, temperature telemetry,
              event timelines, threshold breaches
Imagery:      product UI screenshots, sensor visualizations, maps
```

### Restaurant / Hospitality / Food service

```
Mode:         brand-first
Concept:      A warm, editorial interface where rich photography and
              generous typography make the operational tool feel like
              part of the dining experience.
Personality:  warm, editorial, human, inviting, precise
Dials:        DESIGN_VARIANCE=5 | MOTION_INTENSITY=3 | VISUAL_DENSITY=5
Typography:   Playfair Display (headings) + DM Sans (body)
Color:        warm cream/ivory surfaces, deep burgundy accents,
              warm grays, gold for active/highlight
Spacing:      comfortable, 8px base, generous section breathing
Grid:         12-column, 24px gutter, asymmetric layouts welcome
Shape:        4–6px on cards, 4px on buttons, 0px on images
Borders:      selective — dividers between sections, not on every card
Elevation:    minimal — one shadow level for overlays only
Motion:       Level 2 — warm entrances, smooth transitions
Data:         Reservations, tables, guests, staff, service periods,
              menu items, orders, wait times
Imagery:      food photography, restaurant interiors, ambient textures
```

### Healthcare / Clinical

```
Mode:         product-first
Concept:      A calm, information-dense clinical interface where
              whitespace and typography communicate trustworthiness,
              and patient state is always visible.
Personality:  precise, calm, trustworthy, clinical, clean
Dials:        DESIGN_VARIANCE=2 | MOTION_INTENSITY=1 | VISUAL_DENSITY=7
Typography:   Source Serif 4 (headings) + Source Sans 3 (body)
Color:        white/light-gray surfaces, teal for primary, warm-red
              for critical alerts, muted blue-gray for secondary
Spacing:      structured, 4px base, clinical density
Grid:         12-column, strict alignment, sidebar + main
Shape:        4px max — clinical means sharp
Borders:      structural — section dividers, form field outlines
Elevation:    none — flat surfaces only
Motion:       Level 1 — feedback only, no animation for delight
Data:         Patients, vitals, records, medications, appointments,
              lab results, alerts, chronology
Imagery:      medical illustrations (not photos), iconography for vitals
```

### Research / Academic / Evidence

```
Mode:         product-first
Concept:      A scholarly interface where citation density and evidence
              relationships are the visual structure, and typography
              communicates authority.
Personality:  scholarly, methodical, evidence-focused, dense, precise
Dials:        DESIGN_VARIANCE=3 | MOTION_INTENSITY=2 | VISUAL_DENSITY=8
Typography:   Literata (body/text) + IBM Plex Mono (citations/IDs)
Color:        off-white/cream surfaces, deep navy for text, muted
              sage-green for evidence strength, warm-red for conflicts
Spacing:      dense academic, 4px base, tight line-height for text
Grid:         12-column, sidebar + main, citation margins
Shape:        0–2px — academic means serious
Borders:      structural — citation blocks, evidence containers
Elevation:    none — typographic hierarchy only
Motion:       Level 1 — text transitions, link hover feedback
Data:         Sources, claims, evidence, citations, annotations,
              relationships, confidence levels, extraction results
Imagery:      diagrams, charts, data visualizations, no decorative photos
```

### Finance / Fintech

```
Mode:         product-first
Concept:      A sharp, authoritative interface where data density
              communicates competence and every number has context.
Personality:  sharp, authoritative, precise, data-rich, confident
Dials:        DESIGN_VARIANCE=3 | MOTION_INTENSITY=2 | VISUAL_DENSITY=8
Typography:   IBM Plex Sans (UI) + IBM Plex Mono (numbers/data)
Color:        near-black surfaces, white text, green for positive,
              red for negative, blue for neutral primary
Spacing:      dense, 4px base, information-packed panels
Grid:         12-column, 16px gutter, data-dense layouts
Shape:        0–2px — finance means exact
Borders:      1px rules for data separation, table-like structure
Elevation:    flat — tonal contrast only
Motion:       Level 1 — number transitions, chart animations
Data:         Transactions, portfolios, balances, trends, forecasts,
              risk metrics, compliance status
Imagery:      charts, sparklines, data visualizations — numbers ARE the imagery
```

### E-commerce / Product catalog

```
Mode:         brand-first
Concept:      A vibrant, product-focused interface where photography
              dominates and the shopping experience feels curated.
Personality:  vibrant, curated, product-focused, conversion-aware, clean
Dials:        DESIGN_VARIANCE=5 | MOTION_INTENSITY=3 | VISUAL_DENSITY=5
Typography:   Outfit (headings) + Inter Tight (body) — or pick from
              design/typography.md, NOT default Inter
Color:        white surfaces, product photography provides color,
              accent color from brand, warm neutrals
Spacing:      comfortable, 8px base, product cards breathe
Grid:         responsive product grid, 2–4 columns, masonry optional
Shape:        8px on product cards, 6px on buttons, 0px on images
Borders:      minimal — product images are the structure
Elevation:    subtle — card hover lift, overlay shadows
Motion:       Level 2 — product hover reveals, cart animations
Data:         Products, categories, prices, inventory, reviews,
              carts, orders, wishlists
Imagery:      product photography IS the design — hero images, zoom,
              galleries, lifestyle shots
```

### SaaS / Admin dashboard

```
Mode:         product-first
Concept:      A clean, efficient interface where task completion speed
              matters more than visual drama.
Personality:  clean, efficient, task-focused, unobtrusive, reliable
Dials:        DESIGN_VARIANCE=3 | MOTION_INTENSITY=2 | VISUAL_DENSITY=6
Typography:   Satoshi (headings) + General Sans (body) — or pick from
              design/typography.md
Color:        neutral surfaces (not pure white), one distinctive
              primary, semantic colors for status
Spacing:      moderate, 8px base, comfortable density
Grid:         12-column, top navbar, card palette + slide-over
Shape:        6–8px on cards, 6px on buttons, functional radius
Borders:      subtle — surface separation, not decoration
Elevation:    two levels — surface + overlay
Motion:       Level 1 — feedback, transitions, no spectacle
Data:         whatever the product manages — users, projects, tasks,
              settings, notifications
Imagery:      product UI is the imagery — no decorative photos needed
```

### Portfolio / Creative showcase

```
Mode:         brand-first
Concept:      An expressive, asymmetric interface where the design itself
              demonstrates capability.
Personality:  expressive, bold, asymmetric, memorable, confident
Dials:        DESIGN_VARIANCE=8 | MOTION_INTENSITY=5 | VISUAL_DENSITY=4
Typography:   one distinctive display face + one clean body face
Color:        high-contrast, bold palette — the brand IS the color
Spacing:      generous, 8–12px base, editorial breathing room
Grid:         broken grid — offset elements, varying widths, intentional
Shape:        0px on images, variable on containers — geometry is expression
Borders:      decorative where intentional, absent elsewhere
Elevation:    layered — overlapping elements create depth
Motion:       Level 3 — scroll reveals, text masks, image transitions
Data:         projects, case studies, skills, contact
Imagery:      portfolio work IS the design — full-bleed, high-impact
```

### High-craft / immersive experience (creative agency, premium brand, launch)

```
Mode:         brand-first (high-craft extension)
Concept:      An authored spatial world where one visual idea — carried by
              typography, depth, and a coherent motion grammar — makes the
              brand recognizable without its logo.
Personality:  art-directed, cinematic, intentional, rhythmic, specific
Dials:        DESIGN_VARIANCE=8 | MOTION_INTENSITY=7 | VISUAL_DENSITY=4
Experience:   per workflows/create-high-craft.md (Phases A–I)
Typography:   one concept-strong display family + quiet workhorse body
Color:        concept-driven palette; behavior over time (scroll/cursor
              shifts) defined, not accidental
Spacing:      editorial rhythm — deliberate compression and release
Grid:         broken or unconventional grid held together by strict rules
Shape:        shape language derived from the brand motif
Borders:      only where structure demands
Elevation:    replaced by spatial planes (design/spatial-composition.md)
Motion:       Level 3–5 per design/motion-system.md + written motion budget
3D:           default NO; decision via design/3d-guidelines.md gate
Data:         narrative content, proof points, showcase items
Imagery:      treatment-defined (grade/crop/mask); material serves concept
Fallbacks:    base experience + progressive layers (progressive-enhancement.md)
```

## The direction brief

Internal format (fill it out before coding; write it down when the product is
large or the user asked for reviewable decisions):

```
Mode:         <brand-first or product-first>
Concept:      <one to two sentences>
Personality:  <3–5 words>
Dials:        <DESIGN_VARIANCE (1-10) | MOTION_INTENSITY (1-10) | VISUAL_DENSITY (1-10)>
Typography:   <families + rationale>
Color:        <palette + meaning + semantic roles>
Spacing:      <density + scale + rhythm rules>
Grid:         <columns, gutter, container, alignment>
Shape:        <radius strategy>
Borders:      <where they carry structure>
Elevation:    <layer model>
Motion:       <purpose, durations, reduced-motion; intensity level 0–5 per design/motion-system.md>
Data:         <entities, API ops, domain workflows, mock mode — if applicable>
Responsive:   <transformation rules>
Accessibility:<AA baseline, keyboard, reduced motion>
OpenCode:     <RTCF path + framework targets>
```

### Optional high-craft fields

Add these lines when the product is high-craft/immersive — or whenever useful.
Blank values are intelligently inferred from the project; never force the user
to fill out a configuration form.

```text
Experience Direction: [auto | product-first | brand-first | high-craft | immersive | experimental]
Motion Intensity:     [auto | 0-5]           ← canonical scale in design/motion-system.md
Spatial Depth:        [auto | flat | layered | spatial | immersive]
3D:                   [auto | prohibited | optional | encouraged | required]
Performance Priority: [auto | standard | high | extreme]
Reduced Motion:       required                ← always required, never optional
Visual Reference:     [principles only — never clone a specific site]
```

Rules for these fields:

- `auto` (or blank) means infer from Phases A–I of `workflows/create-high-craft.md`
  and the domain defaults above.
- `Motion Intensity` uses the 0–5 scale from `design/motion-system.md`; at 3+,
  attach a motion budget line (`design/motion-budget.md`).
- `Visual Reference` accepts principles and techniques ONLY ("scroll-driven
  storytelling", "kinetic editorial type"). Requests shaped like "make it look
  like [site]" are refused and re-scoped per the Originality Firewall
  (`design/ai-slop-firewall.md`).
- `Reduced Motion` has no "off" value. It is a constant.
