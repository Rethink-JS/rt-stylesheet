# Philosophy: opinionated by design

Rethink starts from a recurring observation: **a design file can be visually clear yet technically ambiguous.** A name like “Large Hero Heading” communicates an impression, but not necessarily which tablet and mobile treatments belong to it, whether another heading is a variant, or which CSS selector should represent it.

That ambiguity is manageable in a small design. In a system repeatedly handed between designers and developers, it creates decisions that have to be rediscovered.

Rethink's answer is not to encode everything in a name. It encodes only three relationships that are especially important to responsive typography:

1. **Class:** the reusable typography family.
2. **Variant:** an intentional alternate treatment of that family.
3. **Breakpoint:** the viewport-specific representation of the treatment.

~~~text
title1-2-tablet
└────┘ │ └────┘
 class  │ breakpoint
        variant
~~~

The name is readable by a human and also parseable by software given a known breakpoint vocabulary.

## The principles

### 1. Make design decisions explicit

If two text styles belong to the same responsive family, the names should say so. If a new variant exists, it should represent a meaningful, reusable distinction. This moves the relationship from tacit team knowledge into the design artifact itself.

**Trade-off:** the designer follows a naming contract rather than naming styles however they like. Rethink accepts that cost because it makes the relationship inspectable.

### 2. Separate semantics from appearance

HTML `h1` is a structural heading level. `title1-1` is a visual typography treatment. They are not interchangeable. The same class can appear on different semantic elements when appropriate; the document must still have a meaningful semantic structure.

**Trade-off:** a developer cannot determine the correct HTML tag from a typography class. That is intentional.

### 3. Prefer reusable decisions over page-specific labels

A text style named after one homepage section is easy to introduce but hard to reuse. A stable typography family can be shared across pages and components without carrying a page name.

**Trade-off:** the family name alone may not explain every placement decision. Component documentation owns those decisions.

### 4. Treat variants as exceptions worth naming

Not every color, casing, emphasis, or one-off edit deserves a typography variant. A variant is appropriate when another treatment within the same family is deliberately reused or has distinct responsive behavior.

**Trade-off:** this needs judgment. Rethink defines a decision rule, not a magical classifier for design intent.

### 5. Keep breakpoint identity separate from CSS identity

Figma commonly needs explicit named styles at multiple breakpoints. A web implementation often needs **one** selector with multiple declarations/media-query rules. Removing the breakpoint suffix from the CSS identity bridges those representations.

**Trade-off:** a name alone does not determine media query ordering, interpolation, or accessible behavior. Those remain implementation and review concerns.

### 6. Automate the mechanical, review the inferred

An explicit `title1-1-tablet` can be grouped deterministically. If it is missing, a generator may propose a value, but that is a suggestion, not the original design decision. Designers remain accountable for approving inferred typography.

**Trade-off:** the system may refuse to decide when information is insufficient.

## What Rethink is not

- It is not a universal ontology of typography.
- It does not replace design tokens, HTML semantics, CSS cascade knowledge, or responsive layout design.
- It does not claim a particular number of breakpoint styles is always necessary.
- It does not guarantee pixel-perfect rendering, accessibility, or improved productivity merely by adopting the names.
- It does not require Webflow. Its naming model can inform any web implementation.

## Where it is useful

Rethink is strongest when a team has reusable responsive type families, a shared breakpoint policy, repeatable design-to-code handoffs, and a need to audit or generate mappings. For a single-page experiment or a highly dynamic type system driven entirely by CSS custom properties, a formal per-breakpoint naming contract may be unnecessary overhead.

**The core proposition:** choose a small amount of intentional structure at design time to remove avoidable ambiguity during implementation. The [evidence page](evidence.md) keeps that proposition separate from results that still need to be measured.
