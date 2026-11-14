# Evidence: claims, checks, and honest limits

An opinionated methodology should be explainable **and falsifiable**. Rethink separates three kinds of statements:

1. **Direct properties of the naming grammar** — demonstrable without a user study.
2. **Checks against a specific implementation** — demonstrable with test fixtures and browser runs.
3. **Practical outcomes** — require comparative data from real projects.

## What the naming contract directly enables

| Property | Why it follows | How to check it |
| --- | --- | --- |
| Parseable identity | Given known breakpoint tokens, `class-variant-breakpoint` has defined segments | Parse a suite of valid and invalid names |
| Groupable responsive styles | Same class and variant share an output identity | Group style names and inspect resulting keys |
| Detectable missing pairs | Expected class/breakpoint pairs can be enumerated | Compare required versus present pairs |
| Detectable duplicate keys | Two styles map to same identity and breakpoint | Deliberately inject duplicates |
| Stable CSS family names | Removing the breakpoint suffix yields a shared identity | Inspect generated selector names |

These are testable properties, not proof of productivity improvement.

## What needs implementation validation

| Check | Evidence we should collect | Important limitation |
| --- | --- | --- |
| CSS accuracy | Computed browser properties at each authored anchor and nearby widths | CSS cascade and loaded fonts affect the result |
| Fixed/fluid behavior | Boundary and intermediate viewport tests | Interpolation may not reflect design intent |
| Migration safety | Conflict and rollback tests, Figma acceptance tests | In-session undo is not universal transaction safety |
| Rich-text selectors | Nested element fixtures and collision tests | Different CMS markup can require mapping changes |
| Accessibility | 200% resize, reflow, keyboard and contrast checks on real pages | Naming conventions are not WCAG guarantees |

## What we have not measured

Do **not** presently claim published percentages for:

- Faster design-to-development handoff.
- Fewer QA defects or less rework.
- Better team adoption than alternative methodologies.
- Reduced CSS byte size or runtime.
- Accessibility improvements.

The project has practical team usage reported by its creator, but that is background context, **not a controlled measurement**.

## A practical evidence protocol

For each permitted case study, record:

- Project type and size, anonymized where necessary.
- Number of distinct typography families and variants.
- Number of required and present breakpoint pairs.
- Manual mapping decisions and ambiguity reports before/after adoption.
- Review corrections and generated CSS verification failures.
- Who reviewed the data, which artifact versions were used, and any excluded examples.

Use the same definitions when comparing cases. Don't blend new sites with legacy refactors without acknowledging differences. If reporting time saved, define start/end events and avoid retrospective estimates presented as exact measurements.

## Reproducible examples before statistics

The first publishable evidence should be a small, permission-free fixture plus scripted checks that anyone can run. Start with [the worked example](examples/responsive-typography.md), then add machine-readable fixtures and an automated browser verification suite.

The next tier is anonymized real-system evidence, with permission and careful sampling. The final tier is a controlled comparison against existing team workflows. Results should report failures and cases where Rethink costs more work.

## External references

- [MDN: `clamp()`](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/clamp) — the CSS fluid-sizing primitive.
- [W3C: WCAG 2.2, Resize Text](https://www.w3.org/WAI/WCAG22/Understanding/resize-text.html) — accessibility requirements are separate from naming.
- [Design Tokens Format Module 2025.10](https://www.designtokens.org/TR/2025.10/format/) — a complementary interchange format, not something Rethink supersedes.

**Documentation rule:** label examples as illustrative, validation outcomes as measured, and unsupported benefits as hypotheses.
