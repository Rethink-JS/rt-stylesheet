# Documentation and adoption roadmap

The goal is to turn the README-only methodology into a clear, maintained reference while keeping the original repository and its license recognizable.

## Phase 1 — Foundation (this branch)

- [x] Establish navigation, scope, and terminology.
- [x] Explain the opinionated principles and trade-offs.
- [x] Define canonical naming and identity rules.
- [x] Add designer/developer workflows and a worked example.
- [x] Separate generator capabilities from the methodology.
- [x] Maintain an evidence register rather than inventing results.
- [ ] Obtain a design-owner review of every normative rule and example.

## Phase 2 — Executable examples

- [ ] Add machine-readable fixtures for complete, sparse, duplicate, and conflicting style families.
- [ ] Add naming parser checks and coverage-report fixtures.
- [ ] Compare output with a pinned generator development version.
- [ ] Add browser checks for computed styles at anchor, boundary, and intermediate widths.
- [ ] Validate docs examples in CI so future edits cannot silently break them.

## Phase 3 — Applied guidance

- [ ] Add annotated Figma screenshots/reference frames where usage rights allow.
- [ ] Document Webflow setup as one implementation, not as a requirement.
- [ ] Add rich-text and multi-breakpoint edge-case guides.
- [ ] Document migrations, exceptions, troubleshooting, and version compatibility.
- [ ] Add a short decision tree for when a new style should be a family, variant, or utility.

## Phase 4 — Evidence

- [ ] Collect permissioned/anonymized real-world examples.
- [ ] Define repeatable handoff quality and effort metrics.
- [ ] Publish successes **and** failure modes.
- [ ] Distinguish lessons from team practice from generalizable claims.

## Phase 5 — Documentation site

When content and validation settle, migrate or expose these Markdown pages through a dedicated documentation site (Astro Starlight is one candidate). Keep GitHub pages readable and avoid locking the methodology to the site's framework.

No hosted site or Figma plugin release is implied by this roadmap.
