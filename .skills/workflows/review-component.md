# Workflow — Component Review

For evaluating, improving, or validating components before they become part of a
sellable product. This ensures quality, consistency, and marketplace readiness.

## When to Use This

- Before packaging a component for marketplace distribution
- When reviewing existing components for quality gaps
- To validate that a component meets commercial standards
- As a checklist for component sign-off

## The Review Process

### 1. Component Identity Check

**What is this component, really?**
- [ ] Has a specific, concrete name (not "Card", "Section", "Wrapper")
- [ ] Solves a specific problem or supports a specific task
- [ ] Has a clear target user (developer implementing, end user interacting)
- [ ] Differentiates from similar components in the ecosystem

**Anti-Slop Check:**
- [ ] Does NOT use blacklisted fonts (Inter, Roboto, Arial, Space Grotesk)?
- [ ] Does NOT use blacklisted colors (purple/blue gradient on white)?
- [ ] Does NOT look like a generic template component?

**Example:**
- "A button component"
- "Primary CTA button for conversion-focused landing pages"

### 2. Design System Alignment

**Does it belong to a coherent system?**
- [ ] Uses design tokens (colors, spacing, typography, shadows)
- [ ] Follows the established shape language (radius scale)
- [ ] Respects the spacing philosophy (rhythm, not just consistency)
- [ ] Matches the visual personality of the product
- [ ] Has a documented place in the component hierarchy

**Anti-Slop Check:**
- [ ] Does NOT use blacklisted fonts from `design/typography.md`?
- [ ] Does NOT use blacklisted colors from `design/color.md`?
- [ ] Does the component have a distinctive identity that could be
  recognized in a thumbnail test?

### 3. API Quality Check

**Is the API clean and purposeful?**
- [ ] Props have clear, descriptive names
- [ ] Defaults are sensible and documented
- [ ] No prop explosion (too many similar props)
- [ ] Variants are use-case-driven, not color-driven
- [ ] Naming follows the project's conventions

**Variant Quality Test:**
- `color="red" | color="blue" | color="green"` (color variants) — wrong
- `intent="primary" | intent="secondary" | intent="destructive"` (meaning variants) — right

### 4. State Coverage

**Does it handle all expected states?**
- [ ] Default state (designed first, reference state)
- [ ] Hover state (with visual feedback)
- [ ] Active/Focus state (keyboard accessible, visible focus)
- [ ] Disabled state (clearly disabled, accessible)
- [ ] Loading state (if async operations possible)
- [ ] Error state (if applicable)
- [ ] Empty state (if applicable)

**State Communication:**
- [ ] States use multiple cues (color + shape + motion)
- [ ] Color alone is never the only indicator
- [ ] Focus is clearly visible and predictable

### 5. Content Tolerance

**Does it handle real-world content?**
- [ ] Long labels don't break the layout
- [ ] Short labels don't look awkward
- [ ] Numbers are properly formatted
- [ ] Empty strings are handled gracefully
- [ ] Very long strings wrap or truncate appropriately
- [ ] Mixed content (icons + text) is balanced

### 6. Accessibility Audit

**Is it accessible by default?**
- [ ] Semantic HTML (correct element for the job)
- [ ] Keyboard operable (tab, enter, escape where appropriate)
- [ ] Focus visible and predictable
- [ ] ARIA labels where native semantics are insufficient
- [ ] Color contrast passes AA at minimum
- [ ] `prefers-reduced-motion` respected if motion is used
- [ ] Screen reader announces states and changes

### 7. Responsive Behavior

**Does it work at all breakpoints?**
- [ ] Defined at sizes it will actually appear (mobile, tablet, desktop)
- [ ] Restructures meaningfully on small screens (not just shrinks)
- [ ] Touch targets are adequate (44px minimum)
- [ ] Content reflows appropriately
- [ ] No horizontal scroll introduced

### 8. Performance Check

**Is it performant?**
- [ ] No unnecessary dependencies
- [ ] Uses `transform`/`opacity` for animations (not `top`/`left`)
- [ ] No render loops or layout thrashing
- [ ] Efficient event handling (proper cleanup)
- [ ] Lazy loading where appropriate

### 9. Code Quality & Documentation

