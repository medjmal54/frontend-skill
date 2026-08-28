# AI Slop Firewall

The comprehensive anti-AI-slop evaluation system. This is not a checklist to
mechanically verify — it is a multi-stage reasoning process. Each stage asks
questions that require judgment, not just pattern matching.

## How to use this

Run every product through all six stages **plus the Originality Firewall**
below before shipping. A failure at any stage requires redesign, not patching.
The stages are ordered from surface detection to deep identity — each one
progressively harder to fake.

---

## Stage 1 — Pattern Detection

Does this design resemble a common AI/SaaS template? Examine each dimension
honestly.

### Visual patterns

**1. The classic AI SaaS recipe** — Does the page follow this sequence?

```
Navbar → Huge centered hero → Subtitle → [Get Started] [Learn More]
→ 3 feature cards → Dashboard screenshot → 3 testimonials
→ Pricing cards → FAQ → CTA
```

Especially when every section is centered and visually symmetrical. This is
the single most common AI-generated landing page structure.

**Fix:** Derive page structure from the user's goals and domain, not from
a conventional SaaS section sequence.

**2. The "everything is a card" disease** — Are features, statistics,
testimonials, pricing, settings, notifications, and users all presented as
cards? When the entire website looks like a collection of rounded rectangles,
cards have not earned their existence.

**Fix:** Prefer hierarchy, whitespace, dividers, typography, lists, timelines,
overlays, editorial compositions, and direct manipulation where cards do not
provide meaningful grouping.

**3. Excessive rounded corners** — Is there one border-radius value applied
globally? When cards, buttons, inputs, modals, images, tables, and sidebars
all share the same radius, geometry has no hierarchy and the result is soft
plastic UI.

**Fix:** Use different treatments intentionally: page elements sharp or
subtle, panels ~8px, interactive controls ~6px, buttons ~6px, images
perhaps 0px, special surfaces ~12px. Geometry must communicate hierarchy
and product personality. Define a radius scale in design tokens.

**4. Purple/blue gradient syndrome** — Is the palette built around #6366f1 +
#8b5cf6 + white background? Does "AI-powered" appear somewhere on the page?
Gradients must have a product-specific rationale. Never use them as a
substitute for visual identity.

**Fix:** Choose color from brand, meaning, and environment. See
`design/color.md`.

**5. Random icons everywhere** — Does every feature get a shield, lightning
bolt, rocket, sparkles, or chart icon merely because a visual area feels
empty? Icons must communicate a specific semantic function. Never add an icon
because a space looks empty. Never use icons to replace meaningful
information.

**Fix:** Use icons only where they carry semantic weight. If an icon doesn't
help the user understand, identify, or act — remove it.

**6. "Icon + heading + paragraph" repeated 6 times** — Is the feature
section composed of 3–6 identical blocks each with an icon, a heading, and a
paragraph describing a vague benefit? This is the card disease's cousin.

**Fix:** Force composition diversity: one large visual, one editorial
section, one interactive demonstration, one comparison, one workflow, one
dense information block. Never repeat the same layout for multiple sections.

**7. Giant hero text** — Is the hero heading 80–120px with "THE FUTURE OF
SOMETHING"? Scale must be proportional to brand personality, viewport,
information density, and product category — not automatically maximized.

**Fix:** Hero scale follows the product's personality. A clinical dashboard
and a creative portfolio need different hero treatments.

**8. "Everything floats"** — Are badges, cards, screenshots, blobs, pills,
avatars, and decorative circles floating independently around the hero? This
is Dribbble concept art syndrome. Real interfaces need relationships and
structure.

**Fix:** Ask: what is physically/visually anchored to what? Every element
should have a spatial relationship to other elements, not float independently.

**9. Excessive glassmorphism** — Is `backdrop-filter: blur(...)` applied
everywhere, especially dark background + glass cards + purple glow? Glass
effects must represent a meaningful layering relationship, not be the default
panel treatment.

**Fix:** Use glass/translucency only where a real layering relationship
exists (overlay panels, modal backdrops, floating toolbars).

