---
name: rapid-site-sprint
description: The move-fast building partner — compress the full pipeline into a single-session sprint (2–6 hours of agent work) using decision defaults, parallel asset+build tracks, and strict timeboxes. Use when speed is explicit ("today", "ASAP", "quick version", "MVP site", "landing page by tonight") or for v1s that will be iterated. Quality floor stays fixed; scope is what flexes.
---

# Rapid Site Sprint

The full site-builder pipeline optimizes for award submission; this skill optimizes for
**shipping something excellent TODAY**. The trick is not skipping quality — it's skipping
*decisions* (via defaults), *scope* (via the cut list), and *waiting* (via parallel tracks).
A sprint site should still pass the quality bar's Usability checks 100% and look deliberate;
it trades breadth (fewer sections, fewer pages, no WebGL) for speed.

## The sprint contract (state it to the user up front)

"V1 today: one page (or N), [style], placeholders where real assets are pending, quality
floor intact. The cut list below ships in v2."

## Decision defaults (skip Phase-1 deliberation; override only if the brief demands)

| Decision | Default |
|---|---|
| Style | Brief keyword-match: product/launch → viral-trending · shop → ecommerce-brand · portfolio → personal-portfolio (quiet pole) · content → editorial-studio · else → saas-product. Agency/immersive is NOT sprintable — offer editorial-studio instead |
| Stack | Astro + Tailwind for anything static; Next.js only if the brief needs app/commerce features TODAY |
| Fonts | One per register, pre-picked: Bricolage Grotesque (product/launch) · Fraunces + Hanken Grotesk (brand/editorial) · Cabinet Grotesk (studio/portfolio). Self-host variable WOFF2 |
| Palette | Style skill's first palette direction, verbatim; accent from the brand's existing color if one exists |
| Motion | CSS-only: native scroll-driven reveals (motion-recipes §10), marquee §6, hover systems from ui-patterns. NO GSAP, NO Lenis, NO WebGL in a sprint |
| Sections | Style skill's blueprint, first 5 sections only |
| Imagery | Kinetic-gradient + grain hero (zero image dependency) OR one hero image; everything else typographic |

Write the mini-DIRECTION.md anyway (5 lines, 5 minutes) — commitment still applies, it just
takes minutes because the defaults did the deliberating.

## Parallel tracks (the speed structure)

Run as two agents when possible (Codex on assets, Sonnet on build), or interleave as one:

```
TRACK A (build)                        TRACK B (assets)
1. Scaffold + tokens (30m)             1. Manifest stub + art direction (10m)
2. All sections, static, real copy     2. Wordmark, grain, OG template,
   as you go (90m)                        favicon — code assets only (30m)
3. Asset wiring to manifest IDs (15m)  3. Placeholders at every path (5m)
4. CSS motion pass (30m)               4. Prompt specs for post-sprint
5. Responsive + a11y sweep (30m)          image generation (15m)
6. Sprint QA + deploy (30m)
```

The manifest contract makes the tracks collision-free: agree IDs in the first 10 minutes,
then neither track waits for the other.

## Timeboxes (hard — when the box ends, take the default and move)

- Any single design decision: 5 min → take the default
- Any single section: 30 min → simplify to type + space (design-taste: the fix is usually
  bigger type and more space, which is also the fastest fix)
- Any bug: 20 min → replace the pattern with a simpler one from ui-patterns
- Copy per section: 10 min with site-copywriter's rules (voice sheet = the 3 brief
  adjectives; ban list applies even at speed)

## The cut list (what a sprint never includes — write these into NOTES.md as v2)

Preloaders · page transitions · WebGL/3D · custom cursors · pinned scrub scenes ·
horizontal scroll · multi-page beyond the brief's minimum · CMS wiring · easter eggs ·
per-page dynamic OG (one static OG card is fine for v1)

## The never-cut list (the quality floor — non-negotiable even at maximum speed)

Real fonts (never the overused set) · written copy, zero lorem ipsum · semantic HTML +
keyboard nav + visible focus · contrast ratios · image dimensions set (zero CLS) ·
reduced-motion safety (free, since motion is CSS) · mobile at 360px genuinely designed ·
favicon + OG card + custom 404 (all three are ≤ 20 minutes via code-assets) · the manifest,
so v2 assets drop in with no code changes

## Sprint QA (15 minutes, replaces Phase 10)

1. Lighthouse: all budgets green (a no-JS-library sprint site should score ~100 — if not,
   something's wrong, find it)
2. Keyboard-only walk of the primary flow
3. 360px + 1440px screenshots — both look deliberate?
4. The squint test on every section (design-taste)
5. Read the hero aloud — would you click?

## Handoff → v2

`NOTES.md`: the cut list as a prioritized v2 plan, pending manifest images (with their
ready-to-paste prompts from Track B), and the one upgrade with the highest taste-per-hour
ratio (usually: the signature moment the sprint deferred — route it through site-builder
Phase 1 when v2 starts, possibly with a competitive-research pass if the market matters).

Sprint sites are v1s by design: the library's full pipeline is the upgrade path, and
everything the sprint built (tokens, manifest, copy deck, semantic structure) is the same
foundation the full pipeline would have laid — nothing is throwaway.
