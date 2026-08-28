# Name-to-Design Inference

How to derive a complete design direction from a project name alone.

## Why this exists

Users rarely specify design preferences. They say "build me Fieldnote" or
"create a Vault dashboard" and expect the result to feel right. The project
name carries semantic weight — word roots, associations, connotations — that
maps directly to visual decisions. This system extracts that weight and
converts it into a direction brief.

## When to use this

- The user gives a project name without specifying design direction
- The domain defaults in `design/design-direction.md` don't exactly match
- The name is evocative enough to carry design intent (most are)

## Process

### Step 1: Decompose the name

Break the name into semantic components.

| Pattern | Example | Decomposition |
|---|---|---|
| **Compound word** | Fieldnote | field + note |
| **Compound word** | Greenhouse | green + house |
| **Compound word** | Vaultkey | vault + key |
| **Single word** | Pulse | pulse |
| **Single word** | Atlas | atlas |
| **Single word** | Drift | drift |
| **Abstract/invented** | Zephyr | zephyr (west wind) |
| **Abstract/invented** | Kairo | kairos (decisive moment) |
| **Descriptive** | FastShip | fast + ship |
| **Descriptive** | CleanFlow | clean + flow |

### Step 2: Map each component to visual qualities

Use the word-association tables below. Each word maps to a cluster of
visual properties: temperature (warm/cool/neutral), weight (heavy/light),
texture (rough/smooth/glass/metal), motion (still/flowing/pulsing/staccato),
and personality keywords.

### Step 3: Synthesize

Combine the visual qualities from each component into a coherent direction.
When components conflict (e.g., "fire" + "ice"), one typically dominates —
usually the first component or the more emotionally resonant one.

### Step 4: Fill the direction brief

Map the synthesized qualities to the standard direction brief fields:
Mode, Concept, Personality, Dials, Typography, Color, Spacing, Grid,
Shape, Borders, Elevation, Motion, Data, Imagery.

---

## Word-Association Tables

### Nature / Earth

| Word | Temperature | Weight | Texture | Motion | Personality | Color direction | Typography direction |
|---|---|---|---|---|---|---|---|
| field | neutral-warm | medium | rough, organic | still, wind-swept | grounded, honest, open | earth tones, olive, warm gray | sturdy sans-serif |
| forest | cool | heavy | dense, layered | still, rustling | deep, complex, mysterious | deep green, dark brown | serif or slab |
| river | cool | light | smooth, flowing | flowing, constant | adaptive, persistent | blue-green, slate blue | fluid, rounded |
| ocean | cool | heavy | deep, vast | rolling, powerful | vast, calm, profound | navy, teal, deep blue | wide tracking |
| stone | neutral | heavy | rough, solid | still, permanent | solid, enduring, reliable | gray, charcoal, slate | slab serif, bold |
| mountain | cool-neutral | very heavy | rough, massive | still, immovable | authoritative, towering | slate, granite, snow white | heavy weight |
| garden | warm | light | soft, organic | gentle, growing | nurturing, alive, curated | greens, soft pink, cream | humanist sans |
| garden | warm | light | soft, organic | gentle, growing | nurturing, alive, curated | greens, soft pink, cream | humanist sans |
| meadow | warm | light | soft, airy | gentle | peaceful, open, natural | soft green, gold, sky blue | light weight |
| sand | warm | light | granular, soft | shifting, drifting | warm, patient, vast | beige, gold, terracotta | rounded sans |
| fire | hot | light-medium | flickering, bright | flickering, dancing | intense, alive, dangerous | red, orange, ember glow | bold, condensed |
| ice | cold | medium | smooth, sharp | still, crystalline | precise, fragile, pure | cyan, white, pale blue | thin, geometric |
| wind | cool | light | invisible, felt | fast, unpredictable | free, dynamic, unseen | silver, sky blue, transparent | italic, light weight |
| rain | cool | light | wet, soft | falling, constant | refreshing, melancholic | blue-gray, silver | clean sans |

### Materials / Objects

