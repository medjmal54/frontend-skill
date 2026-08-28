# Motion

Motion has a job. The question is always "what does this animation do for the
user?" — if there is no answer, there is no animation. But every interaction
MUST have an answer. A static UI is a dead UI.

This file holds the interaction checklist and CSS recipes. The motion
**grammar** (roles, relationships, choreography) and the authoritative
**intensity scale (0–5)** live in `design/motion-system.md`; workload limits
live in `design/motion-budget.md`.

---

## Animation Intensity Levels

The canonical scale is **Level 0–5** in `design/motion-system.md`:

- **L0 Static** — no motion beyond browser defaults (deliberate choice).
- **L1 Micro-interaction** — feedback and state changes only (dashboards,
  forms, data tools). ≈ the old "Dashboard/App" level.
- **L2 Expressive** — coordinated entrances, scroll reveals, text/image
  reveals, limited ambient (standard landing pages, templates). ≈ the old
  "Landing Page/Template" level.
- **L3 Choreographed** — scroll-driven sequences, narrative transitions,
  sophisticated sequencing; requires a motion budget.
- **L4 Immersive** — spatial movement, canvas experiences, advanced
  transitions; requires progressive enhancement architecture.
- **L5 Experimental** — motion as part of the product concept itself.

Choose the lowest level achieving the desired experience. All recipes below
apply at every level; what changes is how far into the page-animation and
scroll-choreography sections you reach.

---

## The Animation Checklist (Every Product Must Cover All)

If you skip any of these, the product is incomplete.

| Interaction | Required animation | Duration |
|---|---|---|
| Page/view load | Elements stagger in (fade + slide up) | 300–600ms total, 50ms stagger |
| Card/item hover | Scale up + shadow lift + border glow | 150–200ms |
| Card/item click | Scale down press + navigate/expand | 100–150ms |
| Button hover | Background shift + subtle lift or glow | 120–180ms |
| Button press | `scale(0.97)` + darken | 80–120ms |
| Toggle/switch | Thumb slides + color morphs | 200–250ms |
| Modal/drawer open | Backdrop fade + panel slide + content fade-in | 250–400ms |
| Modal/drawer close | Reverse of open | 200–300ms |
| Toast/notification | Slide in from edge + auto-dismiss slide out | 300ms in, 200ms out |
| Dropdown/menu open | Fade + scale from origin point | 150–200ms |
| Tab switch | Indicator slides + content crossfade | 200–300ms |
| List item add/remove | Fade + height collapse/expand | 250–350ms |
| Data value change | Number counts up/down or color flash | 300–500ms |
| Skeleton → loaded | Shimmer resolves to content | 400–600ms |
| Scroll reveal | Elements fade + translate up on viewport entry | 400–600ms |
| Focus ring | Ring scales in around focused element | 100–150ms |

---

## Foundation CSS Recipes (Dashboards + Components)

### Card Hover Lift
```css
.card {
  transition:
    transform var(--duration-fast) var(--ease-spring),
    box-shadow var(--duration-fast) var(--ease-spring),
    border-color var(--duration-fast) var(--ease-spring);
  will-change: transform;
}

.card:hover {
  transform: translateY(-4px) scale(1.02);
  box-shadow: var(--shadow-lg);
  border-color: var(--color-primary-muted);
}
```

### Card Click Press
```css
.card:active {
  transform: translateY(0) scale(0.98);
  transition-duration: var(--duration-instant);
}
```

### Button Hover + Press
```css
.btn {
  transition:
    background-color var(--duration-fast) var(--ease-spring),
    transform var(--duration-instant) var(--ease-spring),
    box-shadow var(--duration-fast) var(--ease-spring);
}

.btn:hover {
  background-color: var(--color-primary-hover);
  box-shadow: var(--shadow-sm);
  transform: translateY(-2px);
}

.btn:active {
  transform: translateY(0) scale(0.97);
  transition-duration: var(--duration-instant);
}
```

### Staggered Grid Entrance
```css
@keyframes card-enter {
  from {
    opacity: 0;
    transform: translateY(12px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.card-grid > .card {
  animation: card-enter var(--duration-slow) var(--ease-spring) both;
}

.card-grid > .card:nth-child(1) { animation-delay: 0ms; }
.card-grid > .card:nth-child(2) { animation-delay: 50ms; }
.card-grid > .card:nth-child(3) { animation-delay: 100ms; }
.card-grid > .card:nth-child(4) { animation-delay: 150ms; }
.card-grid > .card:nth-child(5) { animation-delay: 200ms; }
.card-grid > .card:nth-child(6) { animation-delay: 250ms; }
```

