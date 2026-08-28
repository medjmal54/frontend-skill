# Anti-Generic Design

The guard against the fingerprints of low-quality AI/vibe-coded interfaces —
"AI slop." When you catch yourself producing one of these, stop and redesign —
do not ship it and do not just note it in a review.

## The three killers of good design

### 1. Static UI = Dead UI

If the interface doesn't move, it doesn't breathe. Animation is not decoration
— it's feedback, hierarchy, and soul. A product where nothing animates on
hover, where clicks produce no visual response, where lists pop in all at once,
where modals just appear and disappear — that product is incomplete.

**The rule:** Every interaction must have a corresponding animation. See
`design/motion.md` for the full checklist and CSS recipes. If you can't find
an animation for an interaction, that interaction is broken.

### 2. Tables = Visual Death

HTML tables and table-like grid layouts for data browsing are banned. Tables
are a wall of text with no hierarchy, no visual interest, no scannability.
They are the #1 sign of a generic, low-effort interface.

**The rule:** Use card palettes, pipeline views, rich lists, or metric
dashboards. See SKILL.md Laws for the five data display patterns. Cards are
interactive, visual, animated, and scannable. Tables are none of those.

### 3. Cookie-Cutter Layouts = No Identity

The single most common failure of AI-generated products is a layout that could
belong to any company, any industry, any audience — therefore belongs to none.

**The rule:** Make bold, unexpected choices that feel tailored to this exact
project. The final result should feel unique, memorable, and impossible to
confuse with a generic template.

### 4. Empty Imagery = No Soul

A product with no real imagery — just colored boxes, gradient backgrounds,
and icon placeholders — is visually dead. Images tell the product's story.
They create emotional connection, establish context, and make the product
feel real. Empty colored rectangles are the #1 sign of a product that
was generated, not designed.

**The rule:** Every product must use real imagery. Hero sections need photos
or illustrations. Sections need supporting visuals. Use unsplash.photos or
pexels.com for placeholder images in templates. Image treatments (overlays,
masks, parallax, reveals) add depth. No empty boxes. See `design/motion.md`
for image reveal animations.

### 5. Dashboards Without Charts = Not a Dashboard

A dashboard with only metric cards and no data visualization is a spreadsheet
with better CSS. Cards without sparklines are data-light. Numbers without
trend lines are context-free. A dashboard's value is in making data visual
and scannable.

**The rule:** Every dashboard MUST include at least one chart type (line, bar,
donut, area) plus sparklines on metric cards. Charts must animate on load.
SVG-based preferred (no heavy charting library dependency). See `design/motion.md`
Section 10 for chart animation patterns.

## The AI-slop blacklist (investigate, don't auto-fail)

These are fingerprints of generic AI output. They are **red flags that require
investigation**, not automatic failures. The same pattern can be lazy default
or intentional choice — context determines which.

**The rule:** When you see a blacklisted pattern, ask: "Is this here because
it's the path of least resistance, or because it serves this product?" If the
answer is "path of least resistance," redesign. If there's a defensible reason
tied to the product's domain, audience, or constraints, **document the
justification and move on.**

Justification must be specific, not generic:
- "Inter because it's clean" → NOT a justification (that's every font)
- "Inter because this is a component library sold to agencies who need
  neutral defaults that won't clash with their clients' brands" → VALID
- "Purple gradient because it looks modern" → NOT a justification
- "Purple gradient because the product is a creative studio tool and purple
  signals creativity in our audience's mental model" → VALID
- "Centered hero because it's easy" → NOT a justification
- "Centered hero because this is a single-purpose CTA page where the only
  goal is one click, and centering maximizes focal attention" → VALID

### Overused fonts (investigate — requires justification)
- **Inter** — the default "modern" sans. Often signals "I didn't choose."
  **Justified when:** component libraries (neutral default), utilities where
  performance matters, products targeting developers who expect system fonts.
- **Roboto** — the Android/system default. Usually no personality.
  **Justified when:** Android-native apps, Material Design ecosystem.
- **Arial** — the fallback of last resort. Almost never a design choice.
  **Justified when:** email templates (limited font support), accessibility-
  first tools where rendering reliability > personality.
- **Space Grotesk** — the "I want to look techy" default. Overused.
  **Justified when:** developer tools where the audience expects monospace-
  adjacent aesthetics, and the product has other identity signals.
- **System font stacks as a primary choice** — legitimate for utilities
  where performance is the priority, but never as a shortcut to avoid
  choosing a typeface.

**Instead:** Choose typefaces with character that match the product's
personality. See `design/typography.md` and `design/design-diversity.md`.

### Generic color schemes (investigate — requires justification)
- **Purple/blue gradients on white** — the single most common AI-slop pattern.
  **Justified when:** the product's domain genuinely calls for trust/calm
  (fintech, healthcare) AND the gradient is distinctive (not the default
  indigo-to-violet).
- **Indigo to violet to pink gradients** — the Linear/Stripe derivative.
  **Justified when:** building a product in the dev-tools space where this
  palette has become a genre convention, AND the product has other strong
  identity signals (typography, layout, copy).
- **Blue as a default primary** — blue is the most overused brand color.
  **Justified when:** the product's domain genuinely calls for trust/calm
  AND the blue is distinctive (not the default Tailwind blue).
- **Gray-on-white everything** — reads as "no color decision was made."
  **Justified when:** the product is a dense data tool where color would
  add noise (spreadsheets, code editors, terminal UIs).

**Instead:** Choose color from brand, meaning, and environment.
See `design/color.md`.

### Banned layouts (investigate — requires justification)
- **Centered hero with stacked heading + paragraph + two buttons** — the
  lowest-effort opening.
  **Justified when:** single-purpose CTA page, product launch page where
  one action is the only goal, or the product's identity is intentionally
  minimal/zen.
- **Standard 3-column card grids** — the lowest-effort feature section.
  **Justified when:** the content genuinely has 3 equal-weight items
  (pricing tiers, plan comparison) AND the cards have different treatments.
- **Sidebar + topbar + card wall dashboards** — the unexamined admin default.
  **Justified when:** the product IS an admin tool and the user base expects
  this pattern (enterprise SaaS, internal tools).
- **Every section using the same card treatment** — one pattern everywhere.
  NOT justified. Force composition diversity.
- **Identical section spacing everywhere** — rhythm without thought.
  NOT justified. Spacing must reflect hierarchy.
- **Full-page tables for data browsing** — the laziest data display.
  **Justified when:** the data IS tabular (financial ledger, audit log,
  changelog) AND the table has inline actions, sorting, and visual hierarchy.

**Instead:** Vary the information architecture. Give each section a structure
that serves its specific content. See the pattern table below.

### Banned data display (investigate — requires justification)
- **HTML tables for browsing/comparing records** — visually dead, no
  hierarchy, no scannability.
  **Justified when:** the data is genuinely tabular AND the table has
  inline actions, row hover states, sorting, and visual hierarchy.
- **Table-like CSS grid layouts** — same problem, different markup.
  Same justification rules as HTML tables.
- **Raw number cells** — metrics deserve cards with sparklines, not grid cells.
  **Justified when:** the numbers are part of a dense data view where
  sparklines would add visual noise (spreadsheet, ledger).
- **Boring pagination** — card-based infinite scroll or load-more with
  animation, or use virtual scroll for large datasets.
- **Dense spreadsheets** — if it looks like Excel, it's not designed.
  **Justified when:** the product IS a spreadsheet or data editor.

**Instead:** Use the five data display patterns from SKILL.md:
Card Palette, Master-Detail with Slide-Over, Pipeline/Kanban,
Rich List with Inline Actions, Metric Dashboard.

### Banned content (investigate — requires justification)
- **Lorem ipsum** — use realistic demo content. NOT justified.
- **"Feature 1 / Feature 2"** — write specific, meaningful copy. NOT justified.
- **Fake testimonials** — never invent people's words. NOT justified.
- **Fake metrics** — use clearly framed demo data or omit.
  **Justified when:** the metrics are clearly labeled as demo/example data
  and realistic for the product's domain.
- **Fake logos** — never invent "Trusted by" claims. NOT justified.
- **"Trusted by 10,000+ companies"** — fabricated trust. NOT justified.

### Banned imagery (investigate — requires justification)
- **Empty colored boxes as backgrounds** — use real photos or illustrations.
  **Justified when:** the product is a design tool where the colored boxes
  ARE the content (color picker, palette generator, theme builder).
- **Gradient-only backgrounds with no visual content** — gradients support
  imagery, not replace it.
  **Justified when:** the product's identity is intentionally abstract
  (creative tool, music app) and the gradient IS the visual content.
- **Icon-only sections with no photos** — icons are accents, not imagery.
  **Justified when:** the product is a utility where imagery would distract
  (developer tools, CLI wrappers, config managers).
- **Placeholder rectangles labeled "image here"** — use unsplash/pexels
  placeholders. NOT justified.
- **Products with zero visual content** — every product needs imagery to
  feel real.
  **Justified when:** the product is a text-only tool (markdown editor,
  terminal, API client) where imagery would be incongruous.

**Placeholder image licensing (Unsplash + Pexels):** Both platforms allow
commercial use in digital templates without attribution. Images must be part
of a larger creative work (the UI), not the standalone product being sold.
Do not use for physical prints. Images with identifiable people may need
model releases. Neither platform provides indemnification. For marketplace
products, document the source and advise buyers to replace with their own
assets before production use. See SKILL.md parallax section for full
licensing details.

### Banned dashboard patterns (investigate — requires justification)
- **Metric cards without sparklines** — numbers need trend context.
  **Justified when:** the metric is a single-point value (license key,
  version number) where a trend line would be meaningless.
- **Dashboards without any chart or graph** — data must be visualized.
  **Justified when:** the "dashboard" is actually a status overview
  (server health, uptime monitor) where indicators replace charts.
- **Raw number grids** — use metric cards with visual indicators.
  **Justified when:** the grid is part of a dense data tool where
  visual indicators would add noise.
- **Data tables for browsing** — use card palette, kanban, or rich list.
  **Justified when:** the data is genuinely tabular (financial ledger,
  audit log) AND the table has inline actions, sorting, and hierarchy.

### Banned interactions (investigate — requires justification)
- **Static hover states** — if hovering doesn't animate, it's dead.
  **Justified when:** the element is a read-only display where hover
  animation would be distracting (dense data cell, label).
- **No click feedback** — if clicking doesn't produce a visual response,
  the interaction is broken. NOT justified for interactive elements.
- **Instant state changes** — if a toggle, tab, or panel just flips
  without transition, the UI has no soul.
  **Justified when:** the state change is a binary visibility toggle
  (show/hide password) where animation would slow frequent use.
- **Modals/drawers that just appear** — everything must animate open
  and closed.
  **Justified when:** the modal is a system alert where instant
  appearance communicates urgency.
- **Lists that pop in all at once** — staggered entrance is mandatory.
  NOT justified for user-facing content.
- **transition: all** — never. Use specific properties. NOT justified.

## The generic-AI patterns (and the fix)

| Pattern | Why it reads as generic | Fix |
|---|---|---|
| Generic SaaS hero: giant centered heading, one-line paragraph, two buttons | zero information, pure formula | Give the opening a product-specific layout: real product UI, an editorial lede, a data summary, an asymmetric composition |
| Purple/blue gradient everywhere | unexamined "modern" default | Choose color for meaning and brand, not gradient's sake |
| Inter + huge heading + centered paragraph + two buttons | the default stack | Pick type for the personality; vary the hierarchy |
| Random glassmorphism | decoration without purpose | Use translucency only where layering is real |
| Excessive rounded cards | everything soft, nothing decided | Radius is a designed scale |
| Excessive shadows | elevation used as decoration | Small elevation system: shadows mark layering |
| Repetitive 3-column cards | the lowest-effort grid | Vary information architecture per section |
| Generic dashboard: KPI cards, bar chart, table | the formula dashboard | Design around the real task; use card palette, not tables |
| Generic sidebar + navbar + cards | unexamined admin default | Top navbar + card palette + slide-over detail |
| Fake testimonials / logos / metrics | fabricated trust | Real framing or omit entirely |
| Static interface with no animation | dead UI, no soul | Every interaction must animate. See motion.md |
| Tables for data browsing | visually dead, no hierarchy | Card palette, pipeline, rich list, or metric dashboard |
| All sections same card treatment | one pattern everywhere | Different information architectures with consistent system |
| AI copy that says nothing | filler prose | Specific, useful copy or realistic demo framing |
| Unnecessary animations | motion as proof of AI | Motion must serve hierarchy, feedback, transitions |
| Generic stock illustrations | borrowed cliches | Real imagery placeholders, data viz, or purposeful graphics |
| Skeleton that instantly swaps to content | no loading transition | Shimmer skeleton that resolves with crossfade |
| Toast that just appears | no notification animation | Slide in from edge, auto-dismiss with slide out |
| Empty colored boxes as backgrounds | no visual life | Real photos, illustrations, or purposeful imagery |
| Gradient-only hero with no imagery | empty visual space | Photo, illustration, or product UI in hero |
| Dashboard without charts or graphs | data not visualized | At least one chart type + sparklines on metrics |
| Metric cards without sparklines | no trend context | Sparkline showing trend data on every KPI card |
| Sparse sections with huge gaps | wasted viewport, no density | Fill every section with value: data, imagery, animation, interaction |
| Hero with only title + button + empty space | zero information, wasted 80vh | Fill hero with imagery, ambient motion, supporting data, visual texture |
| Component that takes up space without filling it | sparse = looks unfinished | Every component earns its height with content or visual treatment |
| Section with one line of text and massive padding | padding is not design | Content density reflects purpose; fill space with value |

## The self-check (ask before every milestone)

- Would a professional designer be comfortable putting their name on this?
- Is anything here because "it's what a template does"? Or because it
  serves this specific product?
- Can I articulate WHY each blacklisted pattern is justified for THIS product?
- Does every decorative element relate to the product?
- Is the layout the lowest-effort version, or does it serve the content?
- If I stripped the styling, does the information still make sense?
- Could a designer identify this product's industry/audience from the
  design alone, without reading the copy?
- Does at least one design choice surprise me in a good way?
- Would this be confused with a generic template in a thumbnail test?
- Does every hover animate? Does every click produce feedback?
- Are data displayed using the right pattern for their type?
- Is there a top navbar with navigation and user avatar for app UIs?
- Does every section have real imagery (not just colored boxes)?
- If this is a dashboard, does it have charts/graphs and sparklines?
- If this is a landing page, does it use scroll reveals and text animations?
- Is every section dense with value — not sparse with empty space?
- Does the hero fill its viewport with purpose, not just a title and button?
- Would a buyer feel impressed seeing this from a one-sentence prompt?
- Are advanced motion concepts used where they serve a purpose?
- Does every component earn its height, or is some space wasted?

## The rule

Investigate, then decide. Blacklisted patterns are red flags, not death
sentences. The same pattern can be lazy default or intentional choice —
the difference is whether you can articulate WHY it serves THIS product.
If you can justify it, use it. If you can't, redesign. Never use a
blacklisted pattern because it was the easiest option. Always use it
because it was the right one.

## Further reading

- `design/ai-slop-firewall.md` — The comprehensive 33-rule anti-AI-slop
  evaluation system with six-stage detection process. Run every product
  through all six stages before shipping.
- `design/data-architecture.md` — How to design frontend products around
  real data contracts instead of decorative content. Covers API boundaries,
  CRUD workflows, mock API mode, and domain-specific state machines.
- `design/impressive-motion.md` — Advanced animation concepts (marquees,
  3D rotation, scale effects, text reveals, magnetic effects, scroll-linked
  animations) that make products feel crafted, not generated.
