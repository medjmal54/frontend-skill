# Landing Pages: Brand Representation Through Typography & Concept

Every website gets a landing page. The landing page is the brand's first
impression — it must establish identity, communicate value, and create
emotional resonance. Design is driven by typography and concept, not by
templates.

---

## Typography as Identity

The typeface IS the brand's voice made visible. Choose typefaces that
embody the brand's character before considering readability.

### Type Personality Mapping

| Brand character | Typeface direction | Example families | Treatment |
|---|---|---|---|
| Artisanal / Craft | High-contrast serif | Playfair Display, Cormorant, DM Serif Display | Tight tracking, large sizes, editorial spacing |
| Precision / Tech | Geometric sans | IBM Plex Sans, Outfit, Manrope | Wide tracking at large sizes, monospace accents |
| Warm / Approachable | Soft rounded sans | Nunito, Quicksand, Plus Jakarta Sans | Generous tracking, medium weight, rounded terminals |
| Luxury / Refined | Thin/light serif or sans | Didot, Bodoni, Libre Baskerville | Ultra-light weight, massive sizes, tight leading |
| Industrial / Raw | Monospace or condensed | JetBrains Mono, IBM Plex Mono, Barlow Condensed | Uppercase labels, tight leading, data-dense |
| Organic / Natural | Humanist sans | Source Sans, Lato, Open Sans | Warm italic accents, relaxed spacing |
| Bold / Energetic | Heavy display | Anton, Bebas Neue, Oswald | All-caps, tight leading, massive scale |
| Minimal / Clean | Thin geometric | Inter (at thin weights), Plus Jakarta, Manrope | Whisper-light weights, extreme whitespace |

### Typography Scale for Landing Pages

Use a modular scale (1.333 ratio recommended) to create hierarchy:

```css
:root {
  --type-step: 1.333;
  --body: 1rem;
  --micro: calc(var(--body) / var(--type-step));
  --small: calc(var(--body) / var(--type-step) * 0.9);
  --h6: calc(var(--body) * var(--type-step));
  --h5: calc(var(--h6) * var(--type-step));
  --h4: calc(var(--h5) * var(--type-step));
  --h3: calc(var(--h4) * var(--type-step));
  --h2: calc(var(--h3) * var(--type-step));
  --h1: calc(var(--h2) * var(--type-step));
  --hero: max(calc(var(--h1) * var(--type-step) * var(--type-step)), 17.6vw);
}
```

**Hero text rule:** The hero headline must be BIG enough to feel like a
statement. Minimum `--h1` size on desktop, ideally `--hero` (scales with
viewport). This is not a heading — it's a visual element.

### Typography Treatments

- **Tight tracking at large sizes:** `letter-spacing: -0.02em` to `-0.05em`
  for display text. Tight = premium.
- **Wide tracking at small sizes:** `letter-spacing: 0.06em` to `0.12em`
  for labels and uppercase text. Wide = refined.
- **Contrast weight pairing:** Light body + bold headline, or vice versa.
  Never same weight for both.
- **Font feature settings:** Use `font-feature-settings: "dlig", "ss03"`
  for decorative ligatures on display fonts where available.

---

## Concept Templates

Every landing page has a central visual concept. Choose one based on the
brand's story:

### Concept 1: Scroll-Driven Narrative

The page tells a story as you scroll. Sections reveal progressively.

**Best for:** Brands with a story (origin story, craft process, journey)

**Required elements:**
- Hero with text that reveals on scroll (per-character blur or line-by-line)
- 3+ scroll-tracked sections with parallax depth
- Color transition between sections (dark→light or palette shift)
- Sticky pinned section for key narrative moment
- Progress bar showing scroll position through the story