### Slide-Over Panel
```css
.slide-over-backdrop {
  opacity: 0;
  transition: opacity var(--duration-normal) var(--ease-smooth);
  pointer-events: none;
}

.slide-over-backdrop[data-open="true"] {
  opacity: 1;
  pointer-events: auto;
}

.slide-over-panel {
  transform: translateX(100%);
  transition: transform var(--duration-enter);
  will-change: transform;
}

.slide-over-panel[data-open="true"] {
  transform: translateX(0);
}

.slide-over-panel[data-open="false"] {
  transform: translateX(100%);
  transition: transform var(--duration-exit);
}
```

### Modal Open/Close
```css
.modal-backdrop {
  opacity: 0;
  transition: opacity var(--duration-normal) var(--ease-smooth);
}

.modal-backdrop[data-open="true"] { opacity: 1; }

.modal-content {
  opacity: 0;
  transform: scale(0.95) translateY(8px);
  transition:
    opacity var(--duration-normal) var(--ease-spring),
    transform var(--duration-normal) var(--ease-spring);
}

.modal-content[data-open="true"] {
  opacity: 1;
  transform: scale(1) translateY(0);
}
```

### Toast Notification
```css
@keyframes toast-in {
  from {
    opacity: 0;
    transform: translateX(100%) scale(0.95);
  }
  to {
    opacity: 1;
    transform: translateX(0) scale(1);
  }
}

@keyframes toast-out {
  from {
    opacity: 1;
    transform: translateX(0) scale(1);
  }
  to {
    opacity: 0;
    transform: translateX(100%) scale(0.95);
  }
}

.toast {
  animation: toast-in var(--duration-enter) forwards;
}

.toast[data-dismissing="true"] {
  animation: toast-out var(--duration-exit) forwards;
}
```

### Tab Indicator Slide
```css
.tab-indicator {
  transition: transform var(--duration-normal) var(--ease-spring);
}
```

### Dropdown / Menu
```css
.dropdown-menu {
  opacity: 0;
  transform: scale(0.95) translateY(-4px);
  transform-origin: top left;
  transition:
    opacity var(--duration-fast) var(--ease-spring),
    transform var(--duration-fast) var(--ease-spring);
  pointer-events: none;
}

.dropdown-menu[data-open="true"] {
  opacity: 1;
  transform: scale(1) translateY(0);
  pointer-events: auto;
}
```

### Skeleton Shimmer
```css
@keyframes shimmer {
  from { background-position: -200% 0; }
  to { background-position: 200% 0; }
}

.skeleton {
  background: linear-gradient(
    90deg,
    var(--color-surface) 25%,
    var(--color-surface-raised) 50%,
    var(--color-surface) 75%
  );
  background-size: 200% 100%;
  animation: shimmer 1.5s ease-in-out infinite;
  border-radius: var(--radius-md);
}

.skeleton[data-loaded="true"] {
  animation: none;
  background: none;
}
```

### Focus Ring Scale
```css
:focus-visible {
  outline: 2px solid var(--color-primary);
  outline-offset: 2px;
  animation: focus-ring-in var(--duration-fast) var(--ease-spring);
}

@keyframes focus-ring-in {
  from { outline-offset: 6px; opacity: 0; }
  to { outline-offset: 2px; opacity: 1; }
}
```

### Number Count Animation (JS Helper)
```javascript
/**
 * Animates a number counting up/down with easing.
 * @param {HTMLElement} el - The element to update
 * @param {number} start - Starting value
 * @param {number} end - Ending value
 * @param {number} [duration=400] - Animation duration in ms
 */
function animateValue(el, start, end, duration = 400) {
  const range = end - start;
  const startTime = performance.now();

  function tick(now) {
    const elapsed = now - startTime;
    const progress = Math.min(elapsed / duration, 1);
    const eased = 1 - Math.pow(1 - progress, 3);
    const current = Math.round(start + range * eased);
    el.textContent = current.toLocaleString();
    if (progress < 1) requestAnimationFrame(tick);
  }

  requestAnimationFrame(tick);
}
```

---

## Page Animations (Landing Pages, Templates, Marketing Sites)

These animations transform a static page into a living, breathing experience.
Required for all landing pages, templates, and marketing sites.

### 1. Scroll-Triggered Reveals

Elements animate in as they enter the viewport. The foundation of any
page that feels alive.

#### CSS
```css
@keyframes reveal-up {
  from { opacity: 0; transform: translateY(40px); }
  to { opacity: 1; transform: translateY(0); }
}

@keyframes reveal-left {
  from { opacity: 0; transform: translateX(-40px); }
  to { opacity: 1; transform: translateX(0); }
}

@keyframes reveal-right {
  from { opacity: 0; transform: translateX(40px); }
  to { opacity: 1; transform: translateX(0); }
}

@keyframes reveal-scale {
  from { opacity: 0; transform: scale(0.9); }
  to { opacity: 1; transform: scale(1); }
}

[data-reveal] {
  opacity: 0;
  will-change: transform, opacity;
}

[data-reveal="up"].revealed {
  animation: reveal-up 0.8s var(--ease-spring) forwards;
}

[data-reveal="left"].revealed {
  animation: reveal-left 0.8s var(--ease-spring) forwards;
}

[data-reveal="right"].revealed {
  animation: reveal-right 0.8s var(--ease-spring) forwards;
}

[data-reveal="scale"].revealed {
  animation: reveal-scale 0.8s var(--ease-spring) forwards;
}

[data-reveal].revealed:nth-child(1) { animation-delay: 0ms; }
[data-reveal].revealed:nth-child(2) { animation-delay: 100ms; }
[data-reveal].revealed:nth-child(3) { animation-delay: 200ms; }
[data-reveal].revealed:nth-child(4) { animation-delay: 300ms; }
[data-reveal].revealed:nth-child(5) { animation-delay: 400ms; }
[data-reveal].revealed:nth-child(6) { animation-delay: 500ms; }
```

#### JavaScript
```javascript
/**
 * Initializes scroll-triggered reveal animations using IntersectionObserver.
 * Elements with data-reveal attribute get "revealed" class when in viewport.
 * @param {Object} [options={}] - Configuration options
 * @param {number} [options.threshold=0.15] - How much of element must be visible
 * @param {string} [options.rootMargin="0px 0px -50px 0px"] - Observer root margin
 */
function initScrollReveals(options = {}) {
  const { threshold = 0.15, rootMargin = '0px 0px -50px 0px' } = options;

  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('revealed');
        observer.unobserve(entry.target);
      }
    });
  }, { threshold, rootMargin });

  document.querySelectorAll('[data-reveal]').forEach(el => {
    observer.observe(el);
  });
}

document.addEventListener('DOMContentLoaded', () => initScrollReveals());
```

#### HTML Usage
```html
<section>
  <h2 data-reveal="up">This heading reveals on scroll</h2>
  <p data-reveal="up">This paragraph follows with a stagger</p>
  <div class="card-grid">
    <div class="card" data-reveal="up">Card 1</div>
    <div class="card" data-reveal="up">Card 2</div>
    <div class="card" data-reveal="up">Card 3</div>
  </div>
</section>
```

### 2. Text Reveal Animations

Text that reveals line-by-line or character-by-character creates a
cinematic reading experience. Essential for hero headlines.

#### Line-by-Line Mask Reveal
```css
.text-reveal-line {
  display: block;
  overflow: hidden;
}

.text-reveal-line > span {
  display: inline-block;
  transform: translateY(110%);
  transition: transform 0.8s var(--ease-spring);
}

.text-reveal-line.revealed > span {
  transform: translateY(0);
}

.text-reveal-line:nth-child(1) > span { transition-delay: 0ms; }
.text-reveal-line:nth-child(2) > span { transition-delay: 100ms; }
.text-reveal-line:nth-child(3) > span { transition-delay: 200ms; }
.text-reveal-line:nth-child(4) > span { transition-delay: 300ms; }
```

```html
<h1 class="hero-title">
  <span class="text-reveal-line"><span>We build</span></span>
  <span class="text-reveal-line"><span>digital products</span></span>
  <span class="text-reveal-line"><span>that matter.</span></span>
</h1>
```

#### Character-by-Character Stagger
```javascript
/**
 * Splits text into individual character spans for staggered animation.
 * @param {HTMLElement} el - The element containing text to split
 * @param {string} [className="char"] - CSS class for each character span
 * @returns {HTMLElement[]} Array of character span elements
 */
function splitTextIntoChars(el, className = 'char') {
  const text = el.textContent;
  el.textContent = '';
  el.setAttribute('aria-label', text);

  const chars = [];
  for (const char of text) {
    const span = document.createElement('span');
    span.className = className;
    span.textContent = char === ' ' ? '\u00A0' : char;
    span.style.display = 'inline-block';
    el.appendChild(span);
    chars.push(span);
  }
  return chars;
}

/**
 * Animates characters with staggered entrance.
 * @param {HTMLElement[]} chars - Array of character spans from splitTextIntoChars
 * @param {number} [stagger=30] - Delay between each character in ms
 */
function animateChars(chars, stagger = 30) {
  chars.forEach((char, i) => {
    char.style.opacity = '0';
    char.style.transform = 'translateY(20px)';
    char.style.transition = 'opacity 0.4s var(--ease-spring), transform 0.4s var(--ease-spring)';
    char.style.transitionDelay = `${i * stagger}ms`;

    requestAnimationFrame(() => {
      requestAnimationFrame(() => {
        char.style.opacity = '1';
        char.style.transform = 'translateY(0)';
      });
    });
  });
}
```

