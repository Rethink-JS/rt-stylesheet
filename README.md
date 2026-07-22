# rt-stylesheet

A responsive typography methodology for cleaner design systems and predictable web handoff.

`rt-stylesheet` gives every responsive typography style a predictable structure:

```txt
class-variant-breakpoint
```

Example:

```txt
title1-1-desktop
title1-1-tablet
title1-1-mobile
```

This gives designers a clear way to organise responsive text styles, and gives developers a reliable way to turn those styles into CSS.

---

## Choose your path

### Designers

Use `rt-stylesheet` to create typography systems that are easier to organise, review, complete, and hand off.

You should care about it if:

- your design has separate desktop, tablet, and mobile typography
- your text styles are starting to feel messy or inconsistent
- you want a clear naming system that scales across a project
- you want developers to build the typography exactly as designed
- you want to quickly spot missing responsive styles

Start here: [For Designers](#for-designers)

### Developers

Use `rt-stylesheet` as a naming contract for converting design typography into predictable responsive CSS.

You should care about it if:

- design files contain many text styles with unclear relationships
- you need to map breakpoint-specific design styles to CSS classes
- you want class names, variants, and breakpoints to be parseable
- you want to validate typography coverage before implementation
- you want safer fixed or fluid CSS generation

Start here: [For Developers](#for-developers)


<br>
<br>

---

# For Designers

## What problem does this solve?

Typography in web design is not just one style.

A heading may be:

- 72px on large desktop screens
- 56px on desktop
- 42px on tablet
- 32px on mobile

A paragraph may keep the same size but change line-height. A hero title may use the same desktop size as another heading, but scale down differently on mobile.

Without a system, teams often create text styles like:

```txt
Hero Heading
Hero Heading Mobile
Large Heading
Large Heading Tablet
Section Title
Section Title Mobile
Body Copy
Body Copy Small
```

These names may make sense in the moment, but they do not clearly explain how the styles relate to each other.

`rt-stylesheet` makes those relationships explicit.

Instead of naming styles only by how they look or where they are used, you name them by how they belong to the typography system.

---

## The naming structure

Every responsive text style has three parts:

```txt
class-variant-breakpoint
```

Example:

```txt
title1-1-desktop
```

Read it like this:

```txt
title1   1        desktop
class    variant  breakpoint
```

---

## Class

The class describes the main typography level.

Examples:

```txt
title1
title2
title3
body1
body2
label1
caption1
eyebrow1
```

Use the class to describe the role of the style in the system.

For example:

```txt
title1
```

could be your largest heading style.

```txt
body1
```

could be your primary paragraph style.

The class should be reusable. Avoid tying it too tightly to a specific page or section.

Good:

```txt
title1-1-desktop
```

Avoid:

```txt
homepage-hero-heading-desktop
```

The first one belongs to a system. The second one belongs to a single layout.

---

## Variant

The variant is the number after the class.

Examples:

```txt
title1-1
title1-2
title1-3
```

Variants are useful when styles belong to the same typography family but need different responsive behaviour.

Example:

```txt
title1-1-desktop
title1-1-tablet
title1-1-mobile

title1-2-desktop
title1-2-tablet
title1-2-mobile
```

Both are `title1` styles, but they are different variants.

Use variants when:

- two headings share the same general role
- one heading needs different mobile scaling
- a layout needs an alternate version of an existing typography level
- you want to avoid inventing unrelated names for related styles

This keeps the system flexible without becoming messy.

---

## Breakpoint

The breakpoint describes the screen-size version of the style.

The default breakpoint set is:

```txt
desktop
tablet
mobile
```

A complete default group looks like this:

```txt
title1-1-desktop
title1-1-tablet
title1-1-mobile
```

That tells everyone these three styles belong together.

If a style group only has:

```txt
title1-1-desktop
title1-1-mobile
```

then it is easy to see that the tablet version may be missing.

---

## Expanded breakpoints

Some projects need more than desktop, tablet, and mobile.

`rt-stylesheet` can expand to support larger or more specific responsive systems.

Examples:

```txt
title1-1-desktop-xxl
title1-1-desktop-xl
title1-1-desktop
title1-1-tablet-xl
title1-1-tablet
title1-1-mobile-xl
title1-1-mobile
```

The same structure still applies:

```txt
class-variant-breakpoint
```

Only the breakpoint list grows.

This is useful for:

- large desktop screens
- editorial websites
- product interfaces
- kiosk or display layouts
- projects with custom responsive design requirements

---

## What a complete system looks like

A small system might look like this:

```txt
title1-1-desktop
title1-1-tablet
title1-1-mobile

title2-1-desktop
title2-1-tablet
title2-1-mobile

body1-1-desktop
body1-1-tablet
body1-1-mobile
```

A larger system might include variants:

```txt
title1-1-desktop
title1-1-tablet
title1-1-mobile

title1-2-desktop
title1-2-tablet
title1-2-mobile

title2-1-desktop
title2-1-tablet
title2-1-mobile

body1-1-desktop
body1-1-tablet
body1-1-mobile
```

The important part is consistency.

Once the structure is clear, the system can grow without changing the logic.

---

## Why this helps designers

### It makes responsive typography easier to review

You can immediately see which styles belong together.

```txt
title1-1-desktop
title1-1-tablet
title1-1-mobile
```

This is easier to audit than three unrelated names.

### It makes missing styles easier to spot

If your project uses desktop, tablet, and mobile styles, each class should usually have all three.

That makes missing styles obvious.

### It makes variants intentional

Instead of creating random alternate names, you can create structured variants.

```txt
title1-1
title1-2
title1-3
```

This keeps related styles grouped.

### It improves handoff

Developers do not need to guess which responsive styles belong together.

The structure already explains it.

### It scales cleanly

A naming system should work when the project grows.

`rt-stylesheet` works whether you have 9 text styles or 90.

---

## Designer checklist

Before handoff, check:

- Do all major typography classes have the breakpoint styles they need?
- Are variants intentional?
- Are one-off names avoided?
- Are class names reusable?
- Are desktop, tablet, and mobile styles clearly connected?
- Can someone understand the typography system without extra notes?


<br>
<br>

---

# For Developers

## What problem does this solve?

Design typography is often visually organised but technically ambiguous.

A design file might include styles like:

```txt
Hero Heading
Hero Heading Mobile
Large Heading Tablet
Section Title
Body Copy Small
```

These names are readable, but they are not reliably parseable.

From those names alone, a developer cannot safely infer:

- the CSS class name
- the breakpoint
- the responsive group
- the variant relationship
- whether the style set is complete
- whether CSS can be generated without manual mapping

`rt-stylesheet` solves this by turning responsive typography names into structured input data.

---

## Parseable structure

The structure is:

```txt
class-variant-breakpoint
```

Example:

```txt
title1-1-desktop
```

Parsed:

```json
{
  "class": "title1",
  "variant": "1",
  "breakpoint": "desktop"
}
```

Generated CSS selector:

```css
.title1-1
```

The breakpoint suffix determines where that style belongs in the responsive output.

---

## CSS mapping

A complete style group:

```txt
title1-1-desktop
title1-1-tablet
title1-1-mobile
```

can map to one responsive CSS class:

```css
.title1-1 {
  font-family: var(--font-primary);
  font-weight: 600;
  font-size: 4rem;
  line-height: 1.1;
  letter-spacing: -0.02em;
}

@media screen and (max-width: 991.98px) {
  .title1-1 {
    font-size: 3rem;
    line-height: 1.15;
  }
}

@media screen and (max-width: 479.98px) {
  .title1-1 {
    font-size: 2.25rem;
    line-height: 1.2;
  }
}
```

The exact CSS output can vary by project.

The value of the methodology is that the source names contain enough structure to generate this safely.

---

## Coverage validation

Because the names are structured, responsive coverage can be calculated.

Example:

```txt
8 class variants
3 breakpoints
```

Expected styles:

```txt
8 × 3 = 24
```

If 22 styles are detected:

```txt
22 / 24 = 91.67% coverage
```

Missing styles:

```txt
24 - 22 = 2
```

So the system can report:

```txt
24 expected styles
22 detected styles
2 missing styles
91.67% coverage
```

This is a practical technical advantage.

The naming is not only readable. It is measurable.

---

## Semantic compression

Design files often need explicit breakpoint-specific styles.

Code usually needs fewer responsive classes.

Example:

```txt
24 text styles
8 class variants
3 breakpoints
```

With `rt-stylesheet`:

```txt
24 breakpoint-specific text styles
→ 8 responsive CSS classes
```

Example:

```txt
title1-1-desktop
title1-1-tablet
title1-1-mobile
```

becomes:

```css
.title1-1
```

The breakpoint-specific values live inside the generated CSS rules.

---

## Breakpoint maps

Breakpoints are labels that can be mapped to viewport widths.

Example default map:

```json
{
  "mobile": 480,
  "tablet": 992,
  "desktop": 1440,
  "desktop-xl": 1920,
  "desktop-xxl": 3840
}
```

Example custom map:

```json
{
  "mobile": 390,
  "mobile-xl": 640,
  "tablet": 768,
  "desktop": 1280,
  "desktop-xl": 1440,
  "desktop-xxl": 1920
}
```

The naming model stays the same.

Only the breakpoint map changes.

---

## Fixed and fluid CSS

`rt-stylesheet` can support fixed responsive values or fluid interpolation.

### Fixed output

Fixed output applies the value defined for each breakpoint.

```css
.title1-1 {
  font-size: 4rem;
}

@media screen and (max-width: 991.98px) {
  .title1-1 {
    font-size: 3rem;
  }
}

@media screen and (max-width: 479.98px) {
  .title1-1 {
    font-size: 2.25rem;
  }
}
```

### Fluid output

Fluid output can interpolate between breakpoint values.

```css
.title1-1 {
  font-size: clamp(2.25rem, 1.5rem + 2vw, 4rem);
}
```

A structured naming system makes both approaches easier because each value belongs to a known class, variant, and breakpoint.

---

## Technical benefits

### Deterministic class generation

```txt
title1-1-desktop → .title1-1
title1-1-tablet  → .title1-1
title1-1-mobile  → .title1-1
```

### Missing style detection

Expected styles can be calculated from detected class variants and active breakpoints.

### Safer automation

Structured names can be scanned, grouped, validated, and converted into CSS without relying on fragile manual mapping.

### Breakpoint extensibility

The system supports additional breakpoints without changing the naming model.

### Clear handoff contract

Designers own the typography decisions.

Developers receive predictable implementation data.

---

## Comparison with common naming approaches

| Naming approach | Example | Designer-readable | Machine-parseable | Breakpoint-aware | Variant-aware | CSS-generation friendly |
| --- | --- | --- | --- | --- | --- | --- |
| Visual naming | `Hero Heading Mobile` | Yes | Weak | Inconsistent | Weak | Manual mapping needed |
| Page-specific naming | `Homepage Hero Title` | Yes | Weak | Weak | Weak | Tied to layout |
| Token-only naming | `font-size-heading-xl` | Medium | Strong | Needs extra structure | Weak | Partial |
| Utility naming | `text-48 leading-110` | Weak | Strong | Code-side only | Weak | Already implementation-focused |
| `rt-stylesheet` | `title1-1-mobile` | Yes | Strong | Yes | Yes | Yes |

`rt-stylesheet` is designed specifically for responsive typography handoff, where class identity, variant identity, and breakpoint identity need to stay connected.


<br>
<br>

---

# Rethink Stylesheet Generator

> **Coming soon:** The 'Rethink Stylesheet Generator' Figma plugin is not yet live.

Rethink Stylesheet Generator is the Figma plugin built to help teams apply the `rt-stylesheet` methodology faster and more accurately.

The plugin can:

- scan local text styles
- group responsive variants
- detect missing breakpoint styles
- generate missing text styles as a starting point
- map font families and font weights
- configure breakpoint widths
- generate fixed or fluid responsive CSS
- copy minified CSS
- download `rt-stylesheet.css`
- generate a polished typography stylesheet frame for handoff

---

## Plugin workflow

### 1. Create structured text styles

Create text styles using the methodology:

```txt
title1-1-desktop
title1-1-tablet
title1-1-mobile
```

### 2. Scan the file

Run the plugin and review:

- detected classes
- detected breakpoints
- responsive coverage
- missing styles
- fonts
- weights

### 3. Complete the system

If styles are missing, the plugin can generate suggested missing styles.

Generated styles are a starting point. Designers should review and refine them.

### 4. Configure output

Choose:

- fixed or fluid sizing
- breakpoint values
- font mappings
- root font size
- output filename
- stylesheet frame details

### 5. Export

Generate:

```txt
rt-stylesheet.css
```

and an editable typography stylesheet frame.

---

## Summary

For designers, `rt-stylesheet` creates clarity.

For developers, it creates parseability.

For teams, it creates a cleaner handoff between responsive typography decisions and production CSS.

```txt
class-variant-breakpoint
```
