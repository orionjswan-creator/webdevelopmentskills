---
name: design-taste
description: The taste layer — how to make the aesthetic judgment calls that separate award-level design from competent templates. Typography pairing logic, color-system craft, spacing and hierarchy judgment, the "expensive look" heuristics, and the canonical taste failures to catch. Use during site-builder Phase 1 (Direction), during any UI design decision, or standalone when asked "make this look better/more premium" without clear direction.
---

# Design Taste

Skills can encode recipes; this one encodes **judgment** — the decisions a great art director
makes before and between the recipes. Read it when choosing a direction, and re-read the
failure list before calling anything done.

## The prime rule: commit

The single biggest separator between award work and template work is **commitment to one
idea**. A direction executed at 100% beats three good directions blended at 33%. Every choice
below is a *decision*, made once, written in DIRECTION.md, and enforced everywhere. When in
doubt: fewer fonts, fewer colors, fewer effects, MORE of the one thing that makes this site
itself.

## Typography judgment (where taste is most visible)

**Choosing the display face.** The display font carries ~60% of the site's personality. Ask:
what does the brand sound like when spoken aloud — then match the voice:
- Assured/technical → precise grotesque (Cabinet Grotesk, Switzer, Archivo)
- Cultured/heritage → serif with real optical axes (Fraunces, Cormorant, Libre Caslon)
- Bold/new → expressive display (Clash Display, Bricolage Grotesque, Zodiak heavy)
- Human/warm → soft grotesque or humanist serif (General Sans, Sentient)

Never the overused set (Inter/Roboto/Arial/Helvetica/Poppins/Montserrat/Open Sans/Lato/
Raleway/Space Grotesk as brand face) — not because they're bad, because they're *invisible*.

**Pairing logic** (pick ONE pattern):
1. **One family, full range** — same face, weights 400→800, optical sizes. Safest, most modern.
2. **Serif display + quiet sans body** — the editorial classic. The sans must be *quieter*
   than the serif (if both have personality, they fight).
3. **Grotesque display + mono meta** — the studio/tech classic. Mono is seasoning: labels,
   numbers, timestamps — never paragraphs.

Test a pairing: set a headline + two sentences + a mono label together. If your eye can't
decide where to go first, the pairing fails hierarchy.

**Scale and rhythm.** Use a ratio (1.25 minor third for dense/product; 1.414+ for editorial
drama) but *break it deliberately at the top* — the hero display size should feel almost
uncomfortable (`clamp(3.5rem, 10-12vw, …)`). Tighten what grows: big type wants tracking
−0.02 to −0.04em and leading 0.9–1.05; body stays 1.5–1.7. Fluid type everywhere
(`clamp()`), and `text-wrap: balance` on every headline.

## Color judgment

**The 60/30/10 that award sites actually use: ~85/10/5.** One dominant canvas (85%), one ink
(10%), one accent (5%). The accent's rarity IS its power — if the accent appears in every
section, it's not an accent, it's a second brand color, and the design flattens.

**Craft rules:**
- Never pure black on pure white: `#0a0a0a`-ish on `#f7f5f0`-ish (warm) or `#fbfbfd` (cool).
  Temperature is a decision — warm reads crafted/human, cool reads technical/precise. Pick
  one temperature and keep grays on it (no cool grays on a warm page).
- Dark themes are **layered**, not inverted: canvas → raised surface → overlay, each step
  +4-6% lightness; borders at 8–12% white; text at 92%/60% white, never 100%.
- Work in OKLCH for palette construction (perceptually even steps); name colors semantically
  in tokens (`--surface`, `--ink`, `--accent`) not descriptively (`--blue`).
- Saturated accent ON a neutral field, not saturated-on-saturated. If the brand demands two
  accents, they share either hue-family or lightness — never both free.
- Test every text/background pair including text-over-image at the image's *lightest* point.

## Space and hierarchy judgment

**Whitespace is the price of the premium look.** The most common template tell is sections
that start too soon after the previous one. Award sites spend 120–200px between desktop
sections and let hero moments own the full viewport. If a section feels weak, the first fix
is usually *more space + bigger type*, not more decoration.

**One axis of alignment per composition.** Everything aligns to the grid except the ONE
deliberate violation per screen (the overhanging headline, the offset image). A violation
repeated becomes a motif; violations everywhere become noise.

**Hierarchy check (the squint test):** blur your eyes at any screen — you should see exactly
one primary thing, one secondary, and texture. Three-plus competing weights = redesign the
section, don't nudge pixels.

## The "expensive look" heuristics

What makes viewers subconsciously read a page as high-end (these are cheap to do, expensive
to ignore):

1. **Big type, small everything-else** — oversized display + restrained body/UI.
2. **Real materials** — one consistent photographic/render language (the manifest's art
   direction block); mixed stock styles are the fastest way to look cheap.
3. **Micro-response** — every interactive element acknowledges hover/press within 100ms.
4. **Custom details in default places** — styled `::selection`, styled focus rings,
   a designed 404, favicon that matches, an OG card that looks composed.
5. **Grain/texture at whisper level** (3–5%) — kills the "flat vector void" feel.
6. **Sharp is expensive, soft is friendly** — radius ≈ 0–4px + hairline borders reads luxury;
   radius 12–16px + soft shadows reads product/consumer. Pick per brand, never mix.
7. **Nothing moves that doesn't mean** — one easing family, no decorative bounce.
8. **Confidence in copy** — short declaratives; hedging words break the visual spell.

## Canonical taste failures (audit yourself against these)

- **The blend**: two half-committed directions (e.g. brutalist borders + soft SaaS shadows).
- **Accent inflation**: the 5% color used at 30%.
- **Font drift**: a third font that "just made sense" for one component.
- **Radius roulette**: 3+ different corner radii in actual use.
- **Centered everything**: center-aligning every section kills rhythm — alternate.
- **Hero hedging**: headline + subline + 2 CTAs + badge row + ticker all in the first fold.
- **Decorative motion**: elements animating because they can (see quality-bar Creativity).
- **Stock-mix**: one 3D render + one flat illustration + one photo = three different sites.
- **Contrast cowardice**: gray-on-gray body text (< 4.5:1) because "it looked lighter."
- **The invisible font problem**: shipping the overused set and wondering why it looks generic.

## Applying taste to an existing UI ("make it look better" requests)

Work this exact order — highest leverage first:
1. Fix hierarchy (squint test per screen; usually: bigger heading, more section space).
2. Reduce: remove the weakest element per screen (a badge, a divider, a third button).
3. Replace fonts if on the overused list; retighten display tracking/leading.
4. Consolidate colors to 85/10/5 and one temperature; re-layer dark surfaces if dark.
5. Normalize radii/borders/shadows to one system.
6. Add micro-response to every interactive element.
7. Only THEN consider adding: texture, one signature moment, richer imagery.

Adding before reducing is the amateur order; it's why "improved" pages often get worse.
