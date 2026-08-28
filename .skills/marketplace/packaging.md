# Marketplace Packaging

How to turn finished code into a complete, distributable package. Marketplace
specifics are configurable and updateable — never assume requirements; treat
them as inputs to verify.

## The package

A commercial product package contains, at minimum:

```
product/
├── source-code/          # source code (components, styles, scripts)
│   ├── src/              # component source files
│   ├── dist/             # prebuilt demo/build
│   └── demo/             # runnable showcase with realistic content
│
├── documentation/        # HTML documentation for buyers
│   ├── index.html        # main documentation landing page
│   ├── getting-started.html
│   ├── customization.html
│   ├── components.html   # component reference
│   ├── changelog.html
│   └── assets/           # CSS, JS, images for docs
├── LICENSE               # placeholder or chosen license
└── screenshots/          # marketing assets (see screenshots.md)
```

**Key Change:** Documentation is now delivered as HTML files in a dedicated
`documentation/` folder, making it immediately viewable without build tools.

Include: source, demo, documentation, changelog, feature list, license
placeholder. Exclude: node_modules, build artifacts, secrets, personal
configuration, anything not needed by the customer.

## Documentation requirements

Cover, per `marketplace/documentation.md`:

- What the product is and who it is for (specific, not "modern UI kit").
- Installation and quick start.
- Customization: colors, fonts, content, tokens, structure.
- Component/page reference.
- Changelog.
- License terms and what the customer may/may not do.

## Feature list and copy

- Feature list: accurate, specific, tied to what the code actually does.
- Copy never overclaims: no guaranteed outcomes, no fabricated testimonials,
  no invented stats (`design/anti-generic.md`).

## Versioning and releases

- Semantic versioning for the product; every release updates the changelog and
  version references consistently.

## Pricing recommendation framework

Provide a framework, not a promise. Guidance: compare against comparable
products in the target marketplace; price by scope (component count, page
count, demo depth, docs quality), target audience's willingness to pay, and
ongoing maintenance commitment. Recommend a price range and a rationale, and
note that the final decision belongs to the user. Never claim marketplace
acceptance or revenue.

## Title, description, tags

- Title candidates: specific and keyword-rich, but honest ("Operations
  Dashboard UI Kit for Logistics" not "The Best UI Kit Ever").
- HTML Description draft: states the problem, the solution, what is included, who
  it is for. Written in the buyer's language.
- Tags: the actual technology, product type, and use cases of the product.

## Submission checklist

- Package builds cleanly from a fresh checkout.
- Demo runs with realistic content.
- Docs match the actual product (no stale or invented features).
- License present and appropriate; third-party licenses documented.
- Screenshots match the product and follow `screenshots.md`.
- Compliance review completed (`compliance.md`).
- Code is well-commented (JSDoc for functions, inline comments for complex logic).
- Manual checks (marketplace-specific rules) explicitly listed as unresolved.