```css
.char {
  display: inline-block;
  will-change: transform, opacity;
}
```

### 3. Image Reveal Animations

Images that reveal with clip-path, scale masks, or blur-up create visual
drama. Essential for hero images and photo-heavy sections.

#### Clip-Path Circle Reveal
```css
.image-reveal {
  position: relative;
  overflow: hidden;
}

.image-reveal img {
  display: block;
  width: 100%;
  height: 100%;
  object-fit: cover;
  clip-path: circle(0% at 50% 50%);
  transition: clip-path 1.2s var(--ease-smooth);
}

.image-reveal.revealed img {
  clip-path: circle(75% at 50% 50%);
}
```

#### Scale Mask Reveal
```css
.image-reveal-scale {
  overflow: hidden;
}

.image-reveal-scale img {
  display: block;
  width: 100%;
  height: 100%;
  object-fit: cover;
  transform: scale(1.3);
  transition: transform 1.4s var(--ease-smooth);
}

.image-reveal-scale.revealed img {
  transform: scale(1);
}
```

#### Blur-Up Loading
```css
.image-blur-up {
  position: relative;
  overflow: hidden;
  background-color: var(--color-surface);
}

.image-blur-up .placeholder {
  position: absolute;
  inset: 0;
  filter: blur(20px);
  transform: scale(1.1);
  transition: opacity 0.6s var(--ease-smooth), filter 0.6s var(--ease-smooth);
}

.image-blur-up .full {
  position: absolute;
  inset: 0;
  opacity: 0;
  transition: opacity 0.6s var(--ease-smooth);
}

.image-blur-up.loaded .placeholder {
  opacity: 0;
  filter: blur(0);
}

.image-blur-up.loaded .full {
  opacity: 1;
}
```

```javascript
/**
 * Initializes blur-up image loading.
 * Swaps placeholder for full image when loaded.
 */
function initBlurUpImages() {
  document.querySelectorAll('.image-blur-up').forEach(container => {
    const fullImg = container.querySelector('.full');
    if (!fullImg) return;

    if (fullImg.complete) {
      container.classList.add('loaded');
    } else {
      fullImg.addEventListener('load', () => {
        container.classList.add('loaded');
      });
    }
  });
}
```

#### Ken Burns Effect
```css
@keyframes ken-burns {
  0% { transform: scale(1) translate(0, 0); }
  50% { transform: scale(1.1) translate(-2%, -1%); }
  100% { transform: scale(1) translate(0, 0); }
}

.hero-image img {
  animation: ken-burns 20s ease-in-out infinite;
  will-change: transform;
}

.hero-image:hover img {
  animation-play-state: paused;
}
```

### 4. Parallax Scrolling

Multi-layer depth where background elements move slower than foreground.
Creates a sense of depth and immersion.

```css
.parallax-container {
  position: relative;
  overflow: hidden;
}

.parallax-layer {
  position: absolute;
  inset: 0;
  will-change: transform;
}

.parallax-layer--back {
  transform: translateY(calc(var(--scroll-y) * 0.3));
}

.parallax-layer--mid {
  transform: translateY(calc(var(--scroll-y) * 0.6));
}

.parallax-layer--front {
  transform: translateY(calc(var(--scroll-y) * 1));
}
```

```javascript
/**
 * Initializes parallax scrolling effect.
 * Updates CSS custom property based on scroll position.
 * @param {string} [selector=".parallax-container"] - Container selector
 */
function initParallax(selector = '.parallax-container') {
  const containers = document.querySelectorAll(selector);

  function updateParallax() {
    const scrollY = window.scrollY;

    containers.forEach(container => {
      const rect = container.getBoundingClientRect();
      const centerY = rect.top + rect.height / 2;
      const offset = centerY - window.innerHeight / 2;

      container.style.setProperty('--scroll-y', `${offset}px`);
    });

    requestAnimationFrame(updateParallax);
  }

  requestAnimationFrame(updateParallax);
}

document.addEventListener('DOMContentLoaded', () => initParallax());
```

