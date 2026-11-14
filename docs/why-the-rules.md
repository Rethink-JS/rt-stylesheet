# Why the rules exist

An opinionated method should explain **why**, not ask for obedience. Each rule below identifies the recurring failure mode, its design response, and the cost of the response.

## 1. One reusable class, multiple design breakpoint styles

**Problem:** a designer supplies a desktop, tablet, and mobile style for one visual treatment. If names differ arbitrarily, a developer must manually reconstruct their relationship.

**Rule:** keep the family and variant stable, change only the breakpoint suffix.

~~~text
title1-1-desktop
title1-1-tablet
title1-1-mobile
~~~

**Consequence:** all three source styles map to `.title1-1` (or an equivalent attribute selector) with responsive CSS declarations.

**Trade-off:** the naming contract does not remove the need to check values, media-query ordering, or the effect of page-specific CSS.

## 2. A typography family is not an HTML tag

**Problem:** visual scale and document outline are different concerns. A small visual heading can still be a page's semantic `h1`; a display treatment need not be used for `h1`.

**Rule:** keep `title1` independent of `h1`.

**Consequence:** designers can adjust presentation without forcing changes to semantic document structure.

**Trade-off:** semantic correctness must be validated in markup, not inferred from typography names.

## 3. A variant must justify itself

**Problem:** teams accumulate nearly identical styles named “hero bold,” “hero caps,” or “hero final,” making the style library harder to audit.

**Rule:** make `-2` an explicit reused alternate treatment, not a dumping ground for any changed property.

**Examples:** a strong introductory body treatment that recurs across pages can be `body1-2`. An isolated bold phrase inside a paragraph remains `strong`, not `body1-3`. A change in text casing alone is normally outside the type family.

**Trade-off:** two reasonable designers can disagree about whether an alternate treatment is reusable enough. A short design-system note resolves that better than a fixed algorithm.

## 4. A family number is an identity, not a size promise

**Problem:** naming by visual size can become unstable when type scales change. Assuming `title1` must be the largest also conflates ordering with meaning.

**Rule:** numbers distinguish families; they are not CSS size comparators or semantic heading levels.

**Consequence:** names can remain stable even if a redesigned scale changes relative sizes.

**Trade-off:** unfamiliar teams may need a reference frame showing actual typographic sizes.

## 5. Breakpoint names are explicit, widths are configurable

**Problem:** “tablet” is not a universal CSS width. Two projects may have different responsive decisions.

**Rule:** use a stable breakpoint vocabulary and record the associated widths per project.

**Consequence:** the naming parser can remain constant while implementation values change.

**Trade-off:** breakpoint labels alone are insufficient for implementation; every handoff needs a width map and a policy for coverage/fallbacks.

## 6. Fixed and fluid sizing are both valid

**Problem:** fluid interpolation is useful but not always intended. A designer may want a step change, a constant value, or a nonlinear progression.

**Rule:** responsive identity is independent of the output policy. A generator may offer fixed values or piecewise fluid values.

**Consequence:** naming does not force a particular responsive algorithm.

**Trade-off:** the output strategy must be deliberately selected and tested. See [responsive sizing](responsive-sizing.md).

## 7. Missing styles are questions, not facts

**Problem:** when a tablet value is missing, interpolation can produce plausible typography while hiding that the value was never approved.

**Rule:** report missing values. Treat generated substitutes as suggestions, preserving which values came from the designer.

**Consequence:** handoff is more auditable.

**Trade-off:** filling gaps requires additional review.

## 8. Clear scope beats universal claims

Rethink is a **responsive typography handoff contract**, not a total CSS architecture. Existing token systems, utility classes, component libraries, and authoring tools solve related but different problems. A team can use Rethink alongside them.

### When not to use a rule mechanically

- Don't create three identical Figma styles just to score 100% coverage if the project explicitly uses a shared fallback.
- Don't create a new variant for every local layout exception.
- Don't assume generated `clamp()` output preserves user-selected font scaling.
- Don't rely on family naming to determine semantic HTML.

Use the [worked example](examples/responsive-typography.md) to see the mechanical benefit, then review [evidence and evaluation](evidence.md) for benefits that would need comparative testing.
