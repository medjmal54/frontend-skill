# Impressive Motion

Advanced animation concepts that make a product feel crafted, not generated.
These are the moments that make a buyer think "someone actually designed this."

## The principle

Every animation answers: **Does this make the user feel something?**

Not every animation needs to be loud. But every animation needs to be
intentional. The goal is moments of delight that make the product feel alive
and valuable — not a theme park of motion.

---

## Marquees & Tickers

Infinite horizontal scroll of content. Creates a sense of abundance and
constant activity.

### Use cases
- **News/data tickers** — scrolling headlines, live data feeds, status updates
- **Logo walls** — brand logos scrolling horizontally (not static grid)
- **Feature lists** — scrolling feature names or capabilities
- **Social proof** — scrolling testimonials, review snippets
- **Navigation alternatives** — horizontal menu for secondary navigation

### Implementation pattern
```css
.marquee {
  overflow: hidden;
  white-space: nowrap;
}
.marquee-track {
  display: inline-flex;
  animation: marquee 30s linear infinite;
}
.marquee:hover .marquee-track {
  animation-play-state: paused;
}
@keyframes marquee {
  0%   { transform: translateX(0); }
  100% { transform: translateX(-50%); }
}
```

### Rules
- **Duplicate content** for seamless loop (content appears twice)
- **Pause on hover** — let users read at their pace
- **Variable speeds** — not everything scrolls at the same rate
- **Different directions** — some marquees scroll left, some right, creates depth
- **Stack multiple** — two rows scrolling in opposite directions = visual richness
- **Content must be meaningful** — not filler text scrolling for the sake of motion

---

## Rotation & Spin

Controlled rotation that communicates state, identity, or playfulness.

### Use cases
- **Loading spinners** — custom branded spinners (not generic circles)
- **Card flip** — rotateY(180deg) to reveal back content
- **Icon rotation** — settings gear, refresh arrows, expand/collapse chevrons
- **3D perspective shifts** — subtle rotateX/rotateY on hover for depth
- **Badge/seal rotation** — slow continuous rotation on decorative elements
- **Number wheel** — vertical rotation for counting animations

### Implementation pattern — 3D card flip
```css
.card-flip {
  perspective: 1000px;
}
.card-flip-inner {
  transition: transform 0.6s var(--ease-spring);
  transform-style: preserve-3d;
}
.card-flip:hover .card-flip-inner {
  transform: rotateY(180deg);
}
.card-flip-front, .card-flip-back {
  backface-visibility: hidden;
  position: absolute;
  inset: 0;
}
.card-flip-back {
  transform: rotateY(180deg);
}
```

### Implementation pattern — perspective hover
```css
.card-3d {
  transition: transform 0.3s var(--ease-smooth);
}
.card-3d:hover {
  transform: perspective(800px) rotateX(2deg) rotateY(-3deg);
}
```

### Rules
- **Subtle wins** — 2–5 degrees of rotation on hover, not 45 degrees
- **3D only where depth exists** — don't apply perspective to flat cards
- **Smooth easing** — rotation must use spring or smooth easing, never linear
- **Purpose** — rotation communicates: this is interactive, this has depth,
  this is loading, this is transforming

---

## Scale Effects

Magnification, zoom, and proportional animation that draws attention.

### Use cases
- **Image zoom on hover** — scale(1.05) to scale(1.15) with overflow hidden
- **Magnifying glass** — cursor-following zoom on product images
- **Progress scale** — bars/rings that scale up when filling
- **Number scale** — large numbers that count up and scale into place
- **Card emphasis** — scale(1.02) on hover for subtle lift
- **Stagger scale entrance** — items scale from 0.8 to 1.0 with stagger
- **Minimap zoom** — scale down a full view into a navigable minimap

### Implementation pattern — image zoom
```css
.image-zoom {
  overflow: hidden;
}
.image-zoom img {
  transition: transform 0.5s var(--ease-smooth);
}
.image-zoom:hover img {
  transform: scale(1.12);
}
```

### Implementation pattern — stagger scale entrance
```css
.stagger-item {
  opacity: 0;
  transform: scale(0.85);
  animation: scaleIn 0.4s var(--ease-spring) forwards;
}
.stagger-item:nth-child(1) { animation-delay: 0ms; }
.stagger-item:nth-child(2) { animation-delay: 60ms; }
.stagger-item:nth-child(3) { animation-delay: 120ms; }
@keyframes scaleIn {
  to { opacity: 1; transform: scale(1); }
}
```

