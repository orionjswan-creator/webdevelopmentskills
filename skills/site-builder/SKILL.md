---
name: site-builder
description: Build a complete, award-quality website from a content brief, a chosen style skill, and an asset manifest. Designed for Claude Sonnet 5 / Codex 5.5. Use when asked to build, scaffold, redesign, or "make an award-winning" website. Runs a 10-phase pipeline ending in a self-scored QA pass against award-jury criteria.
---

# Site Builder

You are building a website to the standard of Awwwards SOTD / FWA / CSSDA winners. Juries score
**Design 40% · Usability 30% · Creativity 20% · Content 10%** — beauty matters most, but a site
that stutters, confuses, or loads slowly loses. Your job: original design, flawless execution.

**Inputs** (gather in Phase 0 — never skip):
1. A content brief (brand, audience, pages, tone)
2. A style skill from `skills/styles/` (defines aesthetic + stack)
3. `assets/manifest.md` if it exists (from the asset-creation skill) — otherwise you'll stub it

**Output**: a running site, with every image slot wired to a manifest ID, that passes
`references/quality-bar.md`.

## Non-negotiable rules

- **Patterns, not clones.** Replicate techniques and quality from award winners — never a specific
  site's copy, logo, brand colors, or imagery. Everything you ship is original to this brand.
- **Direction before code.** You commit to a written aesthetic direction (Phase 1) before the
  first line of markup. No "default Tailwind look."
- **Font policy.** Never use overused defaults: Inter, Roboto, Arial, Helvetica, Poppins,
  Montserrat, Open Sans, Lato, Raleway, Space Grotesk, system-ui as the brand face. Pick
  distinctive open fonts (Fontshare, Google's deeper catalog) — each style skill suggests pairings.
- **Never block on assets.** Missing image → labeled placeholder + manifest entry, keep building.
- **Motion respects `prefers-reduced-motion`** and holds 60fps on a mid-range laptop.
- **Trends are seasoning, not the meal.** Check `references/trend-report-2026.md` for what's
  current and what's already dated — but the style skill's core system always wins conflicts.

## The pipeline

Work the phases in order. Each has a "gate" — don't advance until it passes.

### Phase 0 — Brief

Fill this template from the user's request; ask (or infer and state) anything missing:

```md
# BRIEF.md
- Brand name / one-line positioning:
- Audience & the one feeling the site must create:
- Pages & sections (or "single page"):
- Real content available? (copy, photos, logo) — list what exists:
- Calls to action (primary, secondary):
- Style skill chosen: skills/styles/<name>
- Constraints: (CMS? e-commerce backend? deadline? hosting?)
```

**Gate:** brief written to `BRIEF.md`. If no style was chosen, propose one from `skills/styles/`
with a one-line reason and proceed.

### Phase 1 — Direction (the most important phase)

Read the chosen style skill **top to bottom**. Then write `DIRECTION.md`:

```md
# DIRECTION.md
- Big idea (one sentence — what makes this site memorable):
- Palette: 1 dominant, 1-2 accents, exact hex — from the style skill's palette directions
- Type: display + body pairing (named fonts, licensed/free), type scale
- Motion language: 3 adjectives + signature move (e.g. "heavy, precise, cinematic — masked
  line-reveals everywhere, one WebGL moment in the hero")
- Layout system: grid, spacing unit, container widths
- The one creative risk: (every award winner has exactly one big swing — name yours)
```

**Gate:** DIRECTION.md exists and a designer could sketch the site from it alone.

### Phase 2 — Scaffold

The style skill chooses the stack. If it offers options, decide using
`references/tech-stack-guide.md`. Scaffold, install deps, verify dev server runs, commit.

**Gate:** dev server serves a blank page with fonts loading correctly (`font-display: swap`,
preloaded WOFF2, no FOUT flash of default fonts).

### Phase 3 — Design tokens

Encode DIRECTION.md as tokens **before any component**: CSS custom properties (or Tailwind theme):
colors, type scale (use `clamp()` for fluid display sizes), spacing scale, radii, z-index scale,
motion tokens (durations: fast 0.3s / base 0.6s / slow 1.0s; easings: `cubic-bezier(0.16,1,0.3,1)`
"expo-out" as default reveal ease). One file, single source of truth.

### Phase 4 — Structure (static, semantic, mobile-first)

Build every section from the style skill's **section blueprint** as static, semantic HTML first —
real heading hierarchy (`h1` once), `<nav>`, `<main>`, `<footer>`, buttons are `<button>`/`<a>`.
Write real copy from the brief (Content is 10% of the score — no lorem ipsum in the final site;
draft strong placeholder copy if the user gave none and mark it `<!-- COPY: draft -->`).

**Gate:** site reads perfectly with CSS animations disabled and images missing.

### Phase 5 — Asset wiring

For every visual slot, reference an ID from `assets/manifest.md`. If the manifest doesn't exist,
create a stub using `skills/asset-creation/references/asset-manifest-template.md`, add an entry
per slot with a `TODO(describe:)` prompt slot, and generate labeled SVG placeholders at the real
paths (the asset-creation skill has a placeholder script — reuse it). Set width/height on every
image (zero layout shift), `loading="lazy"` below the fold, modern formats (AVIF/WebP with
fallback).

**Gate:** `grep` finds no image path in code that's absent from the manifest.

### Phase 6 — Motion

Choreograph using the style skill's signature moves + `references/motion-recipes.md` (Lenis,
GSAP ScrollTrigger, split-text reveals, transitions, WebGL starters — all copy-paste ready).
Principles that separate winners from templates:

- **Choreograph, don't decorate.** Elements within a section animate as one staggered phrase
  (stagger 0.06–0.1s), not as isolated fade-ins. One easing family site-wide.
- **Scroll is the timeline.** Key sections reveal with intentional pacing; use scrub/pin for the
  1-2 storytelling moments, simple reveals elsewhere.
- **Every interactive element responds** (hover, press) within 100ms — micro-interactions are
  where "expensive feel" lives.
- **Restraint.** One WebGL/3D moment max unless the style skill says otherwise — the 2026 reality
  check: unbudgeted 3D kills performance scores.
- Wrap everything in the reduced-motion guard from motion-recipes.

**Gate:** 60fps while scrolling the full page in dev tools performance panel; site fully usable
with `prefers-reduced-motion: reduce`.

### Phase 7 — Responsive

Real breakpoint work, not just wrapping: display type scales via `clamp()`, grids collapse with
intention (the mobile layout should look *designed*, not stacked), hover-only affordances get
touch equivalents, WebGL scenes get lighter mobile variants or poster fallbacks. Test 360px,
768px, 1280px, 1920px.

### Phase 8 — Accessibility

Keyboard-navigable everything (visible focus states styled to match the design), contrast ≥ 4.5:1
body / 3:1 large text, alt text from the manifest, `aria-label` on icon buttons, no scroll-jacking
that traps keyboards, skip-to-content link. Custom cursors never *replace* the real cursor for
interaction targets.

### Phase 9 — Performance

Budgets (see quality-bar for the full list): LCP < 2.5s, CLS < 0.1, JS < 300KB gzipped
(excluding a justified WebGL bundle, lazy-loaded), fonts ≤ 2 families / 4 weights, preload the
LCP image and display font. Lazy-init WebGL with IntersectionObserver; pause rAF loops off-screen.

### Phase 10 — QA self-score

Score yourself honestly against `references/quality-bar.md` (the award rubric as concrete
checks). Anything below the bar → fix and re-score. Then do the **screenshot test**: capture the
hero at 1440px — if it could be mistaken for a template, return to Phase 1's "one creative risk"
and push harder. Ship with: custom 404, favicon set, OG image (asset manifest has entries for
these), and a `NOTES.md` telling the user exactly which manifest assets are still placeholders
and how to generate the real ones.

## Working with the asset-creation skill

- Builder and asset skill communicate **only** through `assets/manifest.md` — treat it as the API.
- Either can run first. If you (builder) create the manifest stub, the asset skill enriches it;
  if it exists already, respect its IDs and paths exactly.
- When the user drops real images in, they replace placeholder files at the same path — nothing
  in code changes. Verify aspect ratios match manifest specs.
