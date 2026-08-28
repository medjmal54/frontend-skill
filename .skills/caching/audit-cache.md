# Audit Cache

How to store, read, and update cached audit results so the skill never re-runs
an audit that is still valid. This is the core mechanism for avoiding token
waste on iterative prompts.

## Why this exists

Without caching, every prompt re-runs every audit on every file — burning
tokens re-checking typography that hasn't changed, security on files that
weren't touched, and spacing on components that weren't modified. Caching lets
the skill skip what's still valid and audit only what changed.

## The cache model

### What is cached

Audit results are cached **per file, per audit type**:

```
{
  "tokens.css": {
    "color-audit": { "status": "pass", "hash": "a3f2...", "timestamp": "2026-08-16T10:30:00Z" },
    "spacing-audit": { "status": "pass", "hash": "a3f2...", "timestamp": "2026-08-16T10:30:00Z" }
  },
  "metric-card.js": {
    "code-audit": { "status": "pass", "hash": "b7c1...", "timestamp": "2026-08-16T10:35:00Z" },
    "accessibility-audit": { "status": "pass", "hash": "b7c1...", "timestamp": "2026-08-16T10:35:00Z" }
  }
}
```

### What is NOT cached

- **Design direction** — always re-evaluated for coherence with changes.
- **Anti-generic checks** — always re-run on changed files (new changes can
  introduce generic patterns).
- **Visual audit** — always re-run on visually substantial changes (the
  "thumbnail test" depends on the whole, not parts).

## Storage: hybrid approach

### Session memory (fast access)

Store the current cache state in `/memories/session/audit-cache.md` for
instant access within the conversation. This is the primary read path —
the skill checks here first.

Format: a compact markdown table the skill can parse:

```markdown
# Audit Cache (Session)

| File | Audit | Status | Hash | Timestamp |
|------|-------|--------|------|-----------|
| tokens.css | color | pass | a3f2... | 2026-08-16T10:30 |
| tokens.css | spacing | pass | a3f2... | 2026-08-16T10:30 |
| metric-card.js | code | pass | b7c1... | 2026-08-16T10:35 |
| metric-card.js | a11y | pass | b7c1... | 2026-08-16T10:35 |
```

### Project file (persistence)

Mirror the cache to `.factory-cache/audit-state.json` inside the user's
project. This survives across sessions and lets a new conversation resume
without re-auditing everything.

```json
{
  "version": 1,
  "lastFullAudit": "2026-08-16T10:30:00Z",
  "files": {
    "tokens.css": {
      "hash": "a3f2e1...",
      "audits": {
        "color-audit": { "status": "pass", "timestamp": "2026-08-16T10:30:00Z" },
        "spacing-audit": { "status": "pass", "timestamp": "2026-08-16T10:30:00Z" }
      }
    }
  }
}
```

### Sync protocol

1. **On conversation start**: read `.factory-cache/audit-state.json` if it
   exists, load into session memory. If it doesn't exist, start empty.
2. **After each audit**: update session memory immediately, then write to
   the project file.
3. **On "re-audit all"**: clear both session memory and the project file,
   then run full audits.

## The cache entry

Each cached audit records:

- **File path** — relative to the project root.
- **Audit type** — which audit was run (color, spacing, typography, code,
  accessibility, responsive, visual, ux, security/compliance).
- **Status** — pass, conditional (with notes), or fail (with notes).
- **File hash** — a hash of the file content at audit time. Used to detect
  changes (see `change-detection.md`).
- **Timestamp** — when the audit was run.
- **Notes** — any conditions or caveats (e.g., "passes AA, but contrast is
  borderline at 4.6:1 — monitor if tokens change").

## Reading the cache

Before running any audit, the skill checks the cache:

1. Does this file have a cached result for this audit type?
2. Is the cached hash equal to the current file hash?
3. Is the cached status "pass" (or "conditional" with no new concerns)?
4. Has no dependency changed that would invalidate this audit? (See
   `change-detection.md` for dependency-aware invalidation.)

If all four are true: **skip the audit, report the cached result.**

If any is false: **run the audit, update the cache.**

## Writing the cache

After running an audit:

1. Compute the file hash.
2. Record the audit type, status, hash, and timestamp.
3. Update session memory.
4. Update the project file.

## Cache size management

- Remove entries for files that no longer exist (deleted or renamed).
- Keep only the latest result per file per audit type (no history).
- If the cache grows large (>100 files), summarize by component rather than
  by file.

## What the user sees

When the skill uses cached results, it reports them transparently:

```
✓ tokens.css — color audit: PASS (cached, file unchanged since last audit)
✓ tokens.css — spacing audit: PASS (cached, file unchanged since last audit)
→ metric-card.js — code audit: RUNNING (file changed since last audit)
```

Never silently skip an audit without telling the user it was cached.