| Word | Temperature | Weight | Texture | Motion | Personality | Color direction | Typography direction |
|---|---|---|---|---|---|---|---|
| vault | cool | very heavy | metal, stone | still, locked | secure, impenetrable, secret | dark, black, gold accent | heavy, geometric |
| forge | hot | heavy | metal, fire | rhythmic, powerful | industrial, creative, raw | orange, charcoal, steel | bold slab serif |
| steel | cool | heavy | smooth, cold | still, rigid | strong, precise, modern | silver, chrome, blue-gray | geometric sans |
| glass | cool-neutral | light | transparent, smooth | still, reflective | clear, fragile, modern | transparent, white, pale | thin, light weight |
| wood | warm | medium | rough, grain | still, warm | natural, honest, crafted | brown, amber, cream | slab, humanist |
| stone | neutral | heavy | rough, solid | still, permanent | solid, enduring, reliable | gray, charcoal, slate | slab serif, bold |
| crystal | cool | light | faceted, clear | shimmering | precise, valuable, rare | prismatic, cool palette | thin, geometric |
| iron | cool | heavy | rough, dense | still, unyielding | industrial, strong, blunt | dark gray, rust, black | heavy, condensed |
| paper | warm | light | thin, foldable | fluttering | delicate, tangible, honest | cream, white, soft shadow | serif, light |
| ink | neutral | light | fluid, spreading | flowing | expressive, permanent, bold | black, deep blue, sepia | calligraphic or mono |
| thread | warm | light | thin, woven | flowing, connecting | connected, delicate, precise | warm neutrals, accent color | light,细 |
| brass | warm | medium | smooth, warm metal | still, gleaming | classic, warm, valuable | gold, bronze, warm yellow | classic serif |
| copper | warm | medium | smooth, patina | aging, changing | warm, evolving, authentic | copper, patina green, brown | organic sans |
| concrete | neutral | heavy | rough, flat | still, permanent | industrial, urban, honest | gray, warm gray | monospace, bold |
| marble | cool-neutral | heavy | smooth, veined | still, luxurious | elegant, cool, timeless | white, gray veins, gold | thin serif |

### Actions / Concepts

| Word | Temperature | Weight | Texture | Motion | Personality | Color direction | Typography direction |
|---|---|---|---|---|---|---|---|
| pulse | warm | light | — | rhythmic, alive | alive, dynamic, vital | red, pink, warm accent | bold, modern |
| drift | cool-neutral | light | smooth | slow, wandering | relaxed, free, ambient | muted, desaturated, cool | light, italic |
| beacon | warm | light | luminous | steady, guiding | clear, trustworthy, visible | warm white, gold, amber | bold, clear |
| shelter | warm | medium | soft, enclosing | still, protective | safe, caring, reliable | warm neutrals, soft green | rounded, humanist |
| bloom | warm | light | soft, organic | opening, growing | alive, fresh, emerging | pink, green, warm palette | organic, rounded |
| spark | hot | light | bright, brief | flashing, sudden | energetic, creative, brief | orange, yellow, white | bold, italic |
| echo | cool | light | — | repeating, fading | resonant, deep, layered | muted, layered blues | medium weight |
| orbit | cool | medium | smooth, circular | circular, constant | systematic, connected, cosmic | deep blue, white, accent | geometric |
| anchor | cool-neutral | heavy | metal, rope | still, holding | stable, reliable, grounded | navy, rust, cream | heavy, slab |
| compass | neutral | light-medium | metal, glass | pointing, steady | directional, precise, reliable | green, brass, white | geometric, mono |
| signal | neutral | light | — | flashing, transmitting | clear, urgent, communicative | red, green, amber (signal colors) | bold, clear |
| bridge | neutral | heavy | steel, concrete | still, connecting | structural, spanning, reliable | steel gray, blue, rust | geometric, strong |
| lantern | warm | light | glass, metal | flickering, warm | warm, guiding, intimate | amber, warm white, brass | serif, warm |
| crystal | cool | light | faceted, clear | shimmering | precise, valuable, rare | prismatic, cool palette | thin, geometric |
| anchor | cool-neutral | heavy | metal, rope | still, holding | stable, reliable, grounded | navy, rust, cream | heavy, slab |
| ledger | neutral | medium | paper, ink | still, recorded | precise, historical, trustworthy | cream, black, red accent | monospace, serif |
| forge | hot | heavy | metal, fire | rhythmic, powerful | industrial, creative, raw | orange, charcoal, steel | bold slab serif |
| prism | cool | light | faceted | refracting | analytical, revealing, colorful | spectrum, prismatic | geometric, clean |
| relay | neutral | light | — | passing, connecting | sequential, connected, fast | blue, green, neutral | modern sans |
| gauge | neutral | medium | metal, glass | measuring, steady | precise, technical, reliable | silver, red, green zones | monospace |
| ledger | neutral | medium | paper, ink | still, recorded | precise, historical, trustworthy | cream, black, red accent | monospace, serif |
| terminal | cool | medium | screen, metal | static, blinking | technical, direct, no-nonsense | green-on-black, amber-on-black | monospace |
| baseline | neutral | medium | — | still, foundational | essential, minimal, reference | neutral, one accent | clean sans |

