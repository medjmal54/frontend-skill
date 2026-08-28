# Motion Budget

Every product at motion intensity Level 3+ (`design/motion-system.md`) must
establish an approximate motion budget before implementation. The budget is
not a bureaucratic form — it is a deliberate decision about where the
experience's runtime cost goes, so that the page stays fast, smooth, and
battery-friendly while still feeling alive.

Motion is a spend. Every continuously animated element, every scroll-linked
animation, every blur layer, and every canvas draws from the same pool: frame
time. When the pool runs out, animations drop frames, scrolling stutters,
input latency rises, and the "premium" experience becomes a broken one.

---

## Establishing the budget

For high-motion products, write down approximate limits for each line below
in the direction brief. Numbers are defaults; adjust per project and record
the result.

| Budget line | Default guidance (L3) | Notes |
|---|---|---|
| Continuously animated elements visible per viewport | ≤ 2–3 | Ambient loops, drifting layers, pulsing indicators |
| Scroll-linked animations per section | ≤ 1–2 | Parallax layers in ONE system count as one composite |
| Simultaneous entrance-animated elements | ≤ 6–8 with stagger | More than ~10 simultaneous tweens risks jank on low-end mobile |
| Expensive filters animating (`blur`, `backdrop-filter`) | ≤ 1 animated instance | Blur is one of the most expensive properties; prefer static blur + opacity animation |
| Large image animations | ≤ 1 full-viewport | Ken Burns on hero only; never multiple full-bleed drifts |
| Canvas/WebGL usage | 0 unless justified | One scene, lazy-initialized, paused offscreen |
| Video | Autoplay muted loop ≤ 1, `preload="metadata"` | Poster required; never block interaction on video |
| JS animation workload | 1 rAF loop shared by all effects | No per-component rAF loops; batch DOM reads/writes |
| Layout-thrashing patterns | 0 | Never read layout inside rAF after writing it; cache rects |
| Animated DOM nodes | Prefer few deep over many shallow | Composited transforms on parents beat animating dozens of children |

---

## Hard rules

- **Prefer transform/opacity-based animation.** These are compositor-friendly.
  Never animate `width`, `height`, `margin`, `top`, `left`, `padding`,
  `border-radius`. No `transition: all`.
- **Avoid unnecessary continuous animation.** If nothing changes when the
  animation completes, it should not loop forever. Do not animate merely
  because something is visible — visibility is not justification.
- **Pause what cannot be seen.** Use IntersectionObserver to pause ambient
  loops, canvases, and videos that scroll out of view. Resume on re-entry.
- **One shared requestAnimationFrame loop** drives all JS-driven effects;
  components subscribe to it rather than owning their own loops.
- **Respect device tiers.** Cap `devicePixelRatio` (≤ 2), reduce particle
  counts and layer counts on small screens, and disable scroll-parallax on
  touch devices where jank is likely (see `design/responsive.md`).
- **Memory pressure.** Dispose geometries/materials/renderers, revoke object
  URLs, remove listeners on unmount. Long sessions (tab left open) must not
  accumulate GPU memory or listeners.
- **Loading is part of the budget.** Heavy assets are deferred/lazy-loaded;
  the experience must become interactive quickly even if decoration has not
  finished loading. A loader may set the mood briefly but never blocks
  content behind a long fixed timeline.

## Mobile / low-end adjustments

At minimum, when viewport width < 768px or hardware concurrency is low:

- Halve continuous-animation counts; keep at most one ambient element.
- Replace canvas/WebGL scenes with static renders or poster imagery unless
  the scene IS the product.
- Disable scroll-driven parallax; keep simple viewport-entry reveals.
- Reduce blur usage; swap backdrop-filter panels for solid translucent fills.

These reductions are art-direction decisions, documented like everything else.

## Where the budget lives

Record the chosen budget in the direction brief (one line):

```text
Motion budget: 3 ambient elements, 1 parallax system (3 layers),
0 canvas, 0 video autoplay, 1 rAF loop, mobile: ambient reduced to 1,
parallax off.
```

The budget is checked again during audit — see `quality/high-craft-audit.md`
(Performance section). A blown budget is a Major finding; a blown budget plus
measured jank is Blocking.
