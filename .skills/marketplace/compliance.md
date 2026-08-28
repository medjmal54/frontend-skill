# Compliance

Identify compliance risks and unresolved manual checks. The goal is to help the
user ship without legal or marketplace surprises — never to give legal advice,
and never to claim guaranteed marketplace acceptance.

## License clarity

- The product needs a license. Use a placeholder with clear guidance until the
  user chooses one; never assert a specific legal license on the user's behalf.
- Every third-party component must be licensed compatibly with the product's
  intended distribution:
  - Code libraries (framework, utilities, build tools).
  - Fonts (many are licensed, including popular ones; self-hosted ≠ free).
  - Icons (icon sets have licenses; some require attribution, some don't
    permit resale).
  - Images/illustrations (stock assets may prohibit resale or redistribution).
    Unsplash and Pexels allow commercial use in digital templates without
    attribution, but images must be part of a larger creative work, not the
    standalone product. Neither provides indemnification. Document the source
    and advise buyers to replace with their own assets. Images with
    identifiable people may need model releases.
- Any vendored/copied code must carry its original license/attribution.

## Claim accuracy

- No fabricated testimonials, logos, metrics, awards, or "trusted by"
  claims (`design/anti-generic.md`).
- No claims about accessibility, performance, or compatibility the product has
  not been verified against. (Verified AA compliance can be stated if audited;
  otherwise say "designed to meet WCAG 2.1 AA" at most.)
- No trademark use implying affiliation (using real company names/logos as if
  the product is theirs).

## Demo data and privacy

- Demo data uses fictional framing and does not imply real people or real
  companies.
- No real personal data, emails, phone numbers, or credentials anywhere in the
  package, screenshots, or docs.

## Marketplace-specific rules (configurable)

Marketplace requirements change and differ per platform. Treat them as inputs:

- Ask for or recall the target marketplace (and check its current rules where
  possible) rather than assuming: preview requirements, file formats,
  acceptable licenses, exclusivity, use of trademarked names in titles/tags,
  allowed dependencies, and code-preview rules.
- Flag anything the product cannot currently satisfy as an explicit,
  unresolved manual check.

## Security hygiene

- No secrets, API keys, or tokens in the repository, demo, or docs.
- No baked-in credentials in demo data.
- No obvious XSS/injection-prone patterns in generated scripts.

## Manual checks that cannot be automated

List explicitly for the user, e.g.:

- Choosing and confirming the actual license.
- Confirming third-party license compatibility with the chosen marketplace.
- Verifying font/icon/image licenses.
- Re-reading marketplace terms at submission time.
- Any legal advice for their specific distribution.

## Documentation Compliance (HTML Format)

When documentation is delivered as HTML:

- [ ] HTML is valid and well-formed
- [ ] No external dependencies (all CSS/JS bundled or self-contained)
- [ ] Works offline (no external API calls for core functionality)
- [ ] Responsive design for all viewport sizes
- [ ] Accessible (semantic HTML, keyboard navigation, ARIA labels)
- [ ] No hardcoded values that should use tokens
- [ ] Screenshots match the actual product
- [ ] Code examples are accurate and tested
- [ ] No broken links or missing assets

## Sign-off

The package ships for review only when: licensing is either chosen or has a
clear placeholder with guidance, no fabricated claims exist, no real data is
included, and unresolved manual checks are documented.