### Environments / Spaces

| Word | Temperature | Weight | Texture | Motion | Personality | Color direction | Typography direction |
|---|---|---|---|---|---|---|---|
| harbor | cool-neutral | heavy | water, stone | gentle waves | safe, protective, calm | blue, slate, warm accent | sturdy, calm |
| lattice | neutral | light-medium | geometric, open | still, patterned | structured, interconnected | black/white, one accent | geometric, precise |
| canopy | warm | medium | organic, sheltering | still, overhead | sheltering, natural, layered | green, brown, sky | organic, rounded |
| passage | neutral | medium | stone, wood | linear, directional | transitional, connecting | neutral, warm accent | clean, directional |
| summit | cool-neutral | heavy | rock, snow | still, elevated | elevated, achievement, clarity | white, gray, blue | clean, bold |
| shore | warm | medium | sand, water | rhythmic, tidal | boundary, transition, calm | sand, blue, seafoam | relaxed, organic |
| gallery | neutral | light | white walls, light | still, curated |展示, clean, focused | white, black, one accent | elegant, varied |
| workshop | warm | medium | wood, tools | active, busy | productive, hands-on, practical | warm neutrals, tool colors | utilitarian sans |
| laboratory | cool | medium | glass, metal | precise, controlled | exact, clinical, rigorous | white, blue, green accent | monospace, precise |
| corridor | neutral | medium | linear | directional | transitional, connecting | neutral, cool | clean, geometric |
| terrace | warm | light | open, layered | still, breezy | elevated, open, social | warm, sky, green | light, open |

### Qualities / Adjectives

| Word | Temperature | Weight | Texture | Motion | Personality | Color direction | Typography direction |
|---|---|---|---|---|---|---|---|
| swift | cool | light | smooth | fast, direct | fast, efficient, modern | blue, silver | italic, light |
| steady | neutral | medium | solid | constant, reliable | reliable, calm, consistent | neutral, one stable accent | regular weight |
| bright | warm | light | luminous | glowing | optimistic, clear, visible | warm whites, yellow, gold | light, open |
| sharp | cool | light | precise, cutting | sudden, exact | exact, modern, bold | black, white, red accent | condensed, bold |
| soft | warm | light | gentle, yielding | slow, gentle | approachable, human, calm | pastels, muted tones | rounded, light |
| bold | neutral | heavy | — | strong, present | confident, unmissable | high contrast, saturated | heavy, display |
| quiet | cool-neutral | light | smooth | still, minimal | subtle, refined, understated | muted, desaturated | light, thin |
| rapid | hot | light | — | fast, urgent | urgent, energetic, dynamic | red, orange, bright | italic, condensed |
| deep | cool | heavy | dense | slow, profound | complex, layered, serious | dark, saturated, rich | heavy, serif |
| clear | cool | light | transparent | still, open | transparent, obvious, pure | white, pale, minimal | light, open |
| raw | neutral | medium | rough, unfinished | — | honest, unpolished, authentic | natural, brown, gray | slab, rough |
| refined | cool-neutral | light | smooth, polished | — | precise, elegant, controlled | neutral, one jewel tone | thin, geometric |
| ancient | warm | heavy | weathered, textured | still, timeless | historical, wise, enduring | sepia, gold, dark brown | serif, classic |
| modern | cool | light | smooth, clean | dynamic | current, clean, forward | neutral, one bold accent | geometric sans |
| minimal | neutral | light | smooth, empty | still, quiet | reduced, essential, focused | near-white, one accent | thin, light |
| vivid | hot | light | saturated | energetic | alive, bold, unforgettable | saturated, high contrast | bold, varied |

### Domains / Industries

