# Workflow — Create a High-Craft Experience

For products that demand art direction, motion systems, spatial composition,
and optionally 3D: premium marketing sites, creative agency sites, experimental
landing experiences, product launches, brand experiences, cinematic product
presentations, interactive storytelling, motion-first interfaces, spatial
interfaces, selective 3D-enhanced experiences, immersive product demonstrations,
creative portfolios/showcases.

This category exists because a standard landing-page workflow would produce an
insufficient experience for these products — not because they need "more
animation." High-craft means **deliberate art direction, coherent motion
grammar, intentional spatial composition, and technology chosen to fit the
experience**. It never means maximum effects (see `design/design-diversity.md`
→ High-Craft / Immersive).

Routing: entered from `SKILL.md` Step 1 when the request involves immersive,
cinematic, experimental, art-directed, motion-first, spatial, storytelling,
showcase, launch, WebGL/Three.js/shader concepts — or when the project clearly
implies a normal landing-page treatment would fall short. Do NOT route ordinary
marketing pages here.

---

## Phase A — Experience Definition (before any visual thought)

Answer all of these in writing:

- **Product purpose** — what exists and why.
- **Audience** — who arrives, on what device, in what mood.
- **Primary action** — the one thing the experience must drive.
- **Emotional objective** — what should the visitor FEEL (awe, trust, hunger,
  urgency, calm superiority)?
- **Narrative objective** — what sequence should they understand (origin →
  craft → proof; problem → mechanism → result)?
- **Information hierarchy** — what must be learned first, second, optionally.
- **Interaction model** — scroll-driven, cursor-driven, click-through chapters,
  free exploration?
- **Brand personality** — 3–5 words (`design/design-diversity.md`).
- **Visual tension** — what opposition gives it energy (dense vs open, ordered
  vs chaotic, warm vs clinical)?
- **Desired immersion level** — glanceable enhancement → captivation → total
  world?

The governing question:

> What should the user experience, understand, or feel differently because of
> this interface?

Do NOT begin with "which animation should I add." Animation choices are
outputs of this phase, never inputs.

## Phase B — Art Direction (before any layout)

Complete `design/art-direction.md` fully: visual concept, typography strategy,
color strategy, imagery strategy, shape language, texture language, lighting
language, depth language, composition strategy, visual rhythm, motion
personality.

The direction must be coherent enough that the product could be recognized
without seeing its source code. Pre-rejected generic combinations are listed
there — purple/blue gradient + white cards, giant centered SaaS hero + two
buttons, random glassmorphism, floating blobs, excessive rounded cards,
arbitrary glows, decorative 3D with no conceptual purpose.

Select the aesthetic variant deliberately (`design/design-diversity.md` →
High-Craft): restrained immersive, editorial immersive, cinematic, brutalist
spatial, technical experimental, luxury minimal, kinetic typographic,
product-showcase, generative, architectural, atmospheric.

## Phase C — Spatial Model

Define the depth system per `design/spatial-composition.md`: planes,
z-axis hierarchy, overlap rules, focal points, negative space strategy,
sticky anchors, parallax policy, scale relationships, pacing, section-to-section
continuity. Record which plane each major section's content occupies.

## Phase D — Motion Grammar & Intensity

- Define the motion grammar per `design/motion-system.md`: roles in use,
  relationship rules, choreography plan (entrances, exits, staggers, scroll,
  text, media, sections, states, hover/press/focus, loading, navigation,
  cursor-if-justified).
- Choose the **intensity level 0–5** — lowest level achieving Phase A's
  objectives. Marketing context does not auto-elevate the level.
- At Level 3+, write the **motion budget** per `design/motion-budget.md`.

## Phase E — 3D Decision

Run `design/3d-guidelines.md`. Default answer: no 3D. If used, record the
8-question answers, implementation level A–D, fallback design, mobile plan,
reduced-motion plan. Concept-driven only.

## Phase F — Technology & Performance Decision

- Walk the technology ladder (`design/motion-system.md` → Technology
  selection). Respect the project's existing stack; framework baseline per
  SKILL.md Law 5 (HTML/CSS/JS for component-level deliverables, React for
  site-level).
- Write the performance budget: interactivity target, heavy-asset deferral,
  WebGL init strategy, animation property rules, mobile tier reductions.

