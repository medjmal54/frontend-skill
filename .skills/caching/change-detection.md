# Change Detection

How to detect what changed between prompts so the skill can narrow audits to
only the affected areas. Uses two signals combined: prompt intent inference
and file hash comparison.

## Why two signals

- **Prompt intent** is fast but imprecise. "Change the button color" clearly
  affects the button, but the skill can't be sure it doesn't also affect
  tokens or other components.
- **File hashes** are precise but require reading files. They confirm what
  actually changed, not just what the user intended to change.

Combined: the skill uses prompt intent to narrow scope, then file hashes to
confirm what actually changed. This catches both "I changed more than I said"
and "I changed something unrelated."

## Signal 1: Prompt intent inference

### How it works

Analyze the user's prompt to infer the scope of changes:

| Prompt pattern | Inferred scope | Audits to run |
|---|---|---|
| "change [component] color/hover/spacing" | that component only | color/spacing/visual on that component |
| "add a new [component]" | the new component only | all audits on the new component |
| "change the font/typography" | tokens + all components using fonts | typography on all, visual on changed |
| "change the color palette/tokens" | tokens + all components | color on all, visual on all |
| "fix the responsive layout on [page]" | that page only | responsive on that page |
| "add dark mode" | tokens + all components | color, contrast, visual on all |
| "add a new page/section" | the new page only | all audits on the new page |
| "change the animation/motion" | affected components | motion, a11y (reduced-motion), visual |
| "fix accessibility on [component]" | that component only | accessibility on that component |
| "update the docs" | documentation only | documentation compliance only |
| "package for marketplace" | whole project | marketplace audits (packaging, compliance) |
| "re-audit everything" | whole project | all audits (ignore cache) |

### Scope levels

Classify the inferred scope into one of three levels:

- **Targeted** — affects 1-3 specific files/components. Skip all audits
  except those on the affected files.
- **System-wide** — affects tokens or shared infrastructure. Re-audit all
  components for the affected audit types (e.g., color change = re-audit
  color on all components).
- **Full** — affects the whole project or the user explicitly asked for a
  full audit. Run all audits.

### Inferring from keywords

| Keyword in prompt | Likely scope |
|---|---|
| "button", "card", "modal", "nav", specific component name | targeted |
| "color", "palette", "tokens", "theme", "dark mode" | system-wide |
| "font", "typography", "type scale" | system-wide |
| "spacing", "padding", "margin", "grid" | system-wide |
| "responsive", "mobile", "breakpoint" | targeted or system-wide (infer from context) |
| "accessibility", "a11y", "keyboard", "contrast" | targeted |
| "animation", "motion", "transition" | targeted |
| "new page", "new section", "add" | targeted (the new thing) |
| "redesign", "refactor", "restructure" | full |
| "package", "marketplace", "sell", "submit" | full (marketplace audits) |
| "fix", "bug", "broken" | targeted (the broken thing) |

## Signal 2: File hash comparison

### How it works

After each audit, the skill records a hash of each file's content. On the
next prompt, it re-hashes the files and compares:

1. **Read the cached hash** for each file from `.factory-cache/audit-state.json`.
2. **Compute the current hash** of each file.
3. **Compare**: if the hash matches, the file is unchanged. If it differs,
  the file changed and must be re-audited.

### What to hash

Hash the file content (not metadata). Use a simple, fast hash — the goal is
change detection, not cryptographic security. A simple string hash or
short checksum is sufficient.

### When to hash

- **After each audit** — record the hash of the audited file.
- **Before the next audit** — re-hash and compare to detect changes.
- **On "re-audit all"** — re-hash everything (forces re-audit of all).

## Combining the signals

### The decision flow

```
1. Infer scope from the prompt (targeted / system-wide / full).
2. If full: run all audits, ignore cache. Done.
3. If targeted:
   a. Identify the files/components the prompt affects.
   b. Hash those files and compare to cache.
   c. For each changed file: run the relevant audits.
   d. For each unchanged file: report cached results.
   e. Check dependencies (see below) — if a dependency changed, re-audit.
4. If system-wide:
   a. Identify the audit types affected (e.g., color change = color audits).
   b. Hash all files and compare to cache.
   c. For each changed file: run the affected audit types.
   d. For each unchanged file: report cached results for the affected types.
   e. Run non-affected audit types from cache (skip them).
```

### Example: "Change the button hover color"

1. Inferred scope: targeted (button component).
2. Files affected: `button.css`, possibly `tokens.css`.
3. Hash `button.css` — changed? Yes. Run color, visual audits on it.
4. Hash `tokens.css` — changed? No. Report cached color audit.
5. Check dependencies: does `button.css` depend on `tokens.css`? Yes, but
   `tokens.css` didn't change, so no cascade.
6. Result: only `button.css` re-audited. Everything else cached.

### Example: "Change the primary color in tokens"

1. Inferred scope: system-wide (color tokens).
2. Audit types affected: color, contrast, visual.
3. Hash all component files — most unchanged, but tokens changed.
4. Because tokens changed, invalidate color/contrast audits for ALL components
   (dependency-aware invalidation — see `audit-cache.md`).
5. Run color, contrast, visual audits on all components.
6. Skip code, responsive, accessibility (keyboard) audits — cached.

## Dependency-aware invalidation

Some files depend on others. When a dependency changes, or when the user changes a **Taste Dial Parameter** in the prompt (such as `DESIGN_VARIANCE`, `MOTION_INTENSITY`, or `VISUAL_DENSITY`), audits for dependent files must be invalidated even if the files themselves didn't change.

### Dependency map

| If this changes... | Invalidate these audits on... |
|---|---|
| `tokens.css` (color tokens) | color, contrast, visual audits on ALL components |
| `tokens.css` (spacing tokens) | spacing, visual audits on ALL components |
| `tokens.css` (typography tokens) | typography, visual audits on ALL components |
| `tokens.css` (motion tokens) | motion, a11y (reduced-motion) audits on ALL components |
| `tokens.css` (breakpoints) | responsive audits on ALL components |
| Shared primitives (e.g., `field.css`) | audits on composites using that primitive |
| `docs.css` | documentation compliance audit |
| **`DESIGN_VARIANCE` dial** | visual and responsive audits on ALL components |
| **`MOTION_INTENSITY` dial** | motion, a11y (reduced-motion), and visual audits on ALL components |
| **`VISUAL_DENSITY` dial** | spacing and visual audits on ALL components |

### How to detect dependencies

- **Explicit**: if a component imports/uses tokens, it depends on them.
  Most projects have a clear token file.
- **Implicit**: if a component's visual properties reference token names
  (CSS custom properties), it depends on those tokens.
- **State/Dial Shifts**: If the prompt changes a design system configuration parameter (dials), trigger invalidation rules immediately.
- **Conservative default**: when in doubt, assume a token or dial change affects all
  components. It's safer to re-audit than to skip.

## Edge cases

### New files

New files have no cached hash. Run all relevant audits on them.

### Deleted files

Remove their cache entries. No audit needed.

### Renamed files

Treat as deleted + new. Remove old cache entry, audit the new path.

### Files changed outside the skill

The hash comparison catches this — if the user edited a file manually, the
hash changes and the skill re-audits it.

### Ambiguous prompts

If the prompt is unclear ("make it better"), default to a broader scope
rather than skipping audits. When in doubt, audit more, not less.