```html
<section class="parallax-container" style="height: 100vh;">
  <div class="parallax-layer parallax-layer--back">
    <img src="background.jpg" alt="" aria-hidden="true">
  </div>
  <div class="parallax-layer parallax-layer--front">
    <h2 data-reveal="up">Foreground content scrolls normally</h2>
  </div>
</section>
```

### 5. Magnetic Buttons

Buttons that follow the cursor within a radius, creating a magnetic pull
effect. Adds tactile delight to CTAs.

```javascript
/**
 * Initializes magnetic effect on elements.
 * Elements follow cursor within a defined radius on hover.
 * @param {string} [selector=".magnetic"] - Element selector
 * @param {number} [radius=0.3] - Magnetic pull strength (0 = none, 1 = full follow)
 */
function initMagneticButtons(selector = '.magnetic', radius = 0.3) {
  document.querySelectorAll(selector).forEach(el => {
    el.addEventListener('mousemove', (e) => {
      const rect = el.getBoundingClientRect();
      const x = e.clientX - rect.left - rect.width / 2;
      const y = e.clientY - rect.top - rect.height / 2;

      el.style.transform = `translate(${x * radius}px, ${y * radius}px)`;
      el.style.transition = 'transform 0.2s var(--ease-spring)';
    });

    el.addEventListener('mouseleave', () => {
      el.style.transform = 'translate(0, 0)';
      el.style.transition = 'transform 0.5s var(--ease-spring)';
    });
  });
}

document.addEventListener('DOMContentLoaded', () => initMagneticButtons());
```

```css
.magnetic {
  display: inline-block;
  will-change: transform;
  cursor: pointer;
}
```

### 6. Smooth Scrolling

```css
html {
  scroll-behavior: smooth;
}

html {
  scroll-snap-type: y proximity;
}

.snap-section {
  min-height: 100vh;
  scroll-snap-align: start;
}
```

```javascript
/**
 * Enhanced smooth scroll with anchor link support.
 */
function initSmoothScroll() {
  document.querySelectorAll('a[href^="#"]').forEach(link => {
    link.addEventListener('click', (e) => {
      const target = document.querySelector(link.getAttribute('href'));
      if (target) {
        e.preventDefault();
        target.scrollIntoView({ behavior: 'smooth', block: 'start' });
      }
    });
  });
}
```

### 7. Custom Cursor

A dot + circle cursor that follows the mouse and changes state on
interactive elements. Adds a premium, crafted feel.

```css
.custom-cursor {
  position: fixed;
  top: 0;
  left: 0;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: var(--color-primary);
  pointer-events: none;
  z-index: 9999;
  mix-blend-mode: difference;
  transform: translate(-50%, -50%);
  transition:
    width 0.3s var(--ease-spring),
    height 0.3s var(--ease-spring),
    background 0.3s var(--ease-spring);
}

.cursor-ring {
  position: fixed;
  top: 0;
  left: 0;
  width: 48px;
  height: 48px;
  border-radius: 50%;
  border: 1px solid var(--color-primary);
  pointer-events: none;
  z-index: 9998;
  transform: translate(-50%, -50%);
  transition:
    width 0.4s var(--ease-spring),
    height 0.4s var(--ease-spring),
    border-color 0.3s var(--ease-spring),
    opacity 0.3s var(--ease-spring);
}

.custom-cursor.hovering {
  width: 48px;
  height: 48px;
  background: var(--color-primary-muted);
}

.cursor-ring.hovering {
  width: 80px;
  height: 80px;
  opacity: 0.5;
}

.custom-cursor.clicking {
  transform: translate(-50%, -50%) scale(0.8);
}

@media (pointer: fine) {
  * { cursor: none !important; }
}

@media (pointer: coarse) {
  .custom-cursor, .cursor-ring { display: none; }
}
```

```javascript
/**
 * Initializes custom cursor with dot + ring.
 * Changes state on interactive element hover.
 */
function initCustomCursor() {
  if (window.matchMedia('(pointer: coarse)').matches) return;

  const dot = document.querySelector('.custom-cursor');
  const ring = document.querySelector('.cursor-ring');
  if (!dot || !ring) return;

  let mouseX = 0, mouseY = 0;
  let ringX = 0, ringY = 0;

  document.addEventListener('mousemove', (e) => {
    mouseX = e.clientX;
    mouseY = e.clientY;
    dot.style.left = `${mouseX}px`;
    dot.style.top = `${mouseY}px`;
  });

  function animateRing() {
    ringX += (mouseX - ringX) * 0.15;
    ringY += (mouseY - ringY) * 0.15;
    ring.style.left = `${ringX}px`;
    ring.style.top = `${ringY}px`;
    requestAnimationFrame(animateRing);
  }
  requestAnimationFrame(animateRing);

  const interactives = 'a, button, [role="button"], input, select, textarea, .card, .magnetic';
  document.querySelectorAll(interactives).forEach(el => {
    el.addEventListener('mouseenter', () => {
      dot.classList.add('hovering');
      ring.classList.add('hovering');
    });
    el.addEventListener('mouseleave', () => {
      dot.classList.remove('hovering');
      ring.classList.remove('hovering');
    });
  });

  document.addEventListener('mousedown', () => dot.classList.add('clicking'));
  document.addEventListener('mouseup', () => dot.classList.remove('clicking'));
}
```