**10. Fake depth** — Is `box-shadow: 0 20px 40px rgba(...)` on everything?
When every object appears to float 50px above the page, depth has no
hierarchy.

**Fix:** Use borders, tonal contrast, spacing, typography, and restrained
shadows. Depth should establish hierarchy, not decorate.

**11. Excessive whitespace** — Is the layout afraid of density? When titles
are followed by enormous gaps before a paragraph, then another huge gap
before a button, whitespace is not serving hierarchy — it's filling space.
Especially problematic for dashboards, admin systems, tables, and
data-heavy applications.

**Fix:** Whitespace must reflect hierarchy and reading rhythm, not simply
maximize empty space. Data-dense applications legitimately need density.

**12. Everything is perfectly symmetrical** — Is every section centered with
identical left-right balance? Real design uses asymmetry, offset elements,
varying widths, intentional alignment, editorial rhythm, and visual anchors.

**Fix:** Prefer meaningful asymmetry when it improves hierarchy or reinforces
the product's identity. Do not introduce asymmetry randomly — introduce it
where content demands different treatment.

**13. The "three-column law"** — Are three things always presented in three
columns? Feature A | Feature B | Feature C? Never default to a three-column
grid. Choose the number and arrangement of columns based on content
relationships and viewport constraints.

**Fix:** Vary grid structure per section. Some content is better as two
unequal columns, a single wide block, a staggered grid, or an asymmetric
layout.

**14. Decorative blobs** — Are there huge blurred circles (especially purple
and blue) behind the hero section? Decorative elements must reinforce the
brand concept or spatial composition. Remove decoration that does not
contribute to hierarchy, storytelling, or identity.

**Fix:** If a blob doesn't reinforce the brand or help the composition, it
doesn't exist.

### Motion patterns

**15. Excessive animation** — Does scrolling become a theme park? When
everything fades, slides, scales, rotates, bounces, and staggers — it
screams "Look! AI can make animations!" Not premium design.

**Fix:** Every animation must have a reason: feedback, orientation, state
transition, hierarchy, spatial relationship, or delight. If it has no
purpose, remove it. See `design/motion.md`.

**16. The "landing page trying too hard"** — Text flies in, image rotates,
cards float, gradient follows cursor, background particles move, scroll
triggers 15 animations. This is not premium — it is performative.

**Fix:** Restraint is a feature. Choose 2–3 high-impact motion moments per
page. Let the rest be subtle.

**17. Fake interactivity** — Buttons that don't work, dropdowns that don't
change anything, tabs that don't switch content, search fields that don't
filter, "Export" buttons that do nothing. The UI looks finished but behaves
like a screenshot. This is the biggest vibe-coding tell.

**Fix:** Every visible interactive control must either perform its intended
local/demo behavior or be explicitly marked as unavailable. This is
particularly critical for marketplace templates.

### Copy patterns

**18. AI startup vocabulary** — Does the copy use: Revolutionize, Transform,
Supercharge, Unlock, Seamless, Powerful, Next-generation, Cutting-edge,
Effortless, Streamline, Elevate, Intelligent, Empower, Unleash, "Your
all-in-one platform for..."? That vocabulary immediately feels synthetic.

**Fix:** Write copy from the user's actual workflow and consequences. Prefer
concrete nouns, verbs, quantities, constraints, and domain language over
startup adjectives.

Instead of: "Supercharge your team's productivity with our powerful
AI-powered workflow."

Use: "See which shipments need attention before the next delivery window."

**19. Copy that explains the feature instead of selling the outcome** —
"Advanced analytics dashboard that provides powerful insights into your
business data." vs. "See which tables are slowing tonight's service before
the queue reaches the door." The second one demonstrates understanding.

**Fix:** Every feature description should answer: what decision does this
help the user make? What consequence does it prevent? What workflow does it
accelerate?

**20. Everything is "premium"** — Does the copy repeatedly use premium,
modern, elegant, sleek, powerful, cutting-edge? The more it says it, the
less premium it feels.