### Rules
- **Scale range: 0.95–1.12** — beyond that feels jarring
- **Transform-origin matters** — scale from center for cards, from edge for menus
- **Pair with opacity** — scale alone is weak; scale + fade is strong
- **Never scale text for emphasis** — use font-weight or size changes instead

---

## Text Reveal Animations

Making text appear letter-by-letter, word-by-word, or with masking effects.

### Use cases
- **Hero headings** — text that reveals as user scrolls or on page load
- **Split text** — each letter animates independently
- **Mask reveal** — text appears from behind a clipping mask
- **Typewriter** — text types out character by character
- **Blur resolve** — text starts blurred and sharpens into focus
- **Gradient text sweep** — gradient position animates across text

### Implementation pattern — mask reveal
```css
.text-reveal {
  overflow: hidden;
}
.text-reveal > * {
  transform: translateY(100%);
  animation: revealUp 0.6s var(--ease-spring) forwards;
}
@keyframes revealUp {
  to { transform: translateY(0); }
}
```

### Implementation pattern — split text stagger
```css
.split-text span {
  display: inline-block;
  opacity: 0;
  transform: translateY(20px);
  animation: splitIn 0.4s var(--ease-spring) forwards;
}
/* Each span gets increasing delay via JS or nth-child */
```

### Rules
- **Hero text only** — don't animate body text letter-by-letter
- **Speed: 300–600ms** — fast enough to feel snappy, slow enough to notice
- **Stagger 30–50ms** between letters/words
- **One reveal per page** — don't animate every heading this way

---

## Magnetic / Cursor-Following Effects

Elements that respond to cursor position, creating a sense of physicality.

### Use cases
- **Magnetic buttons** — button shifts toward cursor when nearby
- **Cursor trail** — subtle particle or glow following the cursor
- **Parallax mouse** — elements shift based on cursor position
- **Spotlight effect** — radial gradient follows cursor over content
- **Tilt cards** — card tilts based on cursor position (3D perspective)

### Implementation pattern — magnetic button
```js
const btn = document.querySelector('.magnetic-btn');
btn.addEventListener('mousemove', (e) => {
  const rect = btn.getBoundingClientRect();
  const x = e.clientX - rect.left - rect.width / 2;
  const y = e.clientY - rect.top - rect.height / 2;
  btn.style.transform = `translate(${x * 0.3}px, ${y * 0.3}px)`;
});
btn.addEventListener('mouseleave', () => {
  btn.style.transform = 'translate(0, 0)';
});
```

### Implementation pattern — spotlight
```css
.spotlight {
  background: radial-gradient(
    600px circle at var(--mouse-x) var(--mouse-y),
    rgba(255,255,255,0.06),
    transparent 40%
  );
}
```

### Rules
- **Subtle displacement** — 10–30% of cursor movement, not 100%
- **Smooth return** — elements ease back to origin on mouse leave
- **Desktop only** — cursor effects don't work on touch; provide fallback
- **Performance** — use `transform` only, never animate `left`/`top`

---

## Scroll-Linked Animations

Content that responds to scroll position, creating narrative and progression.

### Use cases
- **Progress bars** — fill as user scrolls through content
- **Parallax sections** — elements move at different scroll speeds
- **Sticky sections** — content pins while adjacent content scrolls past
- **Reveal on scroll** — elements animate in as they enter viewport
- **Counter animation** — numbers count up as they scroll into view
- **Horizontal scroll sections** — vertical scroll drives horizontal movement

### Implementation pattern — scroll-triggered counter
```js
function animateCounter(el, target) {
  const duration = 1500;
  const start = performance.now();
  function update(now) {
    const progress = Math.min((now - start) / duration, 1);
    const eased = 1 - Math.pow(1 - progress, 3);
    el.textContent = Math.floor(target * eased).toLocaleString();
    if (progress < 1) requestAnimationFrame(update);
  }
  requestAnimationFrame(update);
}

const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      animateCounter(entry.target, parseInt(entry.target.dataset.target));
      observer.unobserve(entry.target);
    }
  });
}, { threshold: 0.5 });
```

