# Frontend Product Factory

> An [opencode](https://opencode.ai) skill that turns one line of intent into **commercial-grade frontend products** — designed, animated, data-driven, audited, documented, and packaged for marketplaces.

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License: MIT"></a>
  <a href="https://opencode.ai"><img src="https://img.shields.io/badge/powered%20by-opencode-fa5c2c" alt="Powered by opencode"></a>
  <a href=".skills/"><img src="https://img.shields.io/badge/type-skill%20collection-e8a94d" alt="Skill collection"></a>
  <img src="https://img.shields.io/badge/dependencies-none-955f6a" alt="Zero dependencies">
</p>

---

## About

Frontend Product Factory is a **single AI skill, packaged as a reference library**, that makes an agent behave like a senior product engineer — someone who creates, refines, audits, productizes, documents, and packages frontend products that are *worth owning, using, and selling*.

It was written to end the two most common failures of AI-generated frontends: **generic, soulless output** and **portfolios of demos instead of products**. Every product it ships must feel alive and intentional, and must pass a six-stage anti-AI-slop evaluation before it can be called done.

It does not generate "a website." It **creates, refines, audits, productizes, documents, and packages** frontend digital products.

---

## Features

- **One-shot prompt resolution** — give it a product name or a single sentence; it infers the identity, typography, palette, and motion personality automatically. No interview, no setup.
- **Seven enforceable Laws** — purposeful animation, correct data-display patterns, anti-generic composition, mandatory data visualization, the right tech stack, an AI-slop firewall, and API-first data architecture.
- **Domain defaults** — a curated design-direction library for many industry domains, so every output has a native visual identity.
- **Name inference** — the product name is treated as a design brief in miniature and decoded before any code is written.
- **High-craft / immersive tier** — art direction, spatial composition, motion systems, parallax, and concept-driven 3D (raw Three.js), with their own audit workflow.
- **Data architecture** — real data contracts, mock API modes, CRUD lifecycles, and API state design instead of decorative placeholders.
- **Built-in QA** — code, visual, UX, responsive, accessibility, and performance audit workflows run the final product through review agents.
- **Marketplace readiness** — compliance, documentation, packaging, and screenshots guidance so outputs are actually *sellable*.

---

## What you can build

<table>
  <thead>
    <tr><th>Product type</th><th>Workflow</th><th>Technology</th></tr>
  </thead>
  <tbody>
    <tr><td>Single component (button, modal, chart, form field, nav, card)</td><td><code>workflows/create-component.md</code></td><td>HTML + CSS + JS</td></tr>
    <tr><td>Component collection / pack (form system, dashboard cards, data-viz kit)</td><td><code>workflows/create-component-collection.md</code></td><td>HTML + CSS + JS</td></tr>
    <tr><td>UI kit / admin dashboard / SaaS system</td><td><code>workflows/create-ui-kit.md</code></td><td>React (Next.js or Vite)</td></tr>
    <tr><td>Landing page / template / portfolio / e-commerce frontend</td><td><code>workflows/create-template.md</code></td><td>React (Next.js or Vite)</td></tr>
    <tr><td>Immersive / cinematic / art-directed / spatial brand experience</td><td><code>workflows/create-high-craft.md</code></td><td>Technology ladder from <code>design/motion-system.md</code></td></tr>
    <tr><td>Productize existing code into a sellable package</td><td><code>workflows/productize-existing-project.md</code></td><td>Depends on the existing stack</td></tr>
    <tr><td>Review, fix, or audit an existing product</td><td><code>workflows/audit-product.md</code></td><td>Depends on the existing stack</td></tr>
    <tr><td>Review a single component for quality</td><td><code>workflows/review-component.md</code></td><td>Depends on the existing stack</td></tr>
  </tbody>
</table>

---

## Showcase

Examples produced by this skill end-to-end (from a one-line prompt to a packaged, documented product):

<!--
  Drop proof screenshots here — e.g. in a `showcase/` folder:

  <p align="center">
    <img src="showcase/dashboard.png" alt="Example dashboard produced by the skill" width="49%">
    <img src="showcase/component-pack.png" alt="Example component collection produced by the skill" width="49%">
  </p>
-->

<p align="center">
  <em>Showcase images coming soon.</em>
</p>

---

## Installation

The skill is a plain folder of Markdown reference files. No packages, no build step, no runtime dependencies.

### Option A — per project (recommended to try it)

Copy the `.skills/` folder into any project root:

```bash
cp -r .skills /path/to/your-project/.skills
```

opencode discovers the skill and its triggers automatically.

### Option B — global opencode install (recommended to keep it)

Copy the **packaged** skill folder into opencode's global skills directory and register the included agents:

```bash
# distributed, dependency-light package (SKILL.md + minimal refs)
cp -r .skills/.opencode/skills/frontend-product-factory ~/.config/opencode/skills/

# full reference library
cp -r .skills ~/.config/opencode/
```

Then merge `opencode.json` into your opencode config to enable the bundled sub-agents (`design-reviewer`, `code-auditor`, `productizer`).

---

## Quick start

Open your agent, load the skill, and give it intent — not instructions:

```
Build a cold-chain monitoring dashboard
```

or just a name:

```
Build "Fieldnote"
```

From a single sentence it will:

1. **Classify** the request and route to the matching workflow.
2. **Infer design direction** from the name and domain defaults — stating its choice in one line, then proceeding (no clarifying-question round-trips).
3. **Implement** the product following the Seven Laws.
4. **Audit** it through the code, visual, UX, responsive, and accessibility passes.
5. **Package** it for sale — documentation, compliance notes, and marketplace guidance.

Requires the typical prompts; see [`Starter-Prompt.txt`](Starter-Prompt.txt) for the one-shot operating rules that glue the skill to an agent.

---

## How it works

### The Seven Laws (non-negotiable)

1. **Animation is purposeful** — motion guides attention and communicates state; it is spent like a budget, with tokens, staggered entrances, and a sacred `prefers-reduced-motion` contract.
2. **Choose the right data-display pattern** — card palette, master-detail slide-over, pipeline/kanban, rich list, or metric dashboard. Never table/default-everything.
3. **The UI must look human-designed** — an anti-generic blacklist enforces real imagery, domain identity, and no gradient-on-purple AI slop.
4. **Every dashboard visualizes data** — sparklines on every KPI, at least one animated SVG chart, responsive chart behavior.
5. **Pick technology by product** — component packs are dependency-free HTML/CSS/JS; sites and kits use React.
6. **The AI-slop firewall** — a six-stage evaluation (pattern, domain, component-replacement, content, interaction, composition) that any failing product must be redesigned for, never patched.
7. **Data architecture & API-first frontend** — let data shape the UI, model realistic API contracts, ship CRUD lifecycles and mock API modes.

Beyond the laws, the skill ships an **Originality Firewall**: never clone an existing site or reproduce a designer's identity — *learn the technique, invent the identity.*

### Included reference library

| Area | Files | Purpose |
|---|---|---|
| Design direction | `design/design-direction.md`, `design/name-inference.md`, `design/anti-generic.md`, `design/ai-slop-firewall.md`, `design/color.md`, `design/typography.md`, `design/motion*.md`, `design/landing-pages.md`, `design/3d-guidelines.md`, … | Domain defaults, typography and color systems, motion budgets, spatial composition, progressive enhancement, responsive rules |
| Quality | `quality/code-audit.md`, `quality/visual-audit.md`, `quality/ux-audit.md`, `quality/responsive-audit.md`, `quality/accessibility-audit.md`, `quality/high-craft-audit.md` | The audit passes every product must survive |
| Marketplace | `marketplace/compliance.md`, `marketplace/documentation.md`, `marketplace/packaging.md`, `marketplace/screenshots.md` | Making outputs sellable and license-clean |
| Caching | `caching/audit-cache.md`, `caching/change-detection.md`, `caching/scope-narrowing.md` | Reusable-audit bookkeeping so unchanged work is re-audited, not re-done |

### Bundled sub-agents

Defined in `opencode.json`, with read-only review permissions by default:

- **design-reviewer** — visual quality, anti-slop compliance, design-direction coherence.
- **code-auditor** — maintainability, design-system integrity, performance, technical quality.
- **productizer** — transforms existing frontends into marketplace-ready packages (this one is allowed to edit).

---

## Project structure

```
frontend-product-factory/
├── .skills/                         # the skill itself
│   ├── SKILL.md                     # entry point: scope discipline, the Seven Laws, workflows
│   ├── opencode.json                # config: skill paths + bundled sub-agents
│   ├── workflows/                   # per-product-type workflows (create, audit, productize, review)
│   ├── design/                      # design reference library (tokens, motion, anti-slop, 3D, …)
│   ├── quality/                     # audit passes: code, visual, UX, responsive, accessibility
│   ├── marketplace/                 # compliance, documentation, packaging, screenshots
│   ├── caching/                     # audit caching & change-detection reference
│   └── .opencode/
│       ├── agents/                  # design-reviewer, code-auditor, productizer
│       └── skills/frontend-product-factory/   # dependency-light distributable copy
├── Documentation/                   # product documentation
├── Starter-Prompt.txt               # one-shot operating rules for the agent
├── LICENSE                          # MIT
└── README.md
```

---

## Contributing

- **Bug reports / improvements** — open an issue or pull request against any reference file; each file is intentionally short and standalone.
- **New domain defaults** — the fastest way to make a visible impact: add a domain entry to `design/design-direction.md`.
- **New workflows** — follow the pattern of an existing `workflows/` file and reference it from `SKILL.md`.
- **Keep packages in sync** — the distributable copy under `.skills/.opencode/skills/frontend-product-factory/` should stay byte-identical to its sources; a CI check is welcome.

---

## License

[MIT](LICENSE) — Copyright (c) 2026 Frontend Product Factory.
