# Worked example: a three-breakpoint typography system

This example is **illustrative**, not a measured client project. It shows how the naming contract helps reveal responsive relationships and produce reusable CSS identities.

## 1. The design decisions

Suppose a website uses three visual treatments and the team agrees on:

~~~json
{
  "mobile": 480,
  "tablet": 992,
  "desktop": 1440
}
~~~

The Figma text styles:

| Figma text style | Font size | Relative line-height | CSS identity |
| --- | ---: | ---: | --- |
| `title1-1-mobile` | 32px | 1.15 | `title1-1` |
| `title1-1-tablet` | 44px | 1.12 | `title1-1` |
| `title1-1-desktop` | 64px | 1.10 | `title1-1` |
| `body1-1-mobile` | 16px | 1.50 | `body1-1` |
| `body1-1-tablet` | 18px | 1.50 | `body1-1` |
| `body1-1-desktop` | 20px | 1.50 | `body1-1` |
| `caption1-1-mobile` | 14px | 1.40 | `caption1-1` |
| `caption1-1-desktop` | 14px | 1.40 | `caption1-1` |

The caption lacks a tablet-specific style. That could mean "share the same value" or it could simply be an omission. The name contract **reveals the question**; it does not answer it.

## 2. Compute coverage

There are three unique CSS identities and three required breakpoints, so the matrix has nine possible identity/breakpoint pairs.

~~~text
3 identities × 3 breakpoints = 9 expected
8 present
1 missing
Coverage = 8 / 9 = 88.9%
~~~

That is a data-completeness measure, **not** an accessibility or visual-quality score. If the team explicitly excludes caption tablet as unnecessary, record that as an approved exception.

## 3. Review the naming

These names encode the same relationships better than the following informal list:

~~~text
Big Title
Big Title Tablet
Big Title Small
Regular Paragraph
Paragraph Small
Caption
Caption Mobile
~~~

The informal list may be readable but is not consistently parseable without assumptions. The canonical names disclose a precise class identity and breakpoint vocabulary.

## 4. Generate an implementation identity

Three title styles become one reusable selector:

~~~text
title1-1-mobile   ─┐
title1-1-tablet   ─┼──> .title1-1
title1-1-desktop  ─┘
~~~

A fixed output can use explicit media queries:

~~~css
.title1-1 {
  font-size: 4rem;     /* 64px at a 16px root */
  line-height: 1.1;
}

@media screen and (max-width: 991.98px) {
  .title1-1 {
    font-size: 2.75rem; /* 44px */
    line-height: 1.12;
  }
}

@media screen and (max-width: 479.98px) {
  .title1-1 {
    font-size: 2rem;    /* 32px */
    line-height: 1.15;
  }
}
~~~

This is a deliberately minimal *illustration*, not the full output of the Rethink generator. It omits font-family/weight declarations and the attribute-selector counterpart for readability.

## 5. Review the actual handoff

The designer confirms whether the caption should have an explicit tablet style and whether title sizes should transition in fixed steps or fluidly.

The developer confirms loaded webfonts, CSS source order, target markup, computed sizes at every anchor, and behavior at intermediate viewports and 200% text scaling.

The naming convention makes the correspondence visible, but **validation still happens in the rendered site**.

## 6. What this proves—and what it does not

This example demonstrates:

- Each name is mechanically groupable given a breakpoint vocabulary.
- A set of responsive design styles can share one stable CSS identity.
- Missing required identity/breakpoint pairs can be counted.
- A fixed CSS translation can preserve the listed font-size/line-height values at the example ranges.

It does not demonstrate that teams ship faster, that every design should have exactly three breakpoints, or that the output is automatically accessible. Those claims need the evaluation described in [evidence](../evidence.md).
