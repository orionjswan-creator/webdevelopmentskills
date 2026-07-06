---
name: editorial-studio-style
description: Award-winning editorial / magazine / creative-studio style — dramatic serif typography, asymmetric broken grids, kinetic type moments, image reveals, print-design sensibility on the web. Use via the site-builder skill for magazines, journals, design studios, cultural institutions, photographers, writers.
---

# Style: Editorial Studio

Print design's sensibility brought to the web — the genre of Awwwards' typography collections
and type-first studios (the Obys lineage, Immersive Garden's kinetic-type systems). The feeling
to create: **"someone with impeccable taste composed every pixel of this page."** Type IS the
design; images punctuate it.

## Stack (this skill's choice)

**Astro + Tailwind (or vanilla CSS) + GSAP islands.** Editorial sites are content sites:
Astro's zero-JS-by-default + content collections (MDX articles) is the perfect engine, with
GSAP loaded only on pages that choreograph. Next.js only if the site needs app-like features.
Rationale: tech-stack-guide.md.

## Design tokens

- **Palette**: paper and ink — warm white (`#faf7f2`) or newsprint gray canvas, rich black ink
  (`#141210`), ONE editorial accent (vermillion red, cobalt, or dark green) used like a
  printer's spot color: folios, links, one word per spread. Dark "night edition" variant OK.
- **Type**: the whole budget goes here. Display serif with real personality — Instrument
  Serif, Fraunces (high optical size axis), Libre Caslon Condensed, or Zodiak/Sentient
  (Fontshare). Pair with a dry grotesque for meta/UI — Cabinet Grotesk or General Sans. Mono
  for folios/timestamps. Display at `clamp(3rem, 10vw, 10rem)`, tight leading (0.95),
  *italic* moments for contrast. Body serif or sans at 1.125rem/1.6, measure 60–70ch.
- **Layout**: strict 12-col grid **deliberately broken** — headlines overhang columns, images
  offset across gutters, captions sit in margins. Oversized folio numerals (`01`, `02`) as
  graphic elements. Hairline rules + generous margins. The grid is felt because it's
  violated with intention.

## Section blueprint

**Home / Index**
1. **Masthead** — huge serif wordmark or the current issue title; date/edition in mono;
   nav as an understated text row. Optional: masthead letters reveal per-character on load.
2. **Lead story** — magazine cover energy: one dominant image (clip reveal §5) + overhanging
   display headline + dek + byline in mono.
3. **Index list** — the signature editorial pattern: article titles as large serif rows;
   hover = row indents / turns accent / shows a cursor-following preview image (§7 variant).
   Folio number, category, reading time in mono at row edges.
4. **Feature grid** — asymmetric: one 8-col image piece, two 4-col text pieces, a
   pull-quote cell set in giant italic serif. Break alignment once per screen.
5. **Kinetic moment** — ONE scroll-scrubbed type sequence (a manifesto line that scales/
   tightens as you scroll, §3) — per trend-report, one moment, not a system.
6. **Footer** — colophon style: type credits, contact, tiny mono print-style details
   ("Set in Fraunces & Cabinet Grotesk — Published from Porto").

**Article template** (where readers actually live — Content 10% + Usability 30% both live here)
- Title block: category eyebrow → display headline (masked line reveal §2) → dek → byline/date
  in mono → hero image clip reveal.
- Body: 60–70ch measure, drop cap on the first paragraph (`::first-letter`), pull quotes
  breaking the measure at 1.5× width, images with margin captions, section breaks as spot-color
  asterisks/rules.
- Footer of article: next-article teaser as a giant serif link.

## Signature moves (choose 4–5)

| Move | Recipe |
|---|---|
| Index-list hover with floating preview | motion-recipes §7 variant |
| Masked line reveals on headlines | §2 |
| Clip-path image reveals | §5 |
| One kinetic-type scrub moment | §3 |
| Native scroll-driven fade-ins for article content | §10 (no GSAP needed) |
| Marquee ticker of headlines/dates | §6 |
| Drop caps, margin captions, spot-color folios | pure CSS craft |
| View-transition morphs between index and article | §9 |

Motion here is **restrained and typographic** — reveals and settles, no bounce, plenty of
static. The craft shows in spacing and rhythm more than movement.

## Asset slots

| id | dimensions | role |
|---|---|---|
| lead-story | 2400×1600 | homepage lead image |
| article-XX-hero | 2400×1400 | per-article hero |
| article-XX-inline-N | 1600×1100 | in-article images |
| preview-XX | 800×1000 | index-list hover previews (small, lazy) |
| og-article template | 1200×630 | per-article share card (code-generated with title) |

Art direction: documentary/editorial photography or one consistent illustration style — grain,
honest light, "shot for the story" not stock. Duotone/monochrome treatment (CSS
`filter: grayscale(1)` + blend with accent) unifies mixed sources cheaply.

## Do / Don't

- DO obsess over typographic details: real quotes (“”), en/em dashes, `text-wrap: balance` on
  headlines, `hanging-punctuation` where supported, tabular numerals for folios.
- DO make reading comfortable — this style lives or dies on the article page.
- DON'T break the grid randomly; pick 2 violation patterns and repeat them as a system.
- DON'T animate body text, ever. Headlines and images only.
- DON'T let the accent color exceed ~5% of any viewport — spot color, not theme color.

## Mini-QA

- Print an article page to PDF — it should look like a designed magazine spread
- Index page navigable and beautiful with JS disabled (Astro should make this free)
- Headlines survive 360px without awkward two-letter line breaks (`text-wrap: balance`)
- Reading time honest, bylines/dates real, alt text written like captions
