# Design Diversity

There is no universal default style. Choose a visual language deliberately,
from the product's audience, purpose, industry, content, brand personality,
usability, and commercial positioning.

## The languages

| Language | Character | Typography lean | Color lean | Shape/feel | Best for |
|---|---|---|---|---|---|
| Editorial | confident, structured, story-led | strong serif or high-contrast sans, generous sizes | ink-on-paper, one accent | generous whitespace, few rules | magazines, publishing, essays, media brands |
| Swiss / International | precise, objective, grid-true | grotesque sans, tight hierarchy, tabular figures | black/white + one red | hard edges, strict grid, no decoration | corporate, design studios, institutional |
| Brutalist | raw, honest, structural | heavy monospace or grotesque, uppercase | near-monochrome, harsh contrast | exposed structure, minimal rounding | developer tools, studios, counter-culture brands |
| Neo-brutalist | playful, bold, flat | chunky sans, strong weights | hard accent blocks on cream/off-white | hard shadows, thick borders | young brands, indie products, agencies |
| Minimal luxury | quiet, expensive, spacious | refined serif + restrained sans | warm neutrals, one deep accent | gentle radius, generous space, few shadows | fashion, premium products, private services |
| Corporate | clean, trustworthy, orderly | professional sans, standard hierarchy | corporate blues/grays done well | moderate radius, restrained elevation | enterprise, finance, consulting |
| Technical | engineered, legible, dense | humanist sans + monospace for code/data | cool grays, one signal color | small radius, thin borders, tabular numbers | dev tools, data products, APIs, docs |
| Industrial | rugged, material, functional | condensed sans, stenciled/serial tones | metal/earth/amber | square corners, heavy borders | machinery, logistics, hardware |
| Futuristic | sleek, forward, synthetic | geometric sans, wide tracking | dark + neon accents, glassy surfaces (used deliberately) | rounded or angular per concept, glow accents | tech, robotics, entertainment |
| Retro | period-aware, nostalgic | period-appropriate (70s, 80s, y2k, etc.) | era palettes | era shapes and textures | nostalgia brands, events, side projects |
| Playful | friendly, light, expressive | rounded sans | bright but not garish | generous radius, soft shadows | kids, casual apps, consumer fun |
| Soft / friendly | warm, human, reassuring | warm sans or humanist serif | warm neutrals, gentle accents | soft radius, low contrast surfaces | health, education, wellness, small business |
| High-density professional | maximal info, minimal waste | compact sans, small-but-legible scale, tabular | restrained, status colors carry meaning | tight spacing, hairline rules | B2B dashboards, admin, ops tools |
| Magazine-inspired | rhythmic, collage-like | mixed editorial scale | confident accents | asymnmetrical grids, imagery-led | media, lifestyle, culture |
| Data-centric | the data is the design | neutral sans + strong numerals | monochrome + one semantic accent | fine rules, chart-first layouts | analytics, monitoring, science |
| Monochromatic | single-hue sophistication | confident type carries the look | one hue across values | depends on hue personality | fashion, luxury, galleries, minimal brands |
| Warm human-centered | people-first, approachable | warm serif/sans pairing | earth and skin tones | soft shapes, friendly radius | health, education, community, nonprofits |
| Bold typography | type is the visual | oversized display type, strong contrast | minimal palette | layout built by type alone | studios, campaigns, posters, disruptive brands |
| Experimental | novel, surprising, original | unconventional pairings (used with care) | depends on concept | deliberately broken conventions | art, galleries, avant-garde brands |
| Premium commerce | rich, persuasive, upscale | elegant serif/sans pairing | deep neutrals + gilded accent | refined radius, layered elevation | e-commerce, hospitality, luxury retail |
| Government / institutional | trustworthy, clear, universal | neutral sans, strong legibility | restrained blues/grays, WCAG-tested | moderate radius, clear borders | public services, agencies, regulated industries |
| Financial | sober, exact, credible | serif or neutral sans + tabular numerals | dark green / navy / neutrals | fine rules, precise spacing | banking, investing, insurance |
| Scientific | precise, evidence-led | serif body + sans labels, real data | white/black + one accent | fine rules, chart-led layout | research, labs, health science |
| Developer-oriented | utilitarian, dense, honest | mono + sans, low decoration | dark/light code-friendly themes | small radius, visible borders | frameworks, docs, OSS, dev tools |
| Creative studio | expressive, authored, confident | distinctive typography | curated palettes | idiosyncratic, consistent | design agencies, studios, creators |
| High-craft / immersive | art-directed, spatial, cinematic | strong display concept (often oversized or kinetic) | concept-driven palette with deliberate behavior over time | composed depth planes, intentional overlap and rhythm | premium marketing sites, creative agencies, launches, brand experiences, interactive storytelling, showcases |

## High-Craft / Immersive

`workflows/create-high-craft.md` is the dedicated workflow for this family.
Its defining traits: art-directed, spatial, sometimes experimental or
cinematic; editorial or unconventional composition; motion governed by a
grammar (`design/motion-system.md`) rather than sprinkled on; strong
typography; intentional transitions; visual storytelling.

**High-craft does NOT mean maximum effects.** It is a discipline of coherence,
not an arms race of techniques. The visual language may be any of:

- restrained immersive
- editorial immersive
- cinematic
- brutalist spatial
- technical experimental
- luxury minimal
- kinetic typographic
- product-showcase
- generative
- architectural
- atmospheric

Select among these based on the product's audience, purpose, and emotional
objective — not by defaulting to one signature aesthetic. A luxury-minimal
immersive site and a brutalist-spatial one share almost nothing except the
discipline behind them.

The tell of a fake high-craft product is technique stacking: dark background +
giant type + glow + grain + glass cards + custom cursor + particles + 3D
sphere + magnetic buttons + parallax + marquee, all at once. That combination
is itself a generic AI aesthetic. Every technique must earn its place; one
strong idea beats twelve decorative effects.

## Selection rules

- **Never pick at random.** The audience and purpose decide the language. A
  tool for network engineers is not playful; a preschool app is not financial.
- **The same category yields different outcomes.** Two "SaaS UI kits" should
  be able to look nothing alike when audiences differ. Differentiation is a
  feature, not a risk.
- **Hybrids are allowed when coherent.** Combine languages deliberately
  (e.g., editorial typography on a data-centric grid), but one language must
  dominate so the result still feels single-sourced.
- **Stay consistent.** Once chosen, the language governs typography, color,
  spacing, shape, and motion. Drift back toward "default modern" is the most
  common failure.
- **Usability can veto style.** If the chosen language would hurt the task
  (e.g., ultra-dense layout for senior users), adapt it — style never trumps
  usability.
