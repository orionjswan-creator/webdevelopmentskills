---
name: immersive-agency-style
description: Award-winning creative agency / studio portfolio style — the Awwwards SOTD staple. WebGL hero moment, scroll-driven storytelling, masked type reveals, custom cursor, oversized typography, cinematic pacing. Use via the site-builder skill when building an agency, studio, or high-end portfolio site.
---

# Style: Immersive Agency

The genre that dominates Awwwards SOTD: creative studios and agencies whose site IS the
portfolio piece (the tradition of Lusion, Active Theory, Obys, OFF+BRAND's SOTY-winning work).
The feeling to create: **"these people are on another level."** Cinematic, precise, heavy.

## Stack (this skill's choice)

**Vite + vanilla TypeScript + GSAP/ScrollTrigger + Lenis + Three.js.** No framework — the whole
site is custom motion, and full control of the render loop is worth more than components. Use
Astro instead if the site has many content pages (case-study articles); Next.js only if the
client demands React. See site-builder `references/tech-stack-guide.md`.

## Design tokens (directions, not defaults — commit in DIRECTION.md)

- **Palette**: near-black canvas (`#0a0a0a`–`#111`, never pure #000) + off-white text
  (`#f2efe9`-ish) + ONE electric accent (acid green, signal orange, klein blue…). Or invert:
  bone-white canvas, near-black ink, same single accent. Two moods, same system.
- **Type**: expressive grotesque display — Clash Display, Cabinet Grotesk, General Sans
  (Fontshare), or Archivo Expanded. Body: the same family's regular weights or a quiet
  companion (General Sans, Hanken Grotesk). Mono accent for labels/numbers: JetBrains Mono or
  Fragment Mono. Display sizes are HUGE: `clamp(3.5rem, 12vw, 12rem)`, tracking −0.02 to
  −0.04em, leading 0.9–1.0.
- **Layout**: 12-col fluid grid, 2rem gutters; full-bleed moments alternating with tight
  60ch text blocks; section padding ≥ 10rem desktop. Mono-font meta labels
  (`01 / WORK`, `SCROLL ↓`) as a recurring motif.

## Section blueprint (single page or Home + Work + About + Contact)

1. **Preloader** — counter + curtain reveal (motion-recipes §8). Skip on repeat visits.
2. **Hero** — the ONE WebGL moment (motion-recipes §12): shader gradient field, particle
   system, or distorted brand typography. Massive display headline over it, masked line
   reveal, mono meta labels in corners, scroll cue.
3. **Manifesto** — 2–4 short lines of oversized statement type, revealed word-by-word or
   line-by-line on scroll (scrub). This is where the copy voice must be razor-sharp.
4. **Selected work** — 4–8 case cards. Hover: image scale + title letter-spacing shift
   (motion-recipes §13), or a cursor-following preview image on a title-only list. Card ratio
   4:5 or 3:4. Each card: mono index number, project name, 2-word category.
5. **Capabilities / services** — accordion rows or a horizontal-scroll strip (pinned scrub).
   Row hover: background inverts to accent.
6. **About teaser** — split layout: portrait/studio image with parallax (§4) + clip reveal
   (§5), short bio text.
7. **Footer / contact** — the second-biggest type on the page: a giant email link or "Let's
   talk" with magnetic hover (§7). Footer reveals from behind the last section
   (`position: sticky` bottom or negative-margin reveal). Marquee (§6) of services/clients
   above it.

## Signature moves (choose 4–5, not all — restraint reads as confidence)

| Move | Recipe |
|---|---|
| Masked line reveals on ALL display type | motion-recipes §2 |
| One scroll-scrubbed pinned story section | §3 |
| Custom cursor dot + magnetic CTAs | §7 |
| WebGL hero (only one WebGL context) | §12 |
| Curtain page transitions | §9 |
| Marquee strip | §6 |
| Grain overlay site-wide | code-assets §1 |
| Cursor-following work previews | §7 variant: image `position:fixed`, `quickTo` follow, swap `src` per hovered row |

Choreography: default timings from motion-recipes §14. The site should feel **heavy and
precise** — slightly longer durations (1.0–1.2s), expo easings, nothing bouncy.

## Asset slots (seed for the manifest)

| id | dimensions | role |
|---|---|---|
| hero-poster | 2880×1620 | static fallback of the WebGL hero |
| work-01…N | 1600×2000 | case card images (art-directed as one set) |
| about-portrait | 1600×2000 | studio/founder image |
| og-default | 1200×630 | share card (code-generated) |
| logo-wordmark | 320×64 | code-built wordmark |

Case-study imagery is the credibility layer — if the user has no real work to show, interview
for 3–6 fictional-but-plausible project concepts and art-direct them as one photographic set.

## Do / Don't

- DO make the hero readable in 3 seconds: name + what they do + one feeling.
- DO keep ONE creative risk big (the hero) and everything else disciplined.
- DON'T stack WebGL sections; don't scroll-jack; don't let the preloader exceed 2.5s.
- DON'T use more than one accent color; the accent appears rarely enough to feel electric.
- DON'T ship bouncy/elastic easings anywhere except the magnetic-button return.

## Mini-QA (on top of quality-bar.md)

- Hero at 1440px passes the screenshot test against actual Awwwards SOTD winners
- 60fps during the pinned scrub section on a mid-range laptop
- WebGL: DPR ≤ 2, lazy-init, pauses off-screen, poster fallback works (test by forcing
  `prefers-reduced-motion`)
- The email link in the footer is the most satisfying interaction on the page