```html
<div class="custom-cursor"></div>
<div class="cursor-ring"></div>
```

### 8. 3D Hover Transforms

Cards and elements that tilt in 3D based on mouse position. Creates a
tactile, physical feel for product showcases and card grids.

```javascript
/**
 * Initializes 3D tilt effect on elements.
 * Element rotates based on mouse position within its bounds.
 * @param {string} [selector=".tilt-card"] - Element selector
 * @param {number} [maxTilt=15] - Maximum tilt angle in degrees
 */
function init3DTilt(selector = '.tilt-card', maxTilt = 15) {
  document.querySelectorAll(selector).forEach(el => {
    el.addEventListener('mousemove', (e) => {
      const rect = el.getBoundingClientRect();
      const x = (e.clientX - rect.left) / rect.width;
      const y = (e.clientY - rect.top) / rect.height;

      const rotateX = (0.5 - y) * maxTilt;
      const rotateY = (x - 0.5) * maxTilt;

      el.style.transform = `perspective(800px) rotateX(${rotateX}deg) rotateY(${rotateY}deg) scale(1.02)`;
      el.style.transition = 'transform 0.1s ease-out';
    });

    el.addEventListener('mouseleave', () => {
      el.style.transform = 'perspective(800px) rotateX(0) rotateY(0) scale(1)';
      el.style.transition = 'transform 0.5s var(--ease-spring)';
    });
  });
}

document.addEventListener('DOMContentLoaded', () => init3DTilt());
```

```css
.tilt-card {
  transform-style: preserve-3d;
  will-change: transform;
}
```

### 9. Animated Gradient Backgrounds

Subtle hue-rotating gradients that breathe life into hero sections.
Use sparingly — one per page maximum.

```css
@keyframes gradient-shift {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

.animated-gradient {
  background: linear-gradient(
    135deg,
    var(--color-primary),
    var(--color-accent),
    var(--color-primary-muted),
    var(--color-accent-muted)
  );
  background-size: 300% 300%;
  animation: gradient-shift 12s ease infinite;
}
```

### 10. Data Visualization Animations (Charts & Graphs)

Charts and graphs MUST animate on load. These are the patterns for
SVG-based chart animations.

#### Bar Chart (Grow from bottom)
```css
@keyframes bar-grow {
  from { transform: scaleY(0); }
  to { transform: scaleY(1); }
}

.bar-chart rect.bar {
  transform-origin: bottom;
  animation: bar-grow 0.8s var(--ease-spring) forwards;
}

.bar-chart rect.bar:nth-child(1) { animation-delay: 0ms; }
.bar-chart rect.bar:nth-child(2) { animation-delay: 100ms; }
.bar-chart rect.bar:nth-child(3) { animation-delay: 200ms; }
.bar-chart rect.bar:nth-child(4) { animation-delay: 300ms; }
.bar-chart rect.bar:nth-child(5) { animation-delay: 400ms; }
.bar-chart rect.bar:nth-child(6) { animation-delay: 500ms; }
```

#### Line Chart (Draw path)
```css
@keyframes draw-line {
  from { stroke-dashoffset: var(--path-length); }
  to { stroke-dashoffset: 0; }
}

.line-chart path {
  stroke-dasharray: var(--path-length);
  stroke-dashoffset: var(--path-length);
  animation: draw-line 1.2s var(--ease-smooth) forwards;
}
```

```javascript
/**
 * Initializes line chart path drawing animation.
 * Calculates path length and sets it as CSS custom property.
 * @param {string} [selector=".line-chart path"] - Path selector
 */
function initLineChartAnimation(selector = '.line-chart path') {
  document.querySelectorAll(selector).forEach(path => {
    const length = path.getTotalLength();
    path.style.setProperty('--path-length', length);
  });
}
```

#### Donut Chart (Fill ring)
```css
@keyframes donut-fill {
  from { stroke-dashoffset: var(--circumference); }
  to { stroke-dashoffset: var(--target-offset); }
}

.donut-chart circle.progress {
  stroke-dasharray: var(--circumference);
  stroke-dashoffset: var(--circumference);
  animation: donut-fill 1s var(--ease-spring) forwards;
  transform: rotate(-90deg);
  transform-origin: 50% 50%;
}
```

