# Workflow — Audit a Product

For reviewing an existing frontend product (a project the user wrote, one
another tool generated, or a previously generated Factory product). The audit
both reports and fixes.

## 0. Check the cache (before running anything)

If this is not the first audit on this project, read `caching/scope-narrowing.md`
and `caching/audit-cache.md` first. Determine:

- What audits are already cached and still valid (file unchanged, no
  dependency changed)?
- What audits need to run (file changed, dependency changed, or new file)?
- Did the user ask for a full re-audit? If so, clear the cache and run all.

Narrow the audit scope accordingly. Only run audits that aren't satisfied by
the cache. Report cached results transparently.

## 1. Scope

- Determine what is in scope: whole product, specific pages/components, or
  specific concerns (design only, accessibility only, etc.).
- If the user asks for a full audit, run all five audits. If they ask for a
  specific concern, run that one deeply and briefly scan the others.
- Cross-reference with the cache: skip audits that are still valid for
  unchanged files.

## 2. Run the audits

Apply the **quality/** modules in order:

1. `quality/code-audit.md` — structure, tokens, duplication, dependencies,
   naming, maintainability, performance, code commenting.
2. `quality/visual-audit.md` — design intent, hierarchy, identity, spacing
   rhythm, generic-AI fingerprints.
3. `quality/ux-audit.md` — task flows, feedback, states, content quality,
   information architecture.
4. `quality/responsive-audit.md` — behavior at every breakpoint, navigation,
   touch targets, table/form behavior.
5. `quality/accessibility-audit.md` — semantics, keyboard, focus, labels,
   ARIA, contrast, reduced motion.

Also apply `design/anti-generic.md` as a dedicated vibe-code sweep: when you
find a generic-AI pattern, flag it explicitly by name.

## 3. Classify findings

- **Blocking** — breaks core function, accessibility, or commercial viability
  (broken layout, keyboard trap, AA contrast failure, fake claims, generic
  product framing).
- **Major** — materially degrades quality (missing states, inconsistent spacing,
  unlabeled controls, dead code).
- **Minor** — polish (naming nits, minor inconsistencies).

## 4. Produce the audit report

Give the user a compact report:

- Overall assessment and score per concern (e.g., Pass / Conditional / Fail).
- Blocking findings first, then major, then minor — each with file/line where
  possible and the specific fix.
- A prioritized fix list (do this first → last).

## 5. Fix

If the user wants fixes applied, fix blocking and major findings before
anything else, and minor findings that are cheap. Do not stop at reporting —
apply `design/anti-generic.md`'s rule: when you find the problem, fix it.

## 6. Re-verify

After fixes, re-run the affected audits and confirm the findings are resolved.
Report what changed.

## Deliverables

- The audit report (scoped, prioritized, specific).
- Applied fixes with re-verification where the user requested fixes.