| Word | Temperature | Weight | Texture | Motion | Personality | Color direction | Typography direction |
|---|---|---|---|---|---|---|---|
| medical | cool | medium | clean, smooth | still, precise | clinical, trustworthy, clean | white, teal, blue | serif headings, clean body |
| legal | neutral | medium | paper, leather | still, formal | authoritative, traditional, serious | navy, burgundy, cream | classic serif |
| tech | cool | light | glass, metal | dynamic, digital | modern, innovative, fast | blue, purple, dark | geometric sans |
| finance | cool | heavy | metal, marble | still, stable | trustworthy, precise, serious | navy, green, gold | serif + mono |
| food | warm | medium | organic, textured | — | appetizing, warm, inviting | red, orange, cream | rounded, warm |
| fashion | cool-neutral | light | fabric, texture | fluid, seasonal | expressive, curated, aesthetic | black, white, one accent | display, elegant |
| education | warm | light | paper, board | — | accessible, clear, encouraging | blue, green, warm | humanist, clear |
| travel | warm | medium | — | moving, expansive | adventurous, discovery, open | sky blue, sunset, earth | varied, expressive |
| energy | hot | medium | — | powerful, dynamic | powerful, essential, urgent | orange, yellow, dark | bold, heavy |
| agriculture | warm | medium | earth, organic | seasonal, slow | grounded, natural, practical | green, brown, gold | slab, practical |

---

## Compound Name Logic

For compound names, the **first component sets the base** and the
**second component modifies or specifies**.

| Pattern | Example | Base (first) | Modifier (second) | Result |
|---|---|---|---|---|
| nature + object | Fieldnote | grounded, honest | documentation, precision | industrial, exacting |
| nature + object | Greenhouse | alive, organic | shelter, structure | warm, nurturing, enclosed |
| quality + noun | FastShip | speed, efficiency | logistics, movement | dynamic, operational |
| quality + noun | CleanFlow | purity, clarity | movement, fluidity | smooth, minimal, precise |
| action + noun | ForgeBase | creation, power | foundation, stability | industrial, strong, grounded |
| object + object | VaultKey | security, solidity | access, precision | sharp, secure, minimal |
| abstract + noun | PulseBoard | alive, rhythmic | display, control | energetic, data-rich |
| adjective + noun | BrightPath | luminous, clear | direction, guidance | optimistic, clear, guiding |

When the second component is a common product type (board, note, hub, lab,
forge, vault, etc.), it also hints at the **product category**:
- board → dashboard, kanban, monitoring
- note → documentation, recording, logging
- hub → central dashboard, aggregation
- lab → experimentation, testing, analysis
- forge → creation, building, manufacturing
- vault → security, storage, encrypted data
- pulse → real-time monitoring, health, vital signs
- atlas → mapping, geographic, comprehensive overview
- ledger → financial, recording, historical
- relay → sequential, pipeline, workflow

---

## Single-Word Name Analysis

For single-word names, the word's primary meaning drives the design, and
its secondary connotations add nuance.

### Examples

**Pulse**
- Primary: heartbeat, rhythm, vital sign
- Secondary: alive, dynamic, medical, monitoring
- → product-first, alive, rhythmic, data-rich
- → red/pink accents on dark, monospace data, pulse-like animations
- → typography: geometric sans + mono for data

**Atlas**
- Primary: world map, comprehensive reference
- Secondary: vast, structural, cartographic, mythological
- → product-first or brand-first depending on type
- → deep blue, earth tones, expansive layouts
- → typography: wide tracking, display weight

**Drift**
- Primary: slow movement, wandering
- Secondary: relaxed, ambient, snow (drifting), code (drift)
- → brand-first, relaxed, ambient
- → muted palette, slow transitions, floating elements
- → typography: light weight, italic

**Ember**
- Primary: glowing coal, residual fire
- Secondary: warm, intimate, fading, dangerous
- → brand-first, warm, intimate
- → orange/red glow on dark, warm gradients, subtle glow animations
- → typography: serif or rounded sans

**Keystone**
- Primary: central stone in arch, essential element
- Secondary: foundational, structural, organizational
- → product-first, structural, foundational
- → neutral palette, strong grid, architectural shapes
- → typography: slab serif, heavy weight

**Harbor**
- Primary: sheltered port, safe anchorage
- Secondary: safe, protective, maritime, calm
- → product-first, calm, protective
- → blue/slate palette, calm water-like surfaces
- → typography: rounded, sturdy sans

**Terminal**
- Primary: endpoint, command line, transport hub
- Secondary: technical, direct, final, no-nonsense
- → product-first, technical, blunt
- → dark background, green/amber text, monospace everything
- → typography: monospace only