```javascript
/**
 * Initializes donut chart fill animation.
 * Calculates circumference and target offset from data attributes.
 * @param {string} [selector=".donut-chart circle.progress"] - Circle selector
 */
function initDonutChartAnimation(selector = '.donut-chart circle.progress') {
  document.querySelectorAll(selector).forEach(circle => {
    const radius = parseFloat(circle.getAttribute('r'));
    const circumference = 2 * Math.PI * radius;
    const percent = parseFloat(circle.dataset.percent) || 0;
    const offset = circumference - (percent / 100) * circumference;

    circle.style.setProperty('--circumference', circumference);
    circle.style.setProperty('--target-offset', offset);
  });
}
```

#### Sparkline (Draw inline trend)
```css
.sparkline path {
  stroke-dasharray: var(--path-length);
  stroke-dashoffset: var(--path-length);
  animation: draw-line 0.8s var(--ease-smooth) forwards;
}
```

---

## Motion Tokens (Define All in CSS Custom Properties)

```css
:root {
  --ease-spring: cubic-bezier(0.23, 1, 0.32, 1);
  --ease-smooth: cubic-bezier(0.77, 0, 0.175, 1);
  --ease-bounce: cubic-bezier(0.34, 1.56, 0.64, 1);
  --duration-instant: 80ms;
  --duration-fast: 150ms;
  --duration-normal: 250ms;
  --duration-slow: 400ms;
  --duration-enter: 300ms var(--ease-spring);
  --duration-exit: 200ms var(--ease-smooth);
}
```

## Timing Guidelines

- **High-frequency** (hover, focus): 80–150ms. Must feel instant.
- **State changes** (toggle, tab, expand): 150–250ms. Snappy.
- **Layout transitions** (drawer, modal, page): 250–400ms. Smooth but not slow.
- **Entrance staggers** (grid load, list appear): 300–600ms total. Rhythmic.
- **Exit animations** (dismiss, remove): 150–250ms. Faster than entrance.
- **Scroll reveals**: 600–1000ms with stagger between elements.
- **Text reveals**: 400–800ms per line, 50–100ms stagger between lines.
- **Image reveals**: 600–1200ms with easing.
- **Parallax**: Continuous, tied to scroll position.

## What Motion Never Does

- Never loops idly (no floating blobs, infinite spinners on content).
- Never exists because the UI was generated by AI.
- Never slows interaction: input responsiveness is not delayed to "animate."
- Never covers a broken state transition.
- No excessive parallax, no random floating objects, no constant movement.
- No `transition: all`.
- No animating `width`, `height`, `margin`, `top`, `left`, `padding`, `border-radius`.

## Reduced Motion

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }

  .card:hover {
    transform: none;
  }

  .slide-over-panel {
    transition: none;
  }

  .parallax-layer {
    transform: none !important;
  }

  .custom-cursor,
  .cursor-ring {
    display: none;
  }

  .hero-image img {
    animation: none;
  }
}
```

Keep essential feedback (color changes, opacity) instant and non-kinetic.
Users who prefer reduced motion get the same information without motion.

## String-Tune Attribute-Driven Motion (Creative Branding Sites)

For high-variance creative templates and branding sites, integrate the attribute-driven, JS-light philosophy inspired by `@fiddle-digital/string-tune`. Rather than heavy JS frameworks, use data attributes to trigger interactions and control them using CSS variables.

### 1. Scroll Progress Indicator (`string="progress"`)
Bind scroll position to a CSS variable `--scroll-progress` globally.

```html
<div string="progress" class="progress-bar"></div>
```
```css
.progress-bar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 4px;
  background: var(--color-primary);
  transform: scaleX(var(--scroll-progress, 0));
  transform-origin: left;
  z-index: 1000;
}
```
```javascript
window.addEventListener('scroll', () => {
  const progress = window.scrollY / (document.documentElement.scrollHeight - window.innerHeight);
  document.documentElement.style.setProperty('--scroll-progress', progress);
});
```

### 2. Attribute Parallax (`string="parallax"`)
Declare movement directions directly on HTML elements using custom attributes.

```html
<div string="parallax" data-speed="0.2" data-direction="y">...</div>
<div string="parallax" data-speed="-0.1" data-direction="x">...</div>
```
```javascript
function initStringParallax() {
  const elements = document.querySelectorAll('[string="parallax"]');
  window.addEventListener('scroll', () => {
    const scrollY = window.scrollY;
    elements.forEach(el => {
      const speed = parseFloat(el.dataset.speed) || 0.1;
      const dir = el.dataset.direction === 'x' ? 'X' : 'Y';
      el.style.transform = `translate${dir}(${scrollY * speed}px)`;
    });
  });
}
```

### 3. Interactive SVG Pluck String Animation (Guitar String Effect)
An interactive SVG path that behaves like a physical string; it bends when the cursor crosses it and snaps back with spring physics.

```html
<svg class="pluck-string" viewBox="0 0 800 100">
  <path d="M 0 50 Q 400 50 800 50" fill="none" stroke="currentColor" stroke-width="2" />
