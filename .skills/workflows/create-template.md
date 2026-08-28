# Workflow — Create a Template

For landing pages, landing-page kits, complete static templates, marketing
websites, portfolio templates, e-commerce frontend kits, and any
page-level product.

## 1. Product framing

- What is the template, concretely, and who is it for? (A portfolio for
  industrial designers, a landing kit for developer tools, an editorial site
  for a food brand...)
- What is the visitor's primary goal on this page/site?
- What is the conversion or outcome the template is designed to support?
- What makes it different from the hundreds of generic templates in the
  category?

If the user only says "landing page template", choose a concrete, differentiated
product (audience + purpose + personality) and state your decision.

## 2. Design direction

Read `design/design-direction.md`. Choose a visual language deliberately from
`design/design-diversity.md` based on audience, industry, and brand personality.
A template's entire value is a strong, coherent point of view. Read the
supporting **design/** modules before implementing.

## 3. Content strategy (before layout)

Templates fail on generic copy more than on anything else. Define the content:

- Realistic headings, body copy, and section content for the product type —
  never "Lorem ipsum", never "Feature 1 / Feature 2".
- Clearly fictional/demo framing for anything that could look like a real
  claim: "Example revenue", "Sample customer", "Demo workspace".
- No fake logos, fake testimonials, fake metrics, or invented trust signals.
- Content length variation: the template must hold up with short and long copy.

## 3b. Imagery strategy (before layout)

Every section needs visual content. Define the imagery approach:

- **Hero:** Full-bleed photo, gradient + image composition, or product UI showcase.
  Use unsplash.photos or pexels.com for placeholder photos.
- **Feature sections:** Supporting imagery — product screenshots, illustrations,
  or contextual photos. Never just icons on colored backgrounds.
- **Social proof:** Real-style company logos (use actual well-known logos with
  "Example" framing), team photos, or office/workspace images.
- **Footer/secondary:** Texture, pattern, or subtle background imagery.
- **Image treatments:** Define which sections use overlays, clip-path reveals,
  parallax depth, or Ken Burns effects. See `design/motion.md` for recipes.

## 4. Architecture

- Define pages/sections and their hierarchy.
- **Technology stack:** Use React (Next.js for multi-page, Vite + React for
  single-page). Templates and landing pages benefit from component composition,
  image optimization, and routing.
- Structure sections as reusable components with clear boundaries.
- Define the token system (typography, color, spacing, radii, elevation) so the
  template is one product, not an assembly.

**Code Commenting Requirements:**
- HTML files should have structural comments explaining major sections.
- CSS should have comments explaining token usage and component structure.
- JavaScript should have JSDoc comments for functions and inline comments for complex logic.
- Accessibility considerations should be noted in comments where relevant.

## 5. Design section by section

Every section gets a purpose in the page's story — do not repeat one card
treatment everywhere. Vary the information architecture:

- Hero/opening that matches the personality (not the generic centered-hero
  formula).
- Sections with different layouts: editorial columns, data-centric treatments,
  asymmetric grids, case-study layouts, a gallery, a comparison table — chosen
  for the content, not for variety's sake.
- Consistent spacing *philosophy* with deliberate rhythm, not identical padding
  everywhere.

## 6. Interactions

Add interactions only where they help: navigation, sticky behavior, progressive
disclosure (accordions), filters, small form interactions. Apply `design/motion.md`.

**Landing pages MUST use Level 2 or Level 3 animations** (see `design/motion.md`):
- Scroll-triggered reveals on every section (data-reveal attribute)
- Text reveal animations on hero headlines (line-by-line or character-by-character)
- Image reveal animations on hero and section images (clip-path, scale mask, or blur-up)
- Parallax depth on background elements
- Magnetic CTAs (primary call-to-action buttons)
- Smooth scrolling for anchor links
- Staggered entrance for card grids and feature lists

## 7. Responsive

Apply `design/responsive.md`. Page layouts must restructure on mobile: stacked
sections, transformed navigation, re-prioritized content, touch targets. Test
at mobile, tablet, desktop, and large desktop.

## 8. Accessibility

Apply `design/accessibility.md`: semantic structure, one logical h1, heading
hierarchy, keyboard navigation, focus visibility, contrast, reduced motion,
labeled forms, alt text.

## 9. Documentation

Per `marketplace/documentation.md`: what the template is, how to install, how to
customize (content, colors, fonts), structure overview, and demo instructions.

## 10. QA and packaging

Run `quality/visual-audit.md`, `quality/ux-audit.md`, `quality/responsive-audit.md`,
`quality/accessibility-audit.md`, `quality/code-audit.md`. Fix findings. Then
complete the **marketplace/** modules if the template will be distributed.

## Deliverables

- The template (pages/sections) with realistic content.
- Responsive, accessible, documented.
- QA results with fixes applied.
- Marketplace package where requested.
