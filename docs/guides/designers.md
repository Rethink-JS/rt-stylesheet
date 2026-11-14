# Designer guide: from Figma styles to handoff

This workflow assumes a responsive website with several reusable text treatments. Use the [philosophy](../philosophy.md) and [naming specification](../naming.md) as the source of convention.

## Step 1 — Decide what is actually reusable

Audit the typography in your layouts. Group repeated treatments by their role in the design system: titles, body text, captions, labels, display, and similar families.

A style exists because the typography treatment is reused, not because a particular section happens to contain words.

## Step 2 — Assign stable families

Examples:

~~~text
title1
title2
body1
caption1
~~~

Do not assume that `title1` always maps to `h1` or is necessarily the largest text. Keep HTML semantics out of your style naming decisions.

## Step 3 — Introduce variants only when needed

Within `title1`, an alternate treatment might justify `title1-2` because it is intentionally used more than once or scales differently across responsive layouts.

Do not create variants solely for uppercase, a hover color, or occasional bold words inside body text. Record the reason for each meaningful variant in a typography reference frame.

## Step 4 — Agree on breakpoint policy

Agree with development on active viewport widths. The basic vocabulary is `mobile`, `tablet`, and `desktop`; extended breakpoints are available when the project needs them.

Names are not width definitions. Write down actual widths.

## Step 5 — Create the responsive styles

For a family with one variant:

~~~text
title1-1-desktop
title1-1-tablet
title1-1-mobile
~~~

Apply the appropriate typography values in each Figma text style: font family/style, weight, font size, line-height, and letter spacing.

Consistency matters more than any particular pixel scale.

## Step 6 — Review the style matrix

A small table is easier to audit than a long unstructured style list:

| CSS identity | Mobile | Tablet | Desktop |
| --- | --- | --- | --- |
| `title1-1` | Present | Present | Present |
| `body1-1` | Present | **Missing** | Present |
| `caption1-1` | Present | Present | Present |

A missing `body1-1-tablet` can be deliberate if the team has an explicit fallback policy. If not, resolve it before handoff. Do not assume a missing value is correct merely because a generator can infer one.

## Step 7 — Review legibility and content behavior

Check real copy rather than placeholder text. Test long headings, localization, headings with links, dense body text, and narrow viewports. Verify line-height, spacing, wrapping, and hierarchy, not font size alone.

## Step 8 — Hand off the decisions

A complete handoff includes:

- The style names and their intended class identities.
- The breakpoint width map and fixed/fluid sizing choice.
- Typography values for the required variants and breakpoints.
- Notes on intentional omissions, overrides, and special rich-text cases.
- A typography specimen or reference frame and representative pages.
- Any unapproved machine-generated suggestions clearly marked as such.

## Step 9 — Treat generation as assistance, not authority

The [Figma generator](../generator.md) can scan and organize local styles and propose missing variants. Review any inferred values in context, particularly at intermediate widths and at browser text zoom.

### Common mistakes

| Mistake | Better approach |
| --- | --- |
| `Hero Title Mobile` is unrelated to its desktop style by name | `title1-1-mobile` beside `title1-1-desktop` |
| Every bold phrase becomes a new text style | Use semantic inline emphasis where appropriate |
| `title1` is assumed to always be an HTML `h1` | Choose semantic markup independently |
| Breakpoint names are used without widths | Include a project breakpoint map |
| Generated missing styles are accepted silently | Mark inferred values and review them |