</svg>
```
```javascript
function initPluckStrings() {
  const svg = document.querySelector('.pluck-string');
  const path = svg.querySelector('path');
  if (!svg || !path) return;

  let isHovered = false;
  let mouseX = 400, mouseY = 50;
  let y = 50;
  let targetY = 50;
  let vy = 0;
  const tension = 0.12; // spring tightness
  const friction = 0.88; // damper velocity loss

  svg.addEventListener('mousemove', (e) => {
    const rect = svg.getBoundingClientRect();
    mouseX = e.clientX - rect.left;
    mouseY = e.clientY - rect.top;
    
    // Pull line center vertically if cursor is close
    if (Math.abs(mouseY - 50) < 40) {
      isHovered = true;
      targetY = mouseY;
    }
  });

  svg.addEventListener('mouseleave', () => {
    isHovered = false;
    targetY = 50;
  });

  function update() {
    if (isHovered) {
      y += (targetY - y) * 0.2; // lag-follow cursor
    } else {
      let dy = targetY - y;
      let force = dy * tension;
      vy += force;
      vy *= friction;
      y += vy;
    }
    path.setAttribute('d', `M 0 50 Q ${mouseX} ${y} 800 50`);
    requestAnimationFrame(update);
  }
  update();
}
```

### 4. Elastic Letter String Physics (Interactive Signature Look)
Displaces individual letters based on cursor proximity, stretching and skewing characters vertically like rubber bands before snapping back.

```html
<h1 class="string-word">STRETCHY</h1>
```
```css
.string-word {
  display: flex;
  gap: 2px;
  cursor: default;
}
.string-word .char {
  display: inline-block;
  transform-origin: center bottom;
  will-change: transform;
}
```
```javascript
function initElasticLetters() {
  document.querySelectorAll('.string-word').forEach(word => {
    const text = word.textContent;
    word.textContent = '';
    
    const chars = [...text].map(char => {
      const span = document.createElement('span');
      span.className = 'char';
      span.textContent = char === ' ' ? '\u00A0' : char;
      word.appendChild(span);
      return { el: span, y: 0, vy: 0, targetY: 0 };
    });

    word.addEventListener('mousemove', (e) => {
      const rect = word.getBoundingClientRect();
      const mouseX = e.clientX - rect.left;
      const mouseY = e.clientY - rect.top;

      chars.forEach(char => {
        const charRect = char.el.getBoundingClientRect();
        const charX = charRect.left - rect.left + charRect.width / 2;
        const dist = Math.abs(mouseX - charX);
        const maxDist = 120; // radius of influence
        
        if (dist < maxDist) {
          const strength = 1 - dist / maxDist;
          char.targetY = strength * (mouseY - rect.height / 2) * 0.75;
        } else {
          char.targetY = 0;
        }
      });
    });

    word.addEventListener('mouseleave', () => {
      chars.forEach(char => char.targetY = 0);
    });

    const tension = 0.14;
    const friction = 0.84;

    function update() {
      chars.forEach(char => {
        let dy = char.targetY - char.y;
        char.vy += dy * tension;
        char.vy *= friction;
        char.y += char.vy;
        char.el.style.transform = `translateY(${char.y}px) skewY(${char.vy * 0.4}deg) scaleY(${1 + Math.abs(char.vy) * 0.01})`;
      });
      requestAnimationFrame(update);
    }
    update();
  });
}
```

---

## Principles

- **Snappy beats smooth.** Fast feedback feels premium.
- **Spring for enter, smooth for exit.** Enter with energy, leave with calm.
- **Stagger creates rhythm.** 30–100ms between items.
- **Every animation names its purpose.** If you can't say what it does for the user, delete it.
- **Hover states MUST animate.** A hover that just changes color without transition is dead.
- **Landing pages must feel alive.** Scroll reveals, text masks, and image reveals are mandatory.
- **Dashboards must feel responsive.** Chart animations, counter effects, and state transitions are mandatory.