**Fix:** Demonstrate quality through decisions; don't describe the product
as premium. Let the design speak.

### Content patterns

**21. Fake metrics** — Are there "10K+ Happy Customers", "99.9% Uptime",
"250% More Productivity", "4.9/5 Customer Rating" with no reason for those
numbers to exist? For fictional products this is especially dangerous.

**Fix:** Never invent impressive statistics, customer counts, testimonials,
logos, awards, ratings, or performance claims unless explicitly provided by
the user. For demos, use application demo data, not fabricated business
claims.

Instead of: "10K+ Happy Customers"
Use: "42 active shipments, 8 requiring review, 3 excursions today"

Those are application demo data, not fabricated business claims.

**22. Generic avatars and names** — JD / John Doe, AB / Alex Brown, SM /
Sarah Miller, Acme Inc., Nova, Lumina, Nexus, Flow, Pulse, Horizon. Every
SaaS template has these. For a demo, use contextually believable people and
data.

**Fix:** Generate domain-specific fictional entities. For a restaurant:
Osteria Lume, Table 14, Dinner Service, Maria — Floor Manager. For cold
chain: SHP-20481, Milan Distribution Center, Temperature Excursion.

**23. Generic dark mode** — Is dark mode just #0f172a background + white
text + #6366f1 accents? Every dashboard becomes the same dark Tailwind
template. Dark mode should have its own design decisions.

**Fix:** Dark mode is a design choice, not an inversion. Define surface
elevation, text contrast, border treatment, and accent behavior specifically
for dark contexts.

### Composition patterns

**24. Mobile = desktop squeezed smaller** — On mobile, is the sidebar +
main + right panel just stacked vertically? That's not responsive design.
On mobile, reconsider hierarchy, interaction model, navigation, density, and
information priority — not merely dimensions.

**Fix:** Mobile is a different context. Navigation may become a bottom bar
or hamburger. Cards may become a scrollable list. Detail views may become
full-screen. The information architecture adapts, not just the widths.

**25. Accessibility added at the end** — Is the design beautiful with
aria-label thrown everywhere as an afterthought? Real accessibility affects
design from the beginning: focus order, contrast, target size, keyboard
navigation, semantic structure, reduced motion, error communication,
screen-reader relationships.

**Fix:** Accessibility is a design constraint from step one, not a fix-up
at the end.

**26. "Design system" that is actually five colors and 12 variables** —
"We created a comprehensive design system" that consists of --primary,
--secondary, --background, --text, --border. A real design system defines
relationships: typography, spacing, density, radius, elevation, color
semantics, motion, interaction states, component patterns, responsive
behavior, content rules.

**Fix:** A design system is a set of relationships and rules, not a set of
variables. Define how tokens relate to each other and when each applies.

**27. Excessive pills** — Are status indicators always pills: Active, New,
Premium, Recommended, Popular? Eventually the UI looks like a bag of tags.

**Fix:** Status should not automatically become a pill. Choose badges,
typography, color, icons, borders, or contextual indicators according to
semantic importance.

**28. Gradient text overuse** — "Build the future" with gradient text.
Gradient text has become extremely associated with AI-generated landing
pages.

**Fix:** Don't ban gradient text absolutely; require justification. Use it
sparingly and only where it reinforces brand identity.

**29. The "everything has a tooltip" problem** — Are tooltips everywhere
compensating for unclear UI? Toolbars are for genuinely supplementary
information, not to explain unclear primary controls.

**Fix:** If a control needs a tooltip to be understood, the control needs
better design, not a tooltip.

---

## Stage 2 — Domain Test

**If I remove the logo and text, can I still identify the intended industry?**

If the design relies entirely on copy to communicate its purpose — if the
visual language, data patterns, interaction models, and information density
could belong to any product — the design has no domain identity.

A hospital UI should naturally contain concepts like patient state, clinical
urgency, vitals, medical records, chronology, alerts.

A restaurant UI should contain service periods, tables, reservations, guests,
staff, menu/service context.

A research UI should contain sources, evidence, citations, claims,
relationships, annotations.

