# Rethink Stylesheet documentation

**Rethink Stylesheet is an opinionated methodology for structuring responsive typography decisions so that designers and developers can share an explicit, reviewable contract.** The methodology is the product; a Figma generator is one implementation of it.

Rethink deliberately solves a narrow problem: how a reusable typography treatment relates to its variants and breakpoint-specific values. It is **not** a complete CSS framework, layout system, HTML semantics guide, or design-token replacement.

## Start here

| Read this | If you want to… |
| --- | --- |
| [Philosophy](philosophy.md) | Understand the problem, principles, and deliberately chosen trade-offs |
| [Naming specification](naming.md) | Learn exactly what `class-variant-breakpoint` means |
| [Why the rules exist](why-the-rules.md) | See the rationale, alternatives, anti-patterns, and exceptions |
| [Designer guide](guides/designers.md) | Structure typography in Figma and prepare a handoff |
| [Developer guide](guides/developers.md) | Translate a responsive style family into implementation rules |
| [Responsive sizing](responsive-sizing.md) | Understand fixed versus fluid output and its limitations |
| [Worked example](examples/responsive-typography.md) | Follow a small design system from names to CSS |
| [Generator](generator.md) | Understand the Figma tool and distinguish it from the method |
| [Evidence and evaluation](evidence.md) | See which benefits follow mechanically and which require measurement |
| [Documentation roadmap](roadmap.md) | See what is documented and what remains to be built |

## What Rethink standardizes

A responsive style has a reusable family, an intentional variant, and a breakpoint identity:

~~~text
title1-1-desktop
title1-1-tablet
title1-1-mobile
~~~

These are three design representations of **one reusable CSS identity**: `title1-1`. The breakpoint is a property of the design specification, not part of the final class name.

## How to read these documents

- **Methodology rule:** a convention Rethink asks adopters to follow.
- **Implementation detail:** behavior of a particular tool or output mode; it may change between tool releases.
- **Demonstrated property:** a result that follows from the naming contract or can be checked against a concrete example.
- **Hypothesis:** a claimed productivity, quality, or maintainability benefit that must be evaluated with evidence.

The documentation avoids presenting hypotheses as measured results. Examples are illustrative unless attributed to a real, permissioned project.

## License and status

See the repository's [license](../LICENSE). This documentation is being expanded on a working branch. References to development generator features are not guarantees of what is available in the published Figma Community version.