**Implementation pattern:**
```css
/* Scroll-driven text reveal */
.reveal-text {
  --progress: 0;
  opacity: calc(var(--progress));
  filter: blur(calc((1 - var(--progress)) * 8px));
  transform: translateY(calc((1 - var(--progress)) * 20px));
}

/* Per-character stagger */
.reveal-char {
  --char-progress: clamp(0, (var(--progress) - var(--char-index) * 0.02) / 0.3, 1);
  opacity: var(--char-progress);
  filter: blur(calc((1 - var(--char-progress)) * 4px));
}

/* Parallax layer speeds */
.parallax-slow { transform: translateY(calc(scroll * 0.05)); }
.parallax-medium { transform: translateY(calc(scroll * 0.12)); }
.parallax-fast { transform: translateY(calc(scroll * 0.22)); }
```

### Concept 2: Product as Hero

The product is the visual anchor. Shown at massive scale with detailed
close-ups, specs orbit the product.

**Best for:** Physical products (electronics, food, beverages, tools)

**Required elements:**
- Full-viewport product image with parallax drift
- Specs/features positioned around the product (not below it)
- Scroll-triggered exploded view or detail reveals
- Color/variant switcher that changes the entire page palette
- Ambient Ken Burns drift on product image

**Implementation pattern:**
```css
.product-hero {
  position: relative;
  min-height: 100vh;
  display: grid;
  place-items: center;
}

.product-hero__image {
  width: 60vw;
  max-width: 600px;
  animation: kenyburns-drift 20s ease-in-out infinite alternate;
}

/* Specs orbit the product */
.spec {
  position: absolute;
  /* positioned via CSS grid or custom properties */
  opacity: calc(var(--scroll-progress) - var(--spec-delay));
  transform: translateY(calc((1 - var(--scroll-progress)) * 30px));
}
```

### Concept 3: Process as Proof

The brand's process is shown through stepped reveals. Each step is a
scroll-tracked section.

**Best for:** Craft brands (coffee roasting, sugar refining, brewing)

**Required elements:**
- Numbered steps that reveal as you scroll
- Progress indicator showing which step you're on
- Each step has a large image + short description
- Ambient motion in each step (particles, drift, shimmer)
- Final step is the "result" — the product in its finished form

**Implementation pattern:**
```css
.process-step {
  min-height: 100vh;
  position: relative;
}

.process-step__number {
  font-size: var(--hero);
  font-weight: 100;
  opacity: calc(var(--step-progress) * 0.15);
  position: absolute;
  top: var(--space-8);
  left: var(--space-8);
}

.process-step__content {
  opacity: calc(var(--step-progress));
  transform: translateY(calc((1 - var(--step-progress)) * 40px));
}

/* Progress bar between steps */
.process-progress {
  position: fixed;
  left: var(--space-8);
  top: 50%;
  width: 2px;
  height: 40vh;
  background: var(--color-border);
}

.process-progress__fill {
  width: 100%;
  background: var(--color-primary);
  transform: scaleY(var(--scroll-progress));
  transform-origin: top;
}
```

### Concept 4: Sensory Immersion

The page evokes taste, smell, or touch through visual language.

**Best for:** Food, beverage, fragrance, wellness brands

**Required elements:**
- Warm/cool color temperature that shifts with scroll
- Texture imagery (close-up surfaces, grain, liquid, steam)
- Organic motion (slow drift, gentle oscillation, floating particles)
- Large ambient typography (brand words floating in background)
- Sound cues implied through visual rhythm

**Implementation pattern:**
```css
/* Temperature shift */
.sensory-section {
  background: rgb(
    calc(var(--brand-r) + var(--scroll-progress) * var(--shift-r)),
    calc(var(--brand-g) + var(--scroll-progress) * var(--shift-g)),
    calc(var(--brand-b) + var(--scroll-progress) * var(--shift-b))
  );
}

/* Floating ambient text */
.ambient-word {
  position: absolute;
  font-size: clamp(3rem, 10vw, 8rem);
  opacity: 0.06;
  animation: float-drift 12s ease-in-out infinite;
  pointer-events: none;
  user-select: none;
}

@keyframes float-drift {
  0%, 100% { transform: translateY(0) rotate(-2deg); }
  50% { transform: translateY(-15px) rotate(1deg); }
}
```