**If you can replace the domain-specific words with "users / projects /
tasks / analytics" and the design still looks identical, it's generic.**

This is the most important anti-slop test. The product-specific visual
vocabulary rule:

> Every product should contain visual concepts, data patterns, and interaction
> models that are native to its domain. If the design could be transplanted
> into any other industry without changing its structure, it has no identity.

**Failure = redesign.** Not add a logo. Not change the copy. Redesign the
information architecture around the domain.

---

## Stage 3 — Component Replacement Test

**Could these components be dropped into another SaaS product without
changing their design?**

If yes, they're probably too generic. Components should feel like they were
designed for this specific product, not pulled from a universal library.

Signs of failure:
- Every card looks like every other card regardless of content
- Navigation could belong to any application
- Forms have no domain-specific input types or validation patterns
- Status indicators use the same pill/badge treatment for everything
- The sidebar could be swapped into a different product without changes

**Components should reflect their content.** A temperature excursion card
in a cold-chain dashboard should look different from a reservation card in a
restaurant app — not just in color, but in structure, density, and
interaction.

---

## Stage 4 — Content Test

**Could this copy belong to 500 other AI-generated websites?**

Read every piece of text on the page. For each:

- Does it contain a specific number, name, location, or constraint?
- Does it describe a concrete action or consequence?
- Does it use domain-specific vocabulary?
- Would this exact sentence appear on a competitor's landing page?

If the answer to all four is "no" or "maybe," rewrite it.

**The copy test:** Remove all adjectives. If the remaining text is empty,
the copy was all fluff.

Before: "Our powerful AI-driven analytics platform provides seamless
insights to supercharge your team's productivity."

After removing adjectives: "Our platform provides insights to your team."

That's nothing. Rewrite from the user's actual workflow.

---

## Stage 5 — Interaction Test

**Does every interaction communicate state, purpose, and consequence?**

For every interactive element on the page:

| Question | If no... |
|---|---|
| Does hovering produce feedback? | Add hover animation |
| Does clicking produce visible result? | Add click feedback or mark unavailable |
| Does the control communicate its current state? | Add state indication |
| Does the user know what will happen before clicking? | Add affordance or label |
| Is there a loading state for async operations? | Add skeleton/spinner |
| Is there an error state for failure? | Add error handling |
| Is there an empty state for no data? | Add empty state with next step |
| Does the interaction animate? | Add transition per Law 1 |

**No dead controls.** Every visible button, toggle, dropdown, tab, and link
must either work in the demo or be explicitly marked as unavailable.

---

## Stage 6 — Composition Test

**Are multiple layout patterns used because the content requires them, or
because the AI knows several layouts?**

If every section uses the same layout pattern (centered text, centered cards,
centered everything), the composition has no rhythm.

If sections use different patterns but those patterns don't relate to
content differences, the variation is random.

**The test:** For each section, can you explain why THIS layout serves THIS
content? If the answer is "because the last section used a different one,"
that's not a reason.

Good composition uses layout variety to:
- Distinguish content types (data vs. narrative vs. action)
- Create visual rhythm (wide/narrow, dense/sparse, dark/light)
- Guide attention (most important content gets the most visual weight)
- Reinforce hierarchy (primary content dominates, secondary supports)

**Never ban cards, grids, gradients, pills, or animations. Prevent default
selection without reasoning.**

---

## The Originality Firewall (reference handling — applies to every product)

The six stages detect genericness. This firewall detects **derivative
identity** — work that is technically competent but traceably copied. It runs
on every product and is especially critical for high-craft/immersive work
(`workflows/create-high-craft.md`).

### Forbidden

The factory must NEVER:

- Clone an existing website.
- Reconstruct a specific website from screenshots.
- Imitate a specific designer's recognizable personal style as an identity.
- Reproduce a specific award-winning website (Awwwards/FWA/etc.) or a known
  marketplace composition.
- Copy a specific component arrangement, layout system, animation sequence,
  or design system from a reference site.
