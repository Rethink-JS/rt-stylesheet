# Rethink Stylesheet Generator

The **methodology** is the reusable naming and handoff contract. The **generator** is a separate Figma plugin that applies portions of that contract to local text styles and creates implementation artifacts.

Repository: [Rethink-JS/rt-stylesheet-generator](https://github.com/Rethink-JS/rt-stylesheet-generator). Access to its code may be restricted.

## Development capabilities reviewed

The generator's development README describes a v6.0.0 release prepared on 13 November 2026. That repository distinguishes the development release from the version actually published to Figma Community; the development version must not be treated as a verified public release.

Current development documentation and source include:

- Scanning and grouping responsive local text styles.
- Identifying incomplete responsive families and proposing missing styles.
- Configurable breakpoint widths, font mapping, and weight mapping.
- Fixed and piecewise fluid CSS generation.
- CSS class selectors and direct `rt-text-style` attribute selectors.
- Optional rich-text **CSS helper stylesheet**, `rt-stylesheet-helper.css`.
- Generating a typography reference frame in Figma.
- Opt-in naming migration with conservative suggestions, validation, provenance notes, and undo behavior.

The private generator repository also has automated regression-test source. Tests do not substitute for an independent browser and Figma acceptance pass.

## Example mapping

~~~text
Figma:
  title1-1-mobile
  title1-1-tablet
  title1-1-desktop

Implementation:
  .title1-1
  [rt-text-style="title1-1"]
~~~

For rich text, the helper stylesheet can use an element-to-style map:

~~~html
<div class="rich-text" rt-text-style-map="h2=title1-1, p=body1-1">
  <h2>Heading</h2>
  <p>Paragraph</p>
</div>
~~~

Note: the helper is a **CSS file** in the reviewed development version, not a JavaScript helper. Verify the plugin release used on your project before following version-specific instructions.

## What belongs in this repository

This repository documents **how to design and use the methodology**, with examples and stable conventions. The generator repository owns its versioned source, UI, build instructions, release packaging, and tool-specific bugs.

Changes to the methodology may require corresponding generator updates, but they should not be confused with already-shipped generator functionality.
