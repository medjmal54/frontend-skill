# Workflow — Productize an Existing Project

For turning existing code (a side project, an internal tool, a starter, a
half-finished kit) into a coherent, documented, distributable product.

## 1. Inventory and scope

- Map what exists: files, components, pages, features, dependencies.
- Determine what the product actually does and for whom.
- Decide what ships: everything, or a cleaned subset. Dead ends and half-baked
  features either get finished or get cut — a commercial product should not
  carry broken corners.
- State the deliverable scope explicitly so the user can correct it.

## 2. Differentiation assessment

Apply the product-thinking questions: does it solve a recognizable problem?
Is there enough depth? Is it more than a pile of components? If it is generic,
propose how to differentiate it before doing expensive work. A generic product
stays generic after a polish pass.

## 3. Tech assessment

- Verify the stack and dependencies: versions, licenses of third-party libs
  (see `marketplace/compliance.md`), unnecessary dependencies, build setup.
- Ensure the project builds/runs cleanly from scratch.
- Decide if the current architecture is worth keeping or should be simplified.

## 4. Extract the design system

- Identify hardcoded values (colors, spacing, radii, fonts, shadows) scattered
  through the code and centralize them into named tokens.
- Identify recurring patterns and unify them into shared components.
- Establish consistent naming and file structure.
- This step is what turns "someone's code" into "a product".

## 5. Clean up

- Remove dead code, unused dependencies, duplicated components.
- Fix inconsistent component boundaries.
- Apply `quality/code-audit.md` and resolve findings.
- Fix naming inconsistencies across the project.
- Add comprehensive code comments (JSDoc for functions, inline for complex logic).
- Ensure all magic values are documented or converted to tokens.

## 6. Design and UX pass

Run `quality/visual-audit.md`, `quality/ux-audit.md`, and
`design/anti-generic.md`. Fix what fails: hierarchy, spacing rhythm, states,
empty/loading/error handling, content quality (replace placeholder copy with
realistic content). The product must pass the visual quality gate before it is
packaged.

## 7. Responsive and accessibility passes

Apply `design/responsive.md` and `design/accessibility.md`, then run
`quality/responsive-audit.md` and `quality/accessibility-audit.md`. Fix
findings. These are the most common gaps in existing projects and the fastest
way to look unprofessional.

## 8. Demo and build setup

- Ensure a clean build and a runnable demo with realistic content.
- Document how to run and how to produce the distributable build.

## 9. Documentation

Write the full documentation set per `marketplace/documentation.md`:
what it is, installation, quick start, customization, component reference,
changelog, license placeholders.

## 10. Packaging and compliance

Complete the **marketplace/** modules: packaging structure, screenshot plan,
and compliance review (licensing of code, fonts, icons, images; demo-data
privacy; claim accuracy). List any manual checks that remain.

## Deliverables

- The productized codebase: cleaned, tokenized, documented, buildable.
- QA results with fixes applied.
- Marketplace package and screenshot plan where requested.