- Reproduce proprietary/copyrighted visual identities (logos, brand marks,
  signature palettes of real brands).
- Copy source code, prompts, text, or assets from third parties.

Requests shaped like these are refused and re-scoped:

> "Make this look exactly like 21st.dev."
> "Clone this [gallery] page."
> "Recreate this Awwwards winner."
> "Copy this component exactly."
> "Use the same design as [specific site]."

### Allowed: abstracting principles, never identity

When users provide references (screenshots, links, mood boards), extract
**general design principles and techniques** only:

- Allowed abstractions: scroll-driven storytelling, kinetic typography,
  shader backgrounds, spatial compositions, cinematic transitions, magnetic
  interactions, 3D object presentation, depth layering, image reveal
  techniques, morphing transitions, editorial layouts, experimental navigation,
  pacing strategies, typographic contrast systems.
- Forbidden abstraction: "Make it look like Site X."

Record what was extracted in the Originality Rationale (see the high-craft
workflow) so the transformation is explicit.

### The mental model

> **Learn the technique, invent the identity.**

References may influence the vocabulary of techniques. They may never shape
the identity of the resulting product — its palette behavior, typography
system, composition logic, motion personality, copy voice, and motif must be
derived from THIS product's concept, audience, and art direction
(`design/art-direction.md`).

### Detection questions (ask during audit)

- Could someone familiar with the reference identify it in this work?
- Is any section structurally a reconstruction of the reference's arrangement?
- Did we borrow a signature device (specific cursor, specific transition,
  specific grid trick) that functions as the reference's identity?
- If the reference vanished tomorrow, would this design still be fully
  justified by its own brief?

Any "yes" on the first three = redesign trigger.

---

## The full rule set (reference)

When a specific pattern is detected during Stage 1, refer to this list for
the targeted response. These rules are **investigation triggers**, not
automatic failures. Each rule asks: "Is this pattern here because it serves
the product, or because it was the easiest option?" If you can articulate a
product-specific justification, the pattern is allowed. If you can't, redesign.

### Rule 1: Page structure must derive from user goals

Do not use a conventional SaaS section sequence unless the product
genuinely requires it. Derive page structure from the user's goals and
domain. **Justified when:** the product's domain genuinely maps to that
sequence (e.g., a SaaS pricing page legitimately needs pricing tiers).

### Rule 2: Cards must earn their existence

Prefer hierarchy, whitespace, dividers, typography, lists, timelines,
overlays, editorial compositions, and direct manipulation where cards do
not provide meaningful grouping.

### Rule 3: Geometry must communicate hierarchy

Do not apply one border-radius value globally. Different element types
receive different geometric treatments based on their role and relationship.

### Rule 4: Gradients require product-specific rationale

Never use gradients as a substitute for visual identity. If gradients are
used, they must have a product-specific rationale tied to brand or meaning.

### Rule 5: Copy must be concrete and domain-specific

Write from the user's actual workflow and consequences. Prefer concrete
nouns, verbs, quantities, constraints, and domain language over startup
adjectives.

### Rule 6: Never fabricate business metrics

Never invent impressive statistics, customer counts, testimonials, logos,
awards, ratings, or performance claims unless explicitly provided by the
user. For demos, use application demo data, not fabricated business claims.

### Rule 7: Icons communicate semantic function

Never add an icon merely because a visual area feels empty. Never use icons
to replace meaningful information.

### Rule 8: Force composition diversity

Never repeat the same "icon + heading + paragraph" layout for multiple
sections. Use varied information architectures: one large visual, one
editorial section, one interactive demonstration, one comparison, one
workflow, one dense information block.

### Rule 9: Hero scale follows brand personality

Hero typography scale must be proportional to brand personality, viewport,
information density, and product category — not automatically maximized.

### Rule 10: Elements need spatial relationships

Do not let everything float independently. Every element should have a
clear spatial relationship to other elements and structural anchors.

### Rule 11: Glass effects represent layering

Use glassmorphism only where a real layering relationship exists. Never as
the default panel treatment. **Justified when:** the element floats over
scrolling content (fixed nav, sticky toolbar, modal backdrop) where the
blur communicates "this is above that."

