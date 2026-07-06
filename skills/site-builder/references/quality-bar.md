# Quality bar — the award rubric as concrete checks

Awwwards juries score: **Design 40 · Usability 30 · Creativity 20 · Content 10** (a site goes to
18+ jurors; outliers are dropped). This file converts each category into pass/fail checks. Score
each check 0/1; a category passes at ≥ 85%. Fix and re-score until all four pass.

## Design (40%) — visual craft

- [ ] A written DIRECTION.md exists and the shipped site matches it
- [ ] Typography: distinctive display + body pairing (nothing from the banned-fonts list);
      fluid `clamp()` display sizes; line-length 45–75ch for body; consistent type scale
- [ ] Palette: 1 dominant + 1–2 accents used consistently; no orphan colors introduced ad hoc
- [ ] Spacing: single spacing scale; generous whitespace (award sites breathe — section padding
      typically ≥ 120px desktop / 64px mobile)
- [ ] Grid: intentional alignment everywhere; any broken-grid moment is deliberate and repeated
      as a motif, not an accident
- [ ] Imagery: consistent art direction across all images (the asset manifest's art-direction
      block enforces this); no mixed stock-photo styles
- [ ] Details: styled focus states, styled selection color (`::selection`), custom 404, favicon,
      OG image, no default blue links, no default form controls in key flows
- [ ] Dark/light: whichever mode shipped is fully committed (no half-themed components)
- [ ] **Screenshot test**: a 1440px hero screenshot could not be mistaken for a generic template

## Usability (30%) — flawless execution

- [ ] LCP < 2.5s, CLS < 0.1, INP < 200ms (measure with Lighthouse; run twice, throttled)
- [ ] 60fps scroll on a mid-range machine (Performance panel: no long frames during full-page scroll)
- [ ] JS ≤ ~300KB gzipped before any lazy-loaded WebGL bundle; fonts ≤ 2 families / 4 weights,
      WOFF2, preloaded, `font-display: swap`
- [ ] Every image: explicit dimensions, lazy below fold, AVIF/WebP
- [ ] Navigation is obvious within 3 seconds; current-page state visible; logo links home
- [ ] Fully keyboard navigable; visible (styled) focus rings; skip link; no keyboard traps from
      scroll-jacking
- [ ] Contrast: ≥ 4.5:1 body, ≥ 3:1 large text — including text over images/gradients
- [ ] `prefers-reduced-motion` leaves the site complete and beautiful, not broken
- [ ] Works at 360 / 768 / 1280 / 1920px; touch targets ≥ 44px; hover-only info has touch access
- [ ] Forms: labeled inputs, inline validation, meaningful success/error states
- [ ] No horizontal body scroll anywhere; no console errors

## Creativity (20%) — the memorable thing

- [ ] There is **one** identifiable creative risk (the DIRECTION.md "big swing") executed well —
      a signature interaction, a typographic system, a WebGL moment, a navigation concept
- [ ] Motion is choreographed (staggered phrases, one easing family), not template fade-ins
- [ ] At least 3 micro-interactions that reward attention (hover states, cursor behavior,
      easter egg, live element)
- [ ] The site does something the visitor hasn't seen this exact way before — name what it is;
      if you can't, return to Phase 1
- [ ] Trend use is deliberate: check trend-report-2026.md — nothing shipped that reads as
      "last year's template"

## Content (10%) — words and substance

- [ ] Zero lorem ipsum; copy has a voice matching the brand adjective set
- [ ] Headings are specific and confident (not "Welcome to our website")
- [ ] Every image has meaningful alt text (from the manifest)
- [ ] Microcopy is written (buttons, empty states, form errors, 404 page has personality)
- [ ] Meta: unique title/description per page, OG/Twitter cards render correctly
      (test with a card validator)

## Release gate

All four categories ≥ 85% AND: dev build has no errors, production build succeeds, `NOTES.md`
lists remaining placeholder assets + generation instructions, and the git history has meaningful
commits per phase.
