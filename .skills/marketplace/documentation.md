# Documentation

The documentation is part of the product. It must be accurate, useful, and
written for the buyer who is also a developer. Delivered as HTML for immediate
viewability.

## The Documentation Structure

### Folder: `documentation/`

All documentation is delivered as HTML files that can be opened directly in a
browser without any build tools or server required.

```
documentation/
├── index.html              # main documentation landing page
├── getting-started.html      # installation and setup guide
├── customization.html        # theming, tokens, extending
├── components.html         # component reference with examples
├── changelog.html            # version history
├── assets/
│   ├── docs.css            # styling for documentation
│   ├── docs.js             # interactive elements
│   └── images/             # screenshots, diagrams
└── templates/              # HTML templates for consistent structure
```

### HTML Documentation Standards

**File Structure:**
- Single HTML file per topic (no markdown in final product)
- Self-contained with embedded CSS or linked assets
- Responsive design for viewing on any device
- Search functionality (simple client-side search)

**Content Requirements:**

#### index.html (Landing Page)
- Product name and tagline
- Quick start guide (3-4 steps)
- Feature highlights with icons
- Component gallery preview
- Links to other documentation pages

#### getting-started.html
- Environment requirements
- Installation methods (npm, download, framework integration)
- Running the demo
- Folder structure overview
- First component usage example

#### customization.html
- Design token system (colors, typography, spacing)
- Dark/light mode setup
- Content replacement guide
- Adding new components
- Extension patterns

#### components.html
- Component catalog with cards
- Each component has:
  - Name and purpose
  - Visual preview (screenshot)
  - States gallery (hover, active, disabled, etc.)
  - Props/API table
  - Code example with syntax highlighting
  - Customization options
  - Accessibility notes

#### changelog.html
- Version history in reverse chronological order
- Added, Changed, Fixed, Removed sections
- Version numbers and dates

## Documentation Quality Standards

### Content Rules
- Clear, specific, and honest. No marketing fluff.
- Document only what exists; never invent capabilities.
- Errors in docs are blocking findings in an audit.
- Write for a competent developer who has never seen the product.

### Technical Standards
- Valid HTML5 markup
- Semantic structure (header, nav, main, section, article)
- Accessible (keyboard navigable, screen reader friendly)
- Responsive (works on mobile, tablet, desktop)
- Fast loading (optimized CSS/JS, lazy-loaded images)
- Code examples include comprehensive comments explaining usage and parameters

### Example Documentation Template

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>[Component Name] - Documentation</title>
  <link rel="stylesheet" href="assets/docs.css">
</head>
<body>
  <header>
    <nav aria-label="Documentation navigation">
      <!-- navigation links -->
    </nav>
  </header>
  
  <main>
    <article>
      <h1>[Component Name]</h1>
      <p>Purpose: [What this component does]</p>
      
      <section aria-labelledby="states-heading">
        <h2 id="states-heading">States</h2>
        <!-- state previews -->
      </section>
      
      <section aria-labelledby="usage-heading">
        <h2 id="usage-heading">Usage</h2>
        <pre><code class="language-html">&lt;!-- example code --&gt;</code></pre>
      </section>
      
      <section aria-labelledby="api-heading">
        <h2 id="api-heading">API</h2>
        <table>
          <!-- props table -->
        </table>
      </section>
    </article>
  </main>
</body>
</html>
```

## Documentation Generation

For maintainers: Documentation can be generated from markdown sources using
a build process that converts to HTML with consistent styling and navigation.

**Source Format (optional):**
- Markdown files in a `docs-src/` folder
- Build process converts to HTML in `documentation/`

**Manual Approach:**
- Write HTML directly for full control
- Use consistent templates across all pages
- Include all necessary assets for standalone viewing
