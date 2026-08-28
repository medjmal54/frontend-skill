# Progressive Enhancement

Every immersive experience is built as layers on top of a working base. The
base experience must stand alone: real content, working navigation, reachable
primary action — with zero JavaScript and zero advanced CSS.

```text
Base experience
        ↓
Enhanced CSS
        ↓
Interaction enhancement
        ↓
Advanced motion
        ↓
Canvas/WebGL/3D
```

Each layer may fail independently — old browser, blocked JS, disabled WebGL,
reduced-motion preference, slow network, low-end device — without breaking any
layer below it.

---

## The failure contract

If an advanced layer fails, ALL of the following remain true:

- Content remains usable and readable.
- Navigation remains usable.
- The primary CTA remains visible and operable.
- Important information remains accessible (to users AND assistive tech).
- Layout does not collapse (no invisible sections, no overlapping chaos).
- Loading does not become an infinite blocking experience (no loader that can
  hang forever without a timeout escape).

3D and WebGL are enhancements, never prerequisites for basic functionality.

---

## Layer rules

### 1. Base experience
- Semantic HTML carries all content; CSS provides a clean, readable layout
  using tokens (`design/design-direction.md`).
- No element is hidden via `opacity: 0` / `visibility: hidden` in the default
  state waiting for JS to reveal it. If an entrance animation needs a hidden
  initial state, apply it ONLY when JS has confirmed it will run
  (e.g., add a `js-animations` class on `<html>` first), or use animation
  `both` fill from a visible keyframe start.
- Forms work, links navigate, anchors jump — natively.

### 2. Enhanced CSS
- Progressive CSS (`@supports`) for grid gaps, `clamp()` type, aspect-ratio,
  scroll-driven animations where supported; graceful degradation elsewhere.

### 3. Interaction enhancement
- JS adds hover/press/focus choreography, IntersectionObserver reveals,
  smooth anchor scrolling, magnetic/cursor effects (pointer-fine only).
- All interactions have keyboard-operable equivalents.

### 4. Advanced motion
- Scroll-linked systems, pinned sequences, page transitions.
- Gated behind reduced-motion detection: under `prefers-reduced-motion`,
  this layer swaps to static equivalents instead of running silently broken.

### 5. Canvas/WebGL/3D
- Feature-detect (`canvas.getContext('webgl2' || 'webgl')`, context-loss
  handling) before mounting any scene.
- Lazy-init on intersection or intent; poster/fallback occupies the space
  until then.
- Scene failure (context lost, shader compile error) → swap to fallback,
  never leave a black rectangle.

---

## Detection patterns

```javascript
/**
 * Adds capability classes to <html> so CSS/JS can gate enhancements.
 * Base experience assumes NOTHING until proven.
 */
function detectCapabilities() {
  const root = document.documentElement;
  root.classList.add('js'); // enhancements may now hide-for-animation

  const reduceMotion = window.matchMedia('(prefers-reduced-motion: reduce)');
  root.classList.toggle('reduced-motion', reduceMotion.matches);
  reduceMotion.addEventListener?.('change', e =>
    root.classList.toggle('reduced-motion', e.matches));

  try {
    const c = document.createElement('canvas');
    root.classList.toggle('webgl',
      !!(c.getContext('webgl2') || c.getContext('webgl')));
  } catch { root.classList.remove('webgl'); }
}
```

CSS consumes the gates:

```css
/* Hidden-until-reveal ONLY when JS confirmed animations run */
.js [data-reveal] { opacity: 0; }
.reduced-motion .js [data-reveal] { opacity: 1 !important; }

/* Static fallback occupies canvas space */
.scene-fallback { display: block; }
.webgl .scene-fallback { display: none; }
.webgl .scene-canvas { display: block; }
```

## Loader discipline

Immersive pages sometimes use intro loaders. Rules:

- Hard timeout (e.g., 2.5s) after which content shows regardless of asset
  state.
- Progress must reflect real loading, not a fake timeline that lies.
- Reduced motion / repeat visits: skip or shorten dramatically.
- The loader never traps keyboard focus or hides skip access to content.

---

## Audit hooks

Verified in `quality/high-craft-audit.md` (Performance + Accessibility) and
`quality/accessibility-audit.md`: disable JS, disable WebGL, enable reduced
motion, throttle network — at each configuration the base contract above must
hold.