---

## Inference Rules

1. **Temperature wins over domain.** If the name is warm but the domain is
   typically cool (e.g., "WarmVault" in finance), follow the name. The name
   is the user's intent.

2. **First component dominates.** In compound names, the first word sets 60%
   of the direction, the second word adjusts 40%.

3. **Concrete beats abstract.** If the name has both concrete ("stone") and
   abstract ("swift") components, the concrete word sets the visual foundation
   and the abstract word sets the motion/interaction style.

4. **Conflict resolution.** When components suggest contradictory directions
   (e.g., "FireIce"), pick the dominant emotion. "FireIce" → fire is active,
   ice is passive → active wins → warm/hot with cool accents.

5. **Don't over-index on one word.** "Greenhouse" is not necessarily green.
   The word suggests warmth, shelter, organic growth — the color green is
   one option, not a mandate.

6. **Product type constrains.** Even if the name suggests brand-first
   expressiveness, a dashboard/product is always product-first. The name
   influences the *flavor* of product-first, not the mode.

7. **When the name is meaningless** (e.g., "Zephyr", "Kairo"), treat it as
   an abstract name and use its phonetic qualities: hard consonants (k, t, d)
   → sharp/geometric; soft sounds (m, n, l, s) → rounded/organic; vowel-heavy
   → open/spacious.

---

## Quick Reference: Common Product Suffixes

| Suffix | Implies | Default mode | Layout pattern |
|---|---|---|---|
| board | Dashboard, kanban, monitoring | product-first | Card palette or pipeline |
| hub | Central aggregation, control | product-first | Metric dashboard |
| lab | Experimentation, testing | product-first | Card palette + data viz |
| forge | Creation, manufacturing | product-first | Rich list + forms |
| vault | Security, storage | product-first | Master-detail |
| pulse | Real-time, vital signs | product-first | Metric dashboard |
| note | Documentation, logging | product-first | Rich list |
| flow | Workflow, pipeline | product-first | Pipeline/kanban |
| base | Foundation, platform | product-first | Card palette |
| link | Connection, API | product-first | Master-detail |
| view | Display, visualization | depends on content | Varies |
| space | Collaborative, workspace | product-first | Card palette |
| desk | Task management | product-first | Rich list |
| panel | Admin, control | product-first | Sidebar + main |
| ops | Operations, monitoring | product-first | Metric dashboard |

---

## Worked Examples

### "Fieldnote"
- Decompose: field (grounded, honest, outdoor, industrial) + note
  (documentation, precision, recording)
- Synthesis: An industrial documentation tool. Grounded, honest, precise.
  The field gives earth tones and ruggedness; the note gives structure
  and monospace precision.
- → product-first, industrial/exacting, JetBrains Mono + IBM Plex Sans,
  concrete/amber palette, density 8, Level 1 motion
- Matches: cold-chain/logistics defaults (closest domain match)

### "GreenVault"
- Decompose: green (alive, organic, natural) + vault (secure, impenetrable,
  dark)
- Synthesis: Secure but alive. Not a sterile vault — a living one. Dark
  surfaces with organic green accents. Security meets nature.
- → product-first, secure/organic, geometric sans + mono, dark with green
  accents, density 7, Level 1 motion
- Does NOT match any domain default → use name inference

### "PulseBoard"
- Decompose: pulse (alive, rhythmic, vital signs) + board (dashboard,
  monitoring, display)
- Synthesis: A living dashboard. Real-time data that feels alive. Red/pink
  accents, pulse-like animations, dark background for contrast.
- → product-first, alive/rhythmic, geometric sans + mono, dark with warm
  accents, density 7, Level 1 motion with rhythmic micro-animations

### "Drift"
- Decompose: single word — slow movement, wandering, ambient
- Synthesis: Relaxed, ambient interface. Not rushed. Muted colors, slow
  transitions, floating elements. Could be brand-first if it's a creative
  tool, product-first if it's a monitoring tool.
- → depends on product type, but always: muted palette, light typography,
  slow motion, generous spacing

### "Keystone"
- Decompose: keystone (central stone, essential element, foundation)
- Synthesis: Foundational, structural. Strong grid, architectural shapes,
  neutral palette with one structural accent color. The design itself
  communicates solidity.
- → product-first, structural/foundational, slab serif or heavy geometric,
  neutral palette, dense grid, Level 1 motion