---

## Scroll-Driven Animation System

### Using CSS @property for Scroll Interpolation

```css
@property --scroll-progress {
  syntax: "<number>";
  inherits: true;
  initial-value: 0;
}

/* Track scroll via IntersectionObserver or scroll event */
.section {
  --scroll-progress: 0; /* Updated by JS */
}

/* Use in animations */
.animated-element {
  opacity: var(--scroll-progress);
  transform: translateY(calc((1 - var(--scroll-progress)) * 40px));
}
```

### Scroll Progress via JavaScript

```js
function createScrollTracker(section, options = {}) {
  const { start = 0, end = 1 } = options;

  const observer = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting) {
        const rect = entry.boundingClientRect;
        const viewportHeight = window.innerHeight;
        const progress = Math.max(0, Math.min(1,
          (viewportHeight - rect.top) / (viewportHeight + rect.height)
        ));
        section.style.setProperty('--scroll-progress',
          (start + progress * (end - start)).toFixed(3)
        );
      }
    },
    { threshold: Array.from({ length: 100 }, (_, i) => i / 100) }
  );

  observer.observe(section);
  return () => observer.disconnect();
}
```

### Text Reveal Patterns

**Per-character blur reveal:**
```js
function splitTextForReveal(element) {
  const text = element.textContent;
  element.innerHTML = '';
  element.setAttribute('aria-label', text);

  [...text].forEach((char, i) => {
    const span = document.createElement('span');
    span.className = 'reveal-char';
    span.style.setProperty('--char-index', i);
    span.textContent = char === ' ' ? '\u00A0' : char;
    span.setAttribute('aria-hidden', 'true');
    element.appendChild(span);
  });
}
```

```css
.reveal-char {
  display: inline-block;
  opacity: 0;
  filter: blur(4px);
  transform: translateY(8px);
  transition: opacity 0.4s ease, filter 0.4s ease, transform 0.4s ease;
  transition-delay: calc(var(--char-index) * 0.03s);
}

.reveal-char.is-visible {
  opacity: 1;
  filter: blur(0);
  transform: translateY(0);
}
```

**Line-by-line slide-up:**
```css
.reveal-line {
  overflow: hidden;
}

.reveal-line__inner {
  transform: translateY(100%);
  transition: transform 0.6s cubic-bezier(0.23, 1, 0.32, 1);
  transition-delay: calc(var(--line-index) * 0.05s);
}

.reveal-line.is-visible .reveal-line__inner {
  transform: translateY(0);
}
```

---

## Cursor Interactions

### Spotlight Gradient Border

A border that glows and follows the cursor position:

```css
.spotlight-card {
  --spot-x: 50%;
  --spot-y: 50%;
  position: relative;
  border: 1px solid transparent;
  background-origin: border-box;
  background-clip: padding-box, border-box;
}

.spotlight-card::before {
  content: '';
  position: absolute;
  inset: -1px;
  border-radius: inherit;
  background: radial-gradient(
    circle at var(--spot-x) var(--spot-y),
    var(--color-primary) 0%,
    transparent 60%
  );
  opacity: 0;
  transition: opacity 0.3s ease;
  pointer-events: none;
  z-index: -1;
}

.spotlight-card:hover::before {
  opacity: 0.6;
}
```

```js
card.addEventListener('mousemove', (e) => {
  const rect = card.getBoundingClientRect();
  card.style.setProperty('--spot-x',
    ((e.clientX - rect.left) / rect.width * 100) + '%'
  );
  card.style.setProperty('--spot-y',
    ((e.clientY - rect.top) / rect.height * 100) + '%'
  );
});
```

### Magnetic Button

Button that subtly follows cursor position:

