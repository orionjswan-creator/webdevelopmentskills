---
name: site-teardown
description: Study any public website professionally — fingerprint its stack, measure its design tokens (type scale, palette, spacing rhythm), map its section structure and motion grammar, and produce TEARDOWN.md, a pattern report that feeds DIRECTION.md, the award casebook, and the starter kits. Extracts techniques and measurements, never code or content. Use when asked to analyze, deconstruct, "figure out how they built", or learn from a specific site.
---

# Site Teardown

Turn admiration into engineering: given a site worth learning from (an award winner, a
competitor, a client's favorite), produce a structured analysis of *how it works* — the
kind of teardown a senior designer does with devtools open. The output feeds Direction
decisions, the award casebook, competitive-research, and starter-kit improvements.

## The line (hard rules, read first)

**You extract facts, patterns, and measurements — never expression.**

- ✅ Take: layout archetypes, section order, measured type scales and spacing rhythms,
  animation durations/easings, stack and library identification, interaction patterns,
  performance techniques, IA and conversion strategy.
- ❌ Never take: source code (even "cleaned up"), markup structure wholesale, copy, images,
  logos, illustrations, fonts you're not licensed for, or the site's distinctive overall
  look-and-feel recreated recognizably (trade dress). One site's *combination* of
  signature choices is its identity — patterns you learn get recombined through OUR style
  skills into original work.
- Don't mirror/download whole sites — it's unnecessary for analysis (everything below
  works from the live site + devtools/Playwright) and a local copy invites exactly the
  reuse we prohibit. Respect robots.txt and don't hammer: a teardown is a handful of
  page loads.
- **The output test**: TEARDOWN.md should let a designer build something *as good*, never
  something *identical*. If a finding could only be used by copying (an illustration
  style, a mascot, a named phrase), record it as "their ownable identity — do not
  approach" so the team designs *away* from it.

## Workflow (30–60 min per site; Playwright available in this environment)

### 1. Stack fingerprint

From page source, headers, and bundle names (no de-minification needed):
- Framework tells: `__NEXT_DATA__`/`_next/` (Next.js) · `astro-island` (Astro) ·
  `data-svelte`/`__sveltekit` · Nuxt globals · plain Vite hashes.
- Library tells: `gsap`/`ScrollTrigger` globals · `lenis` on window or `data-lenis` ·
  `three` / `<canvas>` with WebGL context · Framer Motion class patterns ·
  Swiper/Embla classnames · Shopify (`cdn.shopify.com`), Sanity (`cdn.sanity.io`).
- Hosting/CDN from response headers (`server`, `x-vercel-*`, `cf-ray`).
- Fonts: `@font-face` sources — foundry fonts are a taste signal AND a license warning.

### 2. Token measurement (Playwright: computed styles on real elements)

- **Type**: font-family per role (display/body/mono), the *measured* scale (h1 vs body px
  at 1440 and 390), tracking on display type, line-heights, `clamp()` usage.
- **Color**: canvas, ink, accent(s) as computed values; count distinct colors in use
  (discipline metric); dark-theme handling.
- **Space**: section paddings, container max-width, grid gutters — derive the spacing
  unit and the "generosity ratio" (section padding ÷ body font size — award sites
  typically 7–12×).
- **Shape**: radii in use, border weights, shadow styles (count them — coherence metric).

### 3. Structure map

Scroll through and record the section stack per key page (the ARCHITECTURE.md text-
wireframe format): section job, content type, proof elements, CTA placement. Note the
template count vs page count (their scope efficiency), nav model, and footer strategy.

### 4. Motion grammar

With devtools (or Playwright tracing): reveal durations and easings (inspect transition/
animation computed values; eyeball-time the choreographed ones), stagger patterns,
scroll-trigger points, pinned scenes (count them), page-transition style, hover language,
and the signature moment — describe what it does and *why it lands*, in words.
Performance while you're there: LCP, CLS, JS weight, fps during scroll (their real
budget, not their reputation).

### 5. Strategy read

What the site is optimizing for (per journey), how it handles the industry's table
stakes, what it does badly (there's always something — that's your differentiation
opening), and its ownable identity (the do-not-approach list).

## Output: `TEARDOWN.md`

```md
# Teardown — <site> — <date>
## Verdict (what this site knows that we should learn — 3 sentences)
## Stack: <framework, libraries, hosting, fonts+licenses>
## Measured tokens: <type scale / palette / spacing / shape — numbers, not adjectives>
## Structure: <per-page section maps; template inventory>
## Motion grammar: <durations, easings, staggers, signature moment described>
## Performance: <measured LCP/CLS/JS/fps — their real budget>
## Strategy: <optimizing for; table stakes handling; weaknesses>
## Their ownable identity — DO NOT APPROACH: <the distinctive expression we design away from>
## What we adopt (patterns → which of our skills/kits they improve):
- <pattern> → <e.g. "motion-recipes candidate: 1.4s expo reveals with 0.12 stagger">
- <pattern> → <e.g. "hospitality-place blueprint: rates section before story section">
## Casebook entry (one row, ready to paste into award-casebook.md)
```

## Where findings flow

- **award-casebook.md** — paste the entry row; the casebook is the compounding memory.
- **starter-kits** — measured patterns become kit improvements (a better reveal timing,
  a smarter section order) implemented from scratch in our own code.
- **competitive-research** — teardowns of direct competitors slot into its step 3.
- **DIRECTION.md** — when a client says "I love this site", tear it down, show them the
  *patterns* you'll match and the identity you won't touch — that conversation, made
  concrete, is an agency-tier deliverable in itself.
