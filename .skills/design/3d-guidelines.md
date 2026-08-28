# 3D Guidelines

3D is **optional**. Never add 3D simply because a product is classified as
high-craft, immersive, or premium. A flat composition with excellent
typography and motion grammar beats a decorative spinning object every time.

This file governs the *decision* to use 3D and the implementation level. The
raw Three.js implementation pattern and concept-object rules live in
`SKILL.md` (3D Objects section) — apply them once this file's gate is passed.

---

## The decision gate (all 8 questions before any 3D code)

Answer in writing during the direction phase:

1. **What does the 3D element communicate?** A concept, property, or story
   native to THIS product (the frozen crystal of cold-chain, the waveform of
   audio). "It looks impressive" is not an answer.
2. **Why can't a simpler technique communicate it?** Consider first: static
   image, CSS 3D transform, SVG animation, canvas 2D. If any of those
   achieves 90% of the effect, use it.
3. **What interaction does 3D enable?** Rotation, inspection, spatial
   navigation, physical response — something 2D cannot offer.
4. **What is the performance cost?** Draw calls, polygon count, texture
   memory, per-frame JS. Estimate against `design/motion-budget.md`.
5. **What is the fallback?** A static render/poster image that preserves the
   composition when WebGL fails or is disabled.
6. **What happens on mobile?** Reduced scene, lower DPR, fewer effects — or
   replaced by the fallback entirely.
7. **What happens with reduced motion?** The animated scene is removed or
   frozen into its static fallback; content never depends on it.
8. **What happens if WebGL is unavailable?** Feature-detect, swap to the
   fallback, keep layout intact (`design/progressive-enhancement.md`).

If questions 1–3 don't produce strong answers, do not use 3D.

---

## Implementation levels

Always choose the simplest viable level.

### Level A — CSS 3D
`perspective`, `transform-style: preserve-3d`, rotateX/Y/Z transitions.
Use for: depth cues, card rotations/flips, layered objects, simple spatial
transitions, tilt-on-hover. Cost: near zero. No dependencies. This level is
underused — most "we need Three.js" moments are Level A moments.

### Level B — Lightweight canvas/WebGL (no scene graph)
Hand-written shaders or small canvas programs: particle fields, procedural
backgrounds, generative textures, simple fluid/noise effects. Use for:
atmospheric scenes, generative identity visuals. Cost: moderate; one rAF loop,
pause offscreen, DPR-capped. Prefer plain Canvas 2D unless the effect truly
needs GPU shading.

### Level C — Three.js / React Three Fiber
Full scene graph: interactive objects, product visualization, spatial scenes,
camera movement, lighting, meaningful drag/zoom interactions. Use for: when
the 3D object IS a core part of the experience (configurator, hero artifact,
spatial narrative). Cost: significant bundle + runtime; lazy-load the scene;
dispose on unmount; follow all rules in SKILL.md's 3D Objects section
(concept-driven, cursor+scroll response, brand-token materials).

### Level D — External 3D tooling (Spline exports, model pipelines, etc.)
Only when justified by the product AND compatible with the project's
technology constraints. Default stance: avoid embeds/iframes (accessibility,
performance, customization loss). If used: self-hosted assets, documented
export pipeline for buyers, license-clean models, explicit fallback.

---

## Universal rules (all levels)

- **Concept-driven or nothing.** The element must embody the product's idea.
- **Fallback first.** Design the static fallback as part of the composition,
  not as an afterthought `<noscript>` dump.
- **Lazy initialization.** Initialize on intersection/interaction, never at
  page load; the page must be interactive before the scene boots.
- **Performance caps.** DPR ≤ 2, antialias only when needed, powerPreference
  set deliberately, geometry/material counts minimized, one shared rAF loop.
- **Lifecycle hygiene.** Dispose geometries, materials, textures, renderers;
  remove listeners; cancel rAF on unmount.
- **Reduced motion:** remove continuous rotation/breathing/camera drift; show
  the static state. Hide fully if a frozen render looks broken (per SKILL.md).
- **Mobile:** reduced scene complexity or full fallback; touch interactions
  replace pointer-only ones; never block scroll with a full-screen canvas.
- **Design-system membership.** Materials/colors/lighting come from the token
  palette; the 3D layer is part of the design system, not a separate universe.
- **One scene maximum.** Multiple independent 3D scenes on one page is a red
  flag against the motion budget.

---

## Decision summary

```text
Does it communicate a product-native concept?
  ├─ no  → no 3D. Compose with type/image/motion instead.
  └─ yes → can CSS 3D do it?
             ├─ yes → Level A.
             └─ no  → can a lightweight shader/canvas do it?
                        ├─ yes → Level B.
                        └─ no  → does real interactivity/spatiality justify
                                  the cost, with fallback+mobile+reduced-motion
                                  plans written?
                                  ├─ yes → Level C (or D if tooling demands).
                                  └─ no  → no 3D.
```