```js
function createMagneticButton(button, strength = 0.3) {
  button.addEventListener('mousemove', (e) => {
    const rect = button.getBoundingClientRect();
    const x = e.clientX - rect.left - rect.width / 2;
    const y = e.clientY - rect.top - rect.height / 2;
    button.style.transform =
      `translate(${x * strength}px, ${y * strength}px)`;
  });

  button.addEventListener('mouseleave', () => {
    button.style.transform = 'translate(0, 0)';
    button.style.transition = 'transform 0.4s cubic-bezier(0.23, 1, 0.32, 1)';
  });

  button.addEventListener('mouseenter', () => {
    button.style.transition = 'none';
  });
}
```

### Hover Reveal Content

Content that appears on hover with a smooth transition:

```css
.hover-reveal {
  position: relative;
  overflow: hidden;
}

.hover-reveal__hidden {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transform: scale(0.95);
  transition: opacity 0.3s ease, transform 0.3s ease;
  background: var(--color-surface-overlay);
}

.hover-reveal:hover .hover-reveal__hidden {
  opacity: 1;
  transform: scale(1);
}
```

---

## Color Behavior as Brand Language

### Cursor Trail

A colored trail that follows the cursor:

```css
.cursor-trail {
  position: fixed;
  width: 200px;
  height: 200px;
  border-radius: 50%;
  background: radial-gradient(circle, var(--color-primary) 0%, transparent 70%);
  opacity: 0.08;
  pointer-events: none;
  transform: translate(-50%, -50%);
  transition: left 0.6s ease, top 0.6s ease;
  z-index: 0;
}
```

### Scroll-Driven Color Shift

Background color changes based on scroll position:

```css
.page {
  --scroll-r: 0;
  --scroll-g: 0;
  --scroll-b: 0;
  background: rgb(
    calc(var(--start-r) + var(--scroll-r) * var(--end-r)),
    calc(var(--start-g) + var(--scroll-g) * var(--end-g)),
    calc(var(--start-b) + var(--scroll-b) * var(--end-b))
  );
}
```

---

## Landing Page Section Templates

### Hero Section (Required)

```css
.hero {
  min-height: 100vh;
  min-height: 100dvh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  position: relative;
  overflow: hidden;
}

.hero__headline {
  font-size: var(--hero);
  font-weight: 700;
  line-height: 0.95;
  letter-spacing: -0.03em;
}

.hero__sub {
  font-size: var(--h4);
  font-weight: 300;
  max-width: 28ch;
}

.hero__ambient {
  position: absolute;
  pointer-events: none;
  opacity: 0.05;
  animation: ambient-drift 15s ease-in-out infinite alternate;
}
```

### Feature/Product Grid

```css
.feature-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: var(--space-8);
}

.feature-card {
  padding: var(--space-8);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-lg);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.feature-card:hover {
  transform: translateY(-4px);
  box-shadow: var(--shadow-lg);
}
```

### CTA Section

```css
.cta-section {
  min-height: 60vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  gap: var(--space-6);
  position: relative;
  overflow: hidden;
}

.cta-section__headline {
  font-size: var(--h2);
  font-weight: 700;
}

.cta-section__ambient {
  position: absolute;
  inset: 0;
  background: radial-gradient(
    ellipse at 50% 100%,
    var(--color-primary) 0%,
    transparent 60%
  );
  opacity: 0.06;
  pointer-events: none;
}
```

---

## Implementation Checklist

For every landing page:

- [ ] Typography chosen for brand character (not just "readable")
- [ ] Hero text is massive (scales with viewport, minimum --h1)
- [ ] At least one concept template applied (narrative, product, process, sensory)
- [ ] Scroll-driven animations present (text reveal, parallax, color shift)
- [ ] Cursor interaction present (spotlight, magnetic, or hover reveal)
- [ ] At least 3 ambient animations running (drift, float, shimmer)
- [ ] Color behavior as brand language (cursor trail, scroll shift, or gradient)
- [ ] All sections earn height with content + motion + imagery
- [ ] Hero fills viewport (no wasted space above fold)
- [ ] `prefers-reduced-motion` disables all kinetic motion, keeps content visible
- [ ] Mobile: scroll parallax disabled, ambient animations reduced
- [ ] No blacklisted patterns (centered hero + button, lorem ipsum, fake metrics)