### Rule 12: Depth establishes hierarchy

Use borders, tonal contrast, spacing, typography, and restrained shadows.
Depth should establish hierarchy, not decorate.

### Rule 13: Whitespace reflects reading rhythm

Whitespace must reflect hierarchy and reading rhythm. Data-dense
applications legitimately need density.

### Rule 14: Asymmetry serves hierarchy

Prefer meaningful asymmetry when it improves hierarchy or reinforces the
product's identity. Do not introduce asymmetry randomly.

### Rule 15: Grid count follows content

Never default to a three-column grid. Choose columns based on content
relationships and viewport constraints.

### Rule 16: Charts answer questions

Every visualization must answer an identifiable user question. Do not add
charts merely to make a dashboard appear sophisticated.

### Rule 17: Every control must function or be marked unavailable

Every visible interactive control must either perform its intended
local/demo behavior or be explicitly marked as unavailable.

### Rule 18: Tooltips supplement, not explain

Use tooltips for genuinely supplementary information, not to explain
unclear primary controls.

### Rule 19: Status indicators match semantic importance

Choose badges, typography, color, icons, borders, or contextual indicators
according to semantic importance. Status should not automatically become a
pill.

### Rule 20: Dark mode has its own design decisions

Dark mode is a design choice, not an inversion. Define surface elevation,
text contrast, border treatment, and accent behavior for dark contexts.

### Rule 21: Mobile reconsiders hierarchy

On mobile, reconsider hierarchy, interaction model, navigation, density,
and information priority — not merely dimensions.

### Rule 22: Accessibility is a design constraint

Accessibility affects design from the beginning: focus order, contrast,
target size, keyboard navigation, semantic structure, reduced motion, error
communication, screen-reader relationships.

### Rule 23: Design systems define relationships

A real design system defines relationships: typography, spacing, density,
radius, elevation, color semantics, motion, interaction states, component
patterns, responsive behavior, content rules.

### Rule 24: Animations must have purpose

Every animation must serve one of: feedback, orientation, state transition,
hierarchy, spatial relationship, or delight. If it has no purpose, remove it.

### Rule 25: Domain-specific fictional entities

Generate contextually believable people, places, and data for demos. Never
use John Doe, Acme Inc., or random alphabet soup.

### Rule 26: Demonstrate quality, don't describe it

Let design decisions communicate quality. Never label the product as
premium, modern, elegant, sleek, or cutting-edge in copy.

### Rule 27: Product-specific visual vocabulary

Every product should contain visual concepts, data patterns, and interaction
models that are native to its domain. If the design could be transplanted
into any other industry, it has no identity.

### Rule 28: Gradient text requires justification

Gradient text is strongly associated with AI-generated pages. Use it
sparingly and only where it reinforces brand identity. **Justified when:**
the gradient is part of the product's logo/brand system and appears
consistently across all brand touchpoints, not just the hero.

### Rule 29: No decorative blobs without purpose

Decorative elements must reinforce the brand concept or spatial composition.
Remove decoration that does not contribute to hierarchy, storytelling, or
identity.

### Rule 30: No global border-radius

Define a radius scale: panels ~8px, controls ~6px, buttons ~6px, images
perhaps 0px, special surfaces ~12px. Geometry communicates hierarchy.

### Rule 31: Layout variety serves content

Use layout diversity to distinguish content types, create visual rhythm,
guide attention, and reinforce hierarchy — not because the AI knows
multiple layouts.

### Rule 32: No fabricated trust signals

Never invent "Trusted by" claims, customer logos, awards, or partnership
badges unless explicitly provided by the user.

### Rule 33: No AI startup vocabulary in copy

Avoid: Revolutionize, Transform, Supercharge, Unlock, Seamless, Powerful,
Next-generation, Cutting-edge, Effortless, Streamline, Elevate, Intelligent,
Empower, Unleash, "Your all-in-one platform for..." — write from the user's
actual workflow instead.