### Rules
- **One scroll effect per section** — don't stack parallax + reveal + counter
- **Performance** — use `IntersectionObserver`, not scroll event listeners
- **Reduced motion** — disable scroll-linked animations under prefers-reduced-motion
- **Mobile: simplify** — reduce parallax layers, skip cursor effects

---

## Number & Data Animations

Making data feel alive and valuable.

### Use cases
- **Count-up** — numbers animate from 0 to final value
- **Digit roll** — slot-machine style vertical digit rotation
- **Color flash** — value changes flash briefly in a color
- **Sparkline draw** — line chart draws itself on load
- **Progress fill** — bar/ring fills from 0 to value
- **Delta indicator** — up/down arrow with color for change

### Implementation pattern — digit roll
```css
.digit-roll {
  display: inline-block;
  overflow: hidden;
  height: 1em;
}
.digit-roll-inner {
  animation: rollUp 0.8s var(--ease-spring);
}
@keyframes rollUp {
  from { transform: translateY(-100%); }
  to   { transform: translateY(0); }
}
```

### Rules
- **Duration: 800–1500ms** — fast enough to not bore, slow enough to register
- **Easing: cubic-bezier(0.23, 1, 0.32, 1)** — spring feel
- **Only on load or value change** — don't re-animate on every render
- **Tabular figures** — numbers must use tabular-nums for alignment

---

## Component-Level Micro-Animations

Small animations on individual components that accumulate into a crafted feel.

### Tabs
- Active indicator slides to new position (200ms)
- Content crossfades (200ms)

### Toggles
- Thumb slides with spring easing (200ms)
- Background color morphs (150ms)

### Accordions
- Content height animates with `grid-template-rows` trick
- Chevron rotates 180deg (200ms)

### Dropdowns
- Menu scales from origin (0.95 → 1.0) + fades (150ms)
- Items stagger in (30ms each)

### Toasts / Notifications
- Slide in from edge (300ms spring)
- Auto-dismiss slide out after delay (200ms smooth)

### Tooltips
- Fade in + slight translateY(-4px) (150ms)
- Arrow appears with content

### Form validation
- Error message slides down from field (200ms)
- Field border color transitions (150ms)
- Check mark draws itself on success (300ms)

---

## Ambient Layered Motion

Multiple simultaneous subtle animations that create depth and life.

### Pattern: Three-layer ambient
```
Layer 1 (background): slow gradient rotation or blob drift (15–25s loop)
Layer 2 (midground):  floating elements with gentle translateY oscillation (4–6s loop)
Layer 3 (foreground): status indicators with pulse glow (2–3s loop)
```

All three run simultaneously. Each at a different speed. The result is an
interface that breathes without any single animation being noticeable.

### Pattern: Data dashboard ambient
```
Sparklines redraw every 5s with new data points
Status dots pulse gently
Progress bars shimmer slowly
Timestamps update
```

The dashboard feels alive — data is flowing, the system is active.

---

## Animation Density Rules

Not every component gets every animation. Choose based on importance.

| Component level | Animations allowed | Examples |
|---|---|---|
| **Hero / primary** | Full: entrance reveal, ambient, scroll, cursor | Landing page hero, main dashboard metric |
| **Secondary** | Moderate: hover effects, entrance stagger, one ambient | Feature cards, data panels |
| **Tertiary** | Minimal: hover lift, focus ring, transition | Form fields, list items, buttons |
| **Utility** | Feedback only: loading, success, error | Toasts, validation, spinners |

### The 3-second rule
If a user looks at a section for more than 3 seconds, there should be at
least one ambient animation running. If nothing moves, the section feels dead.

### The surprise budget
A product gets 2–3 "wow" moments per page. Not every section gets a
spectacular animation. Choose the moments that matter most and make those
impressive. The rest should be polished but quiet.

---

## What NOT to animate

- **Body text** — never animate text that users need to read
- **Form inputs** — never animate the input itself, only validation states
- **Navigation items** — hover effects only, no entrance animation
- **Data tables** — row transitions yes, cell-by-cell animation no
- **Scroll position** — never hijack scroll for animation
- **Cursor** — never change the cursor appearance for decoration
- **Page title** — never animate the browser tab
