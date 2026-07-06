---
name: accessibility-compliance
description: Formal accessibility pass beyond the quality bar's baseline — WCAG 2.2 AA conformance audit, remediation, and an accessibility statement deliverable. Use when the client sells to the public sector or EU market, when compliance is named in the SOW, or when asked to audit/certify accessibility. Legal-exposure contexts (EAA, ADA, Section 508) make this mandatory scope, not optional polish.
---

# Accessibility Compliance

The quality bar's accessibility checks make a site *good*; this skill makes it *defensibly
conformant*. Premium clients increasingly carry legal obligations — the European
Accessibility Act applies to most consumer-facing e-commerce/services in the EU (in force
since June 2025), US clients face ADA litigation risk, and public-sector work requires it
outright. An agency that delivers a conformance audit + statement as standard is selling
risk reduction, which is exactly what agency pricing buys.

**Honesty rule:** you audit and remediate to WCAG 2.2 AA and document it. You do NOT
"certify" legal compliance — the statement discloses methodology and known limitations, and
recommends professional/user testing where warranted. Overclaiming is worse than a finding.

## Scope the pass

- Standard: **WCAG 2.2 AA** (the current baseline standard; AAA criteria only where cheap).
- Sample: every template (not every page) + every interactive component + the full primary
  journey(s) from ARCHITECTURE.md (landing → conversion, end to end).
- Track findings in `A11Y-AUDIT.md`: criterion · location · finding · severity
  (blocker/serious/moderate) · fix · status.

## The audit, in passes

**1. Automated sweep (catches ~30–40%, run first, never alone)**
axe-core (via Playwright — available in this environment) on every template, both themes,
mobile + desktop viewports. Also: Lighthouse a11y score per template, HTML validation
(landmarks, heading order, duplicate IDs).

**2. Keyboard journey (the highest-yield manual pass)**
Complete every primary journey keyboard-only: logical tab order · visible focus at every
stop (styled, per ui-patterns) · no traps (test every modal/drawer/overlay: focus in, Esc
out, focus returns to trigger) · skip link works · custom components (accordions, carousels,
menus) follow their ARIA pattern keystrokes (arrow keys where the pattern demands) · nothing
requires hover or precise pointer (2.5.7 dragging alternatives).

**3. Screen reader pass**
VoiceOver (or NVDA where available) through the primary journey: page title announced ·
landmark structure navigable · headings outline sensibly · images announce the manifest alt
text (decorative ones silenced with `alt=""`) · form fields announce label + error ·
dynamic updates (cart count, form success, toasts) announced via live regions — the classic
award-site failure: visually rich feedback that's silent to AT.

**4. Motion, media, time**
`prefers-reduced-motion` honored everywhere (motion-recipes §0 — verify, don't trust) · no
content flashing >3×/second · autoplaying video muted + pausable · carousels/marquees
pausable · no session/interaction time limits without extension · WebGL/canvas content has
a text alternative describing what it conveys.

**5. Visual/cognitive**
Contrast (4.5:1 / 3:1 incl. text-over-image at lightest point, focus indicators 3:1) ·
200% zoom without loss · 320px reflow without horizontal scroll · text-spacing override
survives · targets ≥ 24×24 CSS px (2.5.8) with the quality bar's 44px as the real goal ·
color never the only signal (form errors, links, states) · consistent nav/naming across
pages.

**6. Forms & auth**
Labels programmatic · errors identified + described + suggested fix · `autocomplete`
attributes on personal fields (1.3.5) · no cognitive test for auth (3.3.8 — magic links or
password managers fine, unassisted puzzles not) · redundant entry avoided (3.3.7).

## Award-site specials (where this library's genres create risk)

- **Custom cursors**: OS cursor never hidden for targets; effects are augmentation only.
- **Smooth-scroll/Lenis**: keyboard scroll, anchors, and find-in-page still work.
- **Pinned scrub scenes**: content readable at reduced-motion; scroll distance not a trap.
- **Overlay menus**: full focus management (ui-patterns spec) — audit every one.
- **Text as texture** (marquees, kinetic type): if it carries meaning, it's real text or
  has an alternative; if decorative, `aria-hidden` + not focusable.
- **Placeholder-driven builds**: manifest alt text ships WITH the placeholder, not later.

## Remediation

Fix by severity: blockers (journey-stopping) → serious (major friction) → moderate. Fix at
the token/component level (a focus-ring fix belongs in tokens, not per-page). Re-run passes
1–2 after; spot-check 3–6.

## Deliverable: the accessibility statement

`/accessibility` page + `A11Y-STATEMENT.md`, plain language:

conformance target (WCAG 2.2 AA) and audit date · methodology (automated + manual passes,
tools, sample) · known limitations with timelines (honest list from the audit's residue) ·
feedback channel (email + expected response time) · enforcement/escalation info where
jurisdiction requires (EU statements have prescribed content — check the client's member
state) · statement review date (6–12 months).

Log the audit + statement in LAUNCH.md and hand the re-audit cadence to the care retainer
(client-delivery): accessibility conformance decays with every content edit — a statement
with a stale date is a liability signpost.
