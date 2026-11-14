# Developer guide: implementing the handoff

Rethink provides a stable mapping from designer-authored responsive text styles to one or more CSS selectors. It is independent of Webflow, although the accompanying generator targets common Webflow workflows.

## 1. Parse the identity, not just the string

Given:

~~~text
title1-1-mobile
title1-1-tablet
title1-1-desktop
~~~

the common implementation identity is `title1-1`. The breakpoint suffix selects a responsive data point; it is not part of the CSS class.

If your project has hyphenated breakpoint tokens (e.g. `desktop-xl`), parse against a **known breakpoint vocabulary** rather than assuming the last hyphen marks the suffix.

Figma folder paths may organize styles but should not affect the CSS identity.

## 2. Resolve duplicate keys before generation

The key `(class-variant, breakpoint)` should map to one design value for the stylesheet being generated. A duplicate across Figma folders can still create conflicting CSS output. If two styles genuinely need distinct values, assign them distinct CSS identities.

## 3. Establish implementation policy

Before generating or writing CSS, decide:

- Whether sizes change at discrete boundaries (fixed) or between anchors (fluid).
- Which breakpoint widths and media-query conventions apply.
- How missing design styles are treated: fallback, designer review, or explicit inferred suggestion.
- How Figma typefaces map to loaded web fonts and font weights.
- Whether classes, `rt-text-style` attributes, or both are used.
- How the generated stylesheet fits into the site's cascade and components.

## 4. Example fixed CSS mapping

The following is a **hand-written illustrative example**, not a byte-for-byte generator snapshot:

~~~css
.title1-1,
[rt-text-style="title1-1"] {
  font-family: var(--font-primary);
  font-weight: 600;
  font-size: 4rem;
  line-height: 1.1;
  letter-spacing: -0.02em;
}

@media screen and (max-width: 991.98px) {
  .title1-1,
  [rt-text-style="title1-1"] {
    font-size: 3rem;
  }
}

@media screen and (max-width: 479.98px) {
  .title1-1,
  [rt-text-style="title1-1"] {
    font-size: 2rem;
  }
}
~~~

This illustrates the **mapping**. Actual generated CSS can include additional declarations, helper selectors, or different media-query structures.

## 5. Use semantic markup independently

~~~html
<h1 class="title1-1">Page title</h1>
<h2 class="title1-1">Another heading, same visual treatment</h2>
<p class="body1-1">Supporting copy.</p>
~~~

A CSS class does not validate the heading hierarchy. Choose markup according to document structure and test accessibility separately.

## 6. Understand rich text

When the content management system renders nested HTML without per-element classes, the generator's optional helper stylesheet can map supported descendants to styles. The current development implementation uses an attribute such as:

~~~html
<div class="rich-text" rt-text-style-map="h2=title1-1, p=body1-1">
  <h2>Section heading</h2>
  <p>Paragraph text.</p>
</div>
~~~

This mapping is **tool-specific**, not part of the canonical name grammar. See [generator documentation](../generator.md) for status and limitations.

## 7. Verify in a browser

At minimum:

- Inspect computed font-size, font-family, weight, line-height, and letter-spacing at authored anchor widths.
- Check immediately below and above every breakpoint boundary.
- Test narrower and wider widths, including viewport gaps between anchors.
- Test 200% text resize, zoom, reflow, real content lengths, and unsupported font fallbacks.
- Check specificity and source order against existing utility and component styles.
- Confirm that explicitly missing styles follow the agreed fallback policy.

A stylesheet can be syntactically valid and still fail the handoff. Good validation compares **computed behavior** against the design decisions, not only generated CSS text.

## 8. Keep ownership clear

Designers specify typography decisions. Developers choose appropriate semantic markup, configure the cascade, and validate browser behavior. Automation helps carry the decisions across the boundary; it does not replace either role.