## Phase G — Accessibility & Reduced-Motion Strategy

Per `design/accessibility.md`, `design/motion-system.md` → Reduced motion
contract, `design/progressive-enhancement.md`:

- Reduced-motion behavior defined per effect class BEFORE building effects.
- Keyboard path through the entire experience defined (scroll-jacked or pinned
  sections still progress via keyboard; focus order sane).
- Content never hidden behind motion; contrast holds over every background
  state the experience passes through.

## Phase H — Responsive Transformation Strategy

Per `design/responsive.md` → Immersive experiences: how the composition
transforms at mobile/tablet/desktop/large-desktop — reduced depth, simplified
motion, 3D removal or reduction, fewer simultaneous elements, changed section
composition, hover→tap replacements, canvas→static alternatives. Mobile is
intentionally art-directed.

## Phase I — Originality Rationale

State in one short paragraph why this identity is original: which techniques
(not identities) informed it, and how the result differs from any referenced
work. References may shape vocabulary, never outcome. See the Originality
Firewall in `design/ai-slop-firewall.md`.

---

## The internal prompt compiler

Before writing code, compile everything above into a structured implementation
brief — an internal design-to-code compilation of THIS project's requirements.
Never copy prompts from third-party sources; generate original instructions
from the project's own requirements.

```text
PROJECT BRIEF
      ↓
EXPERIENCE INTENT        (Phase A)
      ↓
ART DIRECTION            (Phase B)
      ↓
VISUAL SYSTEM            (tokens: type/color/space/shape/elevation)
      ↓
SPATIAL MODEL            (Phase C)
      ↓
MOTION GRAMMAR           (Phase D)
      ↓
INTERACTION STATES       (hover/press/focus/loading/error/empty per element)
      ↓
TECHNOLOGY DECISION      (Phase F)
      ↓
PERFORMANCE BUDGET       (Phase F)
      ↓
ACCESSIBILITY STRATEGY   (Phase G)
      ↓
IMPLEMENTATION PLAN
```

The compiled brief specifies: what is being built, why it exists, visual
concept, content hierarchy, layout/composition, interaction behavior, motion
behavior, responsive behavior, accessibility behavior, performance constraints,
technology constraints, component boundaries, states, and edge cases. If any
section cannot be filled, return to its phase — do not improvise it mid-code.

---

## Implementation order

1. **Base experience first** — full semantic HTML content, token-driven CSS
   layout, working navigation and CTA with zero advanced features
   (`design/progressive-enhancement.md`). This is not scaffolding to throw
   away; it IS the fallback layer.
2. Enhanced CSS layer (@supports upgrades).
3. Interaction layer (reveals, feedback choreography) behind capability gates.
4. Advanced motion layer (scroll systems, transitions) behind reduced-motion
   gates.
5. Canvas/WebGL/3D layer last — lazy-initialized, fallback-first
   (`design/3d-guidelines.md`).
6. Realistic domain-specific content throughout — the slop firewall's content
   rules apply in full (`design/data-architecture.md` where data-driven).

Standard implementation requirements from `SKILL.md` Step 3 still apply
(tokens, states, semantic HTML, responsive restructure, build verification).

## Audit

Run `quality/high-craft-audit.md` IN ADDITION to the standard audits
(`quality/visual-audit.md`, `quality/accessibility-audit.md`,
`quality/responsive-audit.md`, `quality/code-audit.md`, `quality/ux-audit.md`).
A failure in originality, accessibility, or basic usability anywhere is a
redesign trigger, not a patch item.

## Commercial packaging

High-craft products sold or distributed follow every rule in `marketplace/`
unchanged: documentation, source organization, realistic demo content,
licensing transparency (including fonts/models/canvas assets), dependency
justification, customization guidance, responsive + accessibility compliance,
code quality, audits. High-craft must remain commercially usable and
maintainable — a buyer without WebGL knowledge can still install, customize
copy/colors, and ship it.

## Deliverables

- Compiled implementation brief (the compiler output above).
- The experience: base layer + enhancement layers, realistic content.
- Motion budget + performance notes recorded in the direction brief.
- Fallback verification (JS-off / WebGL-off / reduced-motion walkthroughs).
- Full audit results with fixes applied.
- Marketplace package where requested.
