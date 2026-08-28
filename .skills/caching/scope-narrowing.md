# Scope Narrowing

How to narrow audits to only the affected areas, so the skill runs the minimum
number of checks per prompt. This is the practical application of
`audit-cache.md` and `change-detection.md`.

## The principle

Audit only what could have changed. If a prompt touches one component, audit
that component. If it touches tokens, audit the affected audit types across
all components. If it touches nothing relevant, report cached results.

## The narrowing process

### Step 1: Classify the prompt scope

Read the user's prompt and classify it:

| Scope | When | Action |
|---|---|---|
| **Targeted** | Prompt affects 1-3 specific files/components | Audit only those files |
| **System-wide** | Prompt affects tokens or shared infrastructure | Audit affected types on all files |
| **Full** | Prompt affects the whole project or user says "re-audit all" | Run all audits, ignore cache |

### Step 2: Map audits to scope

Not every audit applies to every change. Map which audits are relevant:

| Change type | Audits to run | Audits to skip (cache) |
|---|---|---|
| Color change | color, contrast, visual | code, responsive, a11y (keyboard), motion |
| Spacing change | spacing, visual, responsive | code, a11y (contrast), motion |
| Typography change | typography, visual, a11y (contrast) | code, responsive, motion |
| Motion change | motion, a11y (reduced-motion), visual | code, color, spacing, responsive |
| New component | all audits on the new component | nothing (no cache for new files) |
| Component logic change | code, a11y, ux | color, spacing, typography, visual (unless UI changed) |
| Responsive fix | responsive, visual | code, color, spacing, a11y (unless markup changed) |
| Accessibility fix | a11y | code, color, spacing, typography, visual (unless UI changed) |
| Token change (color) | color, contrast, visual on ALL | code, responsive, a11y (keyboard), motion |
| Token change (spacing) | spacing, visual, responsive on ALL | code, color, a11y (contrast), motion |
| Token change (typography) | typography, visual, a11y (contrast) on ALL | code, responsive, motion |
| Token change (motion) | motion, a11y (reduced-motion) on ALL | code, color, spacing, responsive |
| Token change (breakpoints) | responsive on ALL | code, color, spacing, typography, motion |
| **`DESIGN_VARIANCE` dial** | visual, responsive on ALL | code, color, spacing, typography, motion, a11y |
| **`MOTION_INTENSITY` dial**| motion, visual, a11y (reduced-motion) on ALL | code, color, spacing, typography, responsive |
| **`VISUAL_DENSITY` dial**  | spacing, visual on ALL | code, color, typography, motion, responsive, a11y |
| Docs update | documentation compliance only | all component audits |
| Marketplace packaging | packaging, compliance, screenshots | all component audits (unless code changed) |

### Step 3: Check the cache

For each file and audit type in scope:

1. Does a cached result exist?
2. Does the file hash match (file unchanged)?
3. Has no dependency changed that would invalidate this audit?

If all three: **skip, report cached result.**

If any fails: **run the audit, update the cache.**

### Step 4: Run narrowed audits

Run only the audits that weren't satisfied by the cache. Report progress
transparently:

```
Audit scope: targeted (button component)

✓ tokens.css — color: PASS (cached, unchanged)
→ button.css — color: RUNNING (file changed)
→ button.css — visual: RUNNING (file changed)
✓ button.js — code: PASS (cached, unchanged)
✓ button.js — a11y: PASS (cached, unchanged)
✓ nav.css — color: PASS (cached, unchanged)
✓ nav.css — spacing: PASS (cached, unchanged)
[...skipped 12 more cached results...]
```

### Step 5: Update the cache

After running audits, update the cache for the files that were audited.
Files that weren't audited keep their existing cache entries.

## Scope narrowing by workflow

### Create Component

- **First creation**: no cache exists. Run all audits. Cache results.
- **Subsequent edits**: narrow to the changed files and relevant audit types.

### Create Component Collection

- **First creation**: run all audits on all components. Cache per file.
- **Adding a component**: audit only the new component. Cache it.
- **Editing a component**: audit only that component's changed files.
- **Token change**: re-audit affected types on all components.

### Create UI Kit

- **First creation**: run all audits on all files. Cache per file.
- **Editing a component**: narrow to that component.
- **Token change**: re-audit affected types on all components.
- **Adding a demo view**: audit only the new view.

### Create Template

- **First creation**: run all audits on all pages/sections. Cache per file.
- **Editing a section**: narrow to that section.
- **Token change**: re-audit affected types on all sections.
- **Adding a page**: audit only the new page.

### Productize Existing Project

- **First run**: no cache exists. Run all audits. Cache results.
- **Subsequent edits**: narrow to changed files.

### Audit Product

- **Full audit request**: ignore cache, run all audits, update cache.
- **Specific concern**: run only that audit type, update cache for those files.
- **"Re-audit all"**: clear cache, run all audits, rebuild cache.

## When NOT to narrow

Always run full audits (ignore cache) when:

- The user explicitly asks for a full audit ("re-audit everything").
- The project has no cache yet (first run).
- The cache file is corrupted or missing.
- The skill detects a major structural change (new file organization, renamed
  files, deleted components) that makes the cache unreliable.
- The user switched branches or reverted changes (hashes may match but the
  context changed).

## The "minimum viable audit" principle

When in doubt about whether to audit or cache, ask:

> "Could this change have affected the property being audited?"

- If yes: audit.
- If no: cache.
- If unsure: audit (safer).

The goal is to skip audits that are definitely still valid, not to skip
audits that might be invalid. When in doubt, audit more, not less.

## Reporting to the user

Always be transparent about what was cached vs. audited:

```
Audit Summary
─────────────
Scope: targeted (button component)
Files audited: 2 (button.css, button.js)
Files cached: 14 (unchanged since last audit)
Audits run: 4 (color, visual on button.css; code, a11y on button.js)
Audits cached: 22

Result: PASS — all audited files pass. Cached results remain valid.
```

This builds trust: the user knows the skill isn't silently skipping checks.