**Is the code well-documented and maintainable?**
- [ ] Functions have JSDoc comments explaining purpose, parameters, returns
- [ ] Complex logic has inline comments explaining the "why"
- [ ] Public APIs are documented with usage examples
- [ ] Accessibility considerations noted in comments where relevant
- [ ] Magic numbers explained or converted to tokens
- [ ] Variable names are descriptive and self-documenting
- [ ] Code follows consistent formatting and style

### 10. Animation & Motion Check

**Does it have purposeful motion?**
- [ ] Motion has a clear purpose (hierarchy, feedback, transition, disclosure)
- [ ] No idle loops or decorative animations
- [ ] Durations are short (150-300ms for states, up to 500ms for transitions)
- [ ] Uses `transform`/`opacity` for smooth, GPU-friendly animations
- [ ] `prefers-reduced-motion` is respected
- [ ] Motion enhances, not replaces, visual feedback

**Motion Quality Test:**
- Infinite spinners, floating blobs, decorative parallax — wrong
- Subtle hover effects, state transitions, focus animations — right

### 11. Documentation Quality

**Is it properly documented?**
- [ ] Purpose clearly stated
- [ ] Anatomy diagram or description
- [ ] All states and variants documented
- [ ] Props/API documented with types and defaults
- [ ] Code example with realistic content
- [ ] Customization guidance
- [ ] Accessibility notes

### 12. Marketplace Readiness

**Is it ready for distribution?**
- [ ] No hardcoded values (uses tokens)
- [ ] No secrets or credentials
- [ ] No fake claims or fabricated data
- [ ] License is clear or placeholder with guidance
- [ ] Screenshots would show it accurately
- [ ] Demo showcases all states

## Review Outcomes

### Pass
Component meets all criteria. Ready for packaging.

### Needs Revision
Component has issues. Fix before packaging:
- **Blocking**: Must fix before any release
- **Major**: Should fix for quality
- **Minor**: Polish items

### Reject
Component fundamentally doesn't meet standards. Redesign required.

## Review Template

Use this template to document reviews:

```markdown
# Component Review: [Component Name]

## Summary
**Status:** [Pass / Needs Revision / Reject]
**Date:** [Date]
**Reviewer:** [Name]

## Findings

### Blocking
- [ ] Issue 1: [description, file/line, fix]

### Major
- [ ] Issue 1: [description, file/line, fix]

### Minor
- [ ] Issue 1: [description, file/line, fix]

## Recommendations
[Action items for improvement]

## Next Steps
[What needs to happen before sign-off]
```

## Component Review Checklist

Quick checklist for rapid reviews:

- [ ] Specific, concrete name
- [ ] Solves a real problem
- [ ] Uses design tokens
- [ ] Clean, purposeful API
- [ ] Meaningful variants (not color variants)
- [ ] All states covered
- [ ] States use multiple cues
- [ ] Handles content variation
- [ ] Semantic HTML
- [ ] Keyboard accessible
- [ ] Visible focus
- [ ] AA contrast
- [ ] Responsive at all breakpoints
- [ ] No performance issues
- [ ] Well-commented code (JSDoc + inline)
- [ ] No blacklisted fonts (Inter, Roboto, Arial, Space Grotesk)
- [ ] No blacklisted colors (purple/blue gradient on white)
- [ ] Has distinctive identity (not cookie-cutter)
- [ ] Purposeful motion (if applicable)
- [ ] Fully documented
- [ ] Marketplace ready

## When to Review

| Stage | Purpose |
|-------|---------|
| Component creation | Validate before building |
| Component collection | Ensure cohesion across components |
| Pre-packaging | Final quality gate |
| Post-audit | Identify issues found by audit |
| Marketplace submission | Final verification |

## Integration with Other Workflows

### With Create Component Workflow
After completing steps 1-9 of `workflows/create-component.md`, run this
review to validate the component before documentation and packaging.

### With Create Component Collection Workflow
Review each component individually, then review the collection as a whole for
cohesion and shared system integrity.

### With Audit Product Workflow
Use this review to validate fixes after an audit identifies component issues.

### With Productize Existing Project Workflow
Review each component in the inventory to ensure it meets commercial standards
before packaging.
