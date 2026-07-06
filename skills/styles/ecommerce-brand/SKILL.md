---
name: ecommerce-brand-style
description: Award-winning luxury brand / e-commerce experience style — full-bleed imagery, editorial product layouts, horizontal lookbooks, refined micro-interactions, quiet confidence. Use via the site-builder skill for shops, product brands, fashion, furniture, beauty, food & drink.
---

# Style: E-commerce Brand

The luxury-commerce genre from Awwwards' e-commerce/luxury winner lists (the register of recent
honorees like Gielly Green, Belle Oaks, Bécane Paris, seasonal Max Mara editions): shopping
reframed as an editorial experience. The feeling to create: **"this brand is worth the price."**
Quiet, spacious, tactile — the product photography does the talking; the interface whispers.

## Stack (this skill's choice)

**Next.js (App Router) + Tailwind + headless Shopify (Storefront API)** when there's a real
store — cart/checkout are solved problems, never rebuild them. **Astro** when it's a lookbook /
brand site with a "buy" link out. Motion: Framer Motion for UI state, GSAP for scroll scenes,
Lenis optional (keep native feel on product grids). Rationale: tech-stack-guide.md.

## Design tokens

- **Palette**: warm neutrals — ivory/cream/bone canvas (`#f7f4ee`-ish), charcoal ink
  (`#1c1a17`), one muted accent drawn from the product world (terracotta, sage, oxblood,
  butter). Dark luxury variant: espresso/near-black with cream. Never bright SaaS colors.
- **Type**: display serif with character — Fraunces (soft/wonky axes), Cormorant Garamond,
  Instrument Serif, or Zodiak (Fontshare). Body: quiet sans — Satoshi, General Sans, or
  Hanken Grotesk. Product names in the serif; prices/UI in the sans; letter-spaced uppercase
  sans for eyebrows/labels (`0.12em` tracking, 0.75rem).
- **Layout**: airy 12-col grid, asymmetric editorial placements (image col 1–7, text col
  9–12), section padding ≥ 8rem. Hairline rules (`1px solid` at 15% ink) as the structural
  motif. Radius: 0 or barely-there (2px) — sharp corners read expensive.

## Section blueprint

**Home**
1. **Hero** — full-bleed campaign image (or slow 6–8s Ken Burns zoom, scale 1.0→1.05), serif
   headline overlaid or set just below, one CTA ("Shop the collection"). No carousel.
2. **Featured collection** — editorial grid: mixed image sizes (one 4:5 large, two smaller),
   generous whitespace, hover = image crossfade to second shot + quiet "Add" affordance.
3. **Brand story strip** — full-width image with parallax (§4) + short serif statement,
   clip-reveal (§5). This is the "why we exist" moment.
4. **Product highlights** — horizontal scroll strip (pinned scrub or native
   `scroll-snap-type: x mandatory`) — the lookbook moment.
5. **Editorial/press** — quotes set in large serif italics, publication logos, hairline rules.
6. **Footer** — newsletter with a well-written incentive, quiet sitemap, oversized serif
   brand mark.

**PLP (collection)** — editorial grid, filters as understated text buttons (not sidebar
machinery), 4:5 cards: image, serif name, sans price. Hover: crossfade to on-model/in-context
shot. Optional: every ~6th cell is a full-width campaign image breaking the grid rhythm.

**PDP (product)** — the money page:
- Split layout: left = scrollable gallery (tall images, no thumbnails-in-a-box), right =
  `position: sticky` info column: serif name, price, 2-line description, variant selector
  (styled radio swatches), add-to-cart.
- Add-to-cart: full-width, instant optimistic feedback ("Added ✓" morph), cart drawer slides
  in (glassmorphism per trend-report is allowed here — it's a modal layer).
- Below: details accordion (materials, care, shipping), "pairs with" cross-sell (3 items max).

**Cart drawer** — side panel, line items with images, quantity steppers, subtotal, checkout
CTA. Free-shipping progress bar if thresholds exist. Never a separate cart page as primary.

## Signature moves (choose 4–5)

| Move | Recipe |
|---|---|
| Image crossfade on product-card hover | CSS: stacked imgs, opacity swap 0.5s ease |
| Ken Burns hero | CSS: `animation: kb 8s ease-out forwards` scale 1→1.05 |
| Clip-path reveals on section images | motion-recipes §5 |
| Horizontal lookbook strip | §3 pinned scrub, or native scroll-snap |
| Sticky PDP info column | CSS `position: sticky; top: 6rem` |
| Cart-drawer choreography | Framer Motion: drawer 0.5s expo, items stagger 0.05s |
| Hairline-rule grid motif | 1px borders at 15% ink opacity |

Micro-interactions carry the luxury feel: swatch hover states, quantity stepper precision,
input focus underlines that draw in from the left, the "Added" morph. Budget real time here.

## Asset slots

| id | dimensions | role |
|---|---|---|
| hero-campaign | 2880×1800 | homepage hero |
| product-XX-main / -alt | 1600×2000 each | per product: studio shot + in-context shot |
| story-strip | 2880×1400 | brand story full-width |
| lookbook-01…N | 1400×1750 | horizontal strip |
| og-default | 1200×630 | share card |

Art-direction block matters most in this style: ONE photographic language (same light, same
surfaces, same grade) across every product image. If the user has real product photos, grade
placeholders to match them, not vice versa. Real photos > generated for actual products —
generated product images misrepresent goods; use `awaiting-user` status and spec exact shot
lists instead (angles, light, background per product).

## Do / Don't

- DO let images be huge and text be small — inverted hierarchy is the luxury signature.
- DO write price/shipping/returns clearly — trust is conversion (Usability 30%).
- DON'T animate product grids heavily; shoppers are task-driven — save motion for story moments.
- DON'T use urgency patterns (countdowns, fake stock warnings) — they read cheap and juries
  punish dark patterns.
- DON'T generate fake "real product" photos for an actual store (illustrative/campaign mood
  imagery is fine; the manifest marks the difference).

## Mini-QA

- PDP → add-to-cart → drawer → checkout link works keyboard-only
- Product images: correct aspect everywhere, zero CLS, crossfade doesn't double-load eagerly
- The hero screenshot could open a printed lookbook
- Lighthouse on PLP with 24 products still passes budgets (lazy images below fold)
