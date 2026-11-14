# Naming specification

This page defines the **methodology contract**, not a claim that all existing Figma files or versions of the generator accept exactly the same syntax.

## Canonical form

~~~text
class-variant-breakpoint
~~~

Example:

~~~text
title1-1-desktop
title1-1-tablet
title1-1-mobile
~~~

All three resolve to the web-facing identity `title1-1`.

| Segment | Meaning | Example |
| --- | --- | --- |
| Class | Reusable typography family | `title1` |
| Variant | Positive integer identifying a deliberate alternate treatment within the family | `1` |
| Breakpoint | Name from a project's configured breakpoint vocabulary | `desktop` |

The canonical example `title1-2-desktop-xl` reads as family `title1`, variant `2`, breakpoint `desktop-xl`. Since breakpoint names themselves may contain hyphens, **do not parse by blindly splitting on the final hyphen**. Resolve the breakpoint against the configured vocabulary.

## Class

Use a short reusable family name such as `title1`, `body2`, `label1` or `caption1`. A family number is an identifier, **not a guaranteed rank** by physical size or an HTML heading level. Typography relationships and accessibility need to be reviewed independently of names.

Recommended: lowercase letters and digits with a recognizable family purpose. Avoid space-separated informal labels, casing-only variants, and location-specific names.

### Variant

Use `-1` for a family's first variant, `-2` for the next, and so on. Variants should exist only when there is a meaningful, intentionally reused distinction: e.g. an alternate weight, line-height, or responsive scaling behavior.

A different font family or substantially different desktop scale may be a new family instead of a variant. The choice is design intent, not something determinable from numerical similarity alone.

### Breakpoint

Default core names:

~~~text
mobile
tablet
desktop
~~~

The generator also recognizes expanded names including:

~~~text
mobile-xl
mobile-xxl
tablet-xl
tablet-xxl
desktop-xl
desktop-xxl
~~~

The breakpoint **widths are configurable**. The labels should not be mistaken for universal device categories. Every team should document the agreed width map and its media-query convention before implementation.

### Figma organization

Folders can organize style names without changing the CSS family identity:

~~~text
Typography/title1-1-desktop
Typography/title1-1-tablet
Typography/title1-1-mobile
~~~

The current generator can recognize both suffix-based names and slash-separated breakpoint variants. Use one style consistently in a project; the canonical written convention in this documentation is the suffix form.

## Identity and uniqueness

A responsive style can be identified by the pair:

~~~text
(class + variant, breakpoint)
~~~

For example `(title1-1, tablet)`.

Within a single stylesheet, that pair must be unambiguous. Two Figma folders must not silently define competing values for the same CSS identity and breakpoint. When multiple distinct style families would collapse onto one CSS selector, split them or resolve the collision during handoff.

## Completeness is relative to the project

For `N` variants and `B` required breakpoints, the expected count is `N × B`. A coverage figure can be calculated as:

~~~text
coverage = unique present required pairs / unique expected required pairs
~~~

This is a **coverage metric**, not a visual correctness score. A missing breakpoint can be intentional if a project defines a documented fallback or interpolation policy. Conversely, 100% named-style coverage does not ensure a good responsive design.

## What does not belong in the name

Usually keep these concerns separate:

- Semantic HTML hierarchy (`h1`–`h6`, `p`, `blockquote`).
- Text content and casing.
- One-off page placement or layout.
- Text color, decoration, and hover states.
- Inline `strong` and `em` emphasis inside a paragraph.
- Component-specific interaction states.

These can still affect presentation, but they should not automatically create new Rethink typography variants.

## Examples and anti-patterns

| Input | Assessment | Reason |
| --- | --- | --- |
| `title1-1-desktop` | Canonical | Explicit class, variant, breakpoint |
| `body2-2-mobile-xl` | Canonical | Supported expanded breakpoint shape |
| `Typography/title1-1-tablet` | Organized style | Folder is not part of selector identity |
| `Hero Heading Mobile` | Not canonical | Relationships require human interpretation |
| `homepage-hero-title-mobile` | Not recommended | Couples a reusable type identity to a page |
| `title1-2` | Incomplete | No explicit breakpoint under this contract |
| `title1-1-mobile` defined twice with different values | Conflict | One key maps to competing declarations |

For implementation specifics, see [developer guidance](guides/developers.md); for the reasoning behind the conventions, see [why the rules exist](why-the-rules.md).
