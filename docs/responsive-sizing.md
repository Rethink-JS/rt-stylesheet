# Responsive sizing: fixed, fluid, and explicit boundaries

Rethink's naming model identifies a typography style at a breakpoint. It does **not** prescribe how values behave between those breakpoints.

This distinction matters because teams sometimes treat all responsive typography as either strictly fixed or universally fluid. Both can be correct.

## Fixed values

A fixed interpretation sets a value at designated ranges. For example:

~~~css
.body1-1 { font-size: 2rem; }

@media (max-width: 991.98px) {
  .body1-1 { font-size: 1.75rem; }
}

@media (max-width: 479.98px) {
  .body1-1 { font-size: 1.5rem; }
}
~~~

This creates deliberate steps rather than continuous scaling. It is useful when the design calls for specific sizes across ranges or when interpolation would undermine hierarchy.

## Fluid interpolation

For two anchors, the straight-line interpolation can be expressed as:

~~~text
value(w) = a + (b - a) × (w - wa) / (wb - wa)
~~~

where `(wa, a)` and `(wb, b)` are viewport-width/value pairs.

For **24px at 480px** and **32px at 1440px**, assuming a 16px root font size:

~~~css
.body1-1 {
  font-size: clamp(
    1.5rem,
    calc(1.25rem + 0.833333vw),
    2rem
  );
}
~~~

At 480px the preferred expression gives approximately 24px, and at 1440px approximately 32px. The bounds prevent the font size from continuing to grow or shrink outside the intended range. This is an explanatory mathematical example; it is not a promise of the exact generated output of every plugin version.

For more than two authored anchors, a tool may use **piecewise** fluid functions with media queries so that adjacent pairs can have different slopes. The breakpoint ordering and cascade must be verified per style family, especially when some anchors are missing.

See [MDN's `clamp()` reference](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/clamp) for CSS semantics.

## What interpolation does not determine

Two anchor values do not prove that the designer intended a straight line. A visual treatment could legitimately:

- Remain fixed until a breakpoint.
- Interpolate nonlinearly.
- Use a different family weight or line-height at an intermediate width.
- Switch components entirely at some viewport.

Interpolation is a **policy**, not a recovered fact. The designer must approve it.

## Fallbacks and missing anchors

Suppose `title1-1-mobile` and `title1-1-desktop` exist, but `title1-1-tablet` does not.

The system should identify the missing row. The implementation then needs an explicit decision: use a known fallback, ask the designer for the value, or generate an inferred candidate and mark it for review.

The current generator can interpolate/extrapolate missing numerical values and use bounded heuristics with only one source style. Those are helpful workflow tools, but they are not evidence of the intended original value.

## Accessibility considerations

Using `rem` and `clamp()` is not a conformance guarantee. Combining `vw` with hard maximum/minimum constraints can interact with zoom and user font preferences. Test text at **200% resizing**, across the actual breakpoint changes, and verify that content and controls remain usable. See [WCAG 2.2 Understanding 1.4.4](https://www.w3.org/WAI/WCAG22/Understanding/resize-text.html).

## The contract in one sentence

**Naming tells us which values belong together; policy decides what happens between them; browser validation checks whether the implementation behaves as intended.**
