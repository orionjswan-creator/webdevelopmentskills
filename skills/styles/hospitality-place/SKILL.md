---
name: hospitality-place-style
description: Award-level place-marketing style for hotels, restaurants, resorts, venues, and luxury real estate — cinematic video/imagery heroes, sensory storytelling, and a booking/enquiry path that survives the spectacle. The premium agency market genre. Use via the site-builder skill for any business that sells a physical place or experience.
---

# Style: Hospitality & Place

The genre of Awwwards' hotel/restaurant and real-estate winner lists (the Balmoral /
Badrutt's Palace / Elyse Residence register — see the award casebook): selling a *place*
means selling how it will feel to be there. The feeling to create: **"I can already imagine
myself there — where do I book?"** Cinematic first, but the booking path is sacred: these
sites earn real revenue, and the casebook's lesson is that winners keep utility obvious
inside the spectacle.

## Stack (this skill's choice)

**Astro + Tailwind + GSAP islands** for most places (content-heavy, SEO-critical, editorially
updated). **Next.js** when there's real booking/availability logic in-house. Booking itself:
integrate the operator's existing engine (SevenRooms/OpenTable/Tock for restaurants;
SynXis/Mews/Cloudbeds links for hotels; enquiry forms for real estate) — never rebuild
reservation systems inside a site project.

## Design tokens

- **Palette**: drawn from the place itself — ask for (or infer from) the interiors/landscape:
  stone, plaster, olive, sea, ember. One warm neutral canvas, deep ink, one atmospheric
  accent. Dark variant for night-led venues (bars, fine dining).
- **Type**: serif-led — Fraunces, Cormorant Garamond, or Libre Caslon for display (menus,
  headlines); quiet sans (Satoshi, Hanken Grotesk) for UI/booking; mono only for practical
  data (hours, coordinates, rates). Italic serif for sensory captions.
- **Layout**: full-bleed imagery alternating with narrow text measures (55–65ch); generous
  section padding; hairline rules. The rhythm is *cinematic wide shot → intimate detail* —
  alternate scale like a film edit.

## Section blueprint

**Home**
1. **Hero** — full-viewport video loop (8–15s, muted, no audio autoplay, ≤ 4MB, poster
   fallback + `prefers-reduced-motion` swap to still) or a slow Ken Burns image. Name +
   one-line sense of place ("A farmhouse table in the Vaucluse"). **Persistent booking
   affordance from the first pixel**: a booking bar (dates/party size) or a fixed
   "Reserve" button in the nav — visible without scrolling, always.
2. **The promise** — 2–3 sentences of sensory copy + a detail image pair (texture, plate,
   light through a window). Clip reveals (motion-recipes §5), parallax at whisper level.
3. **Rooms / Menu / Residences** — the inventory section, genre-adapted:
   - Hotel: room cards (4:3, crossfade hover) → room detail pages with gallery, amenities
     as designed list, rate + "Check availability".
   - Restaurant: the menu as a *designed typographic document* (real HTML, not a PDF —
     though offer the PDF), courses set like an editorial page.
   - Real estate: residences/plans with specs table, floorplans (SVG when possible),
     virtual-tour embed, enquiry CTA.
4. **The story** — provenance: the chef/architect/family, the land, the building's history.
   One pinned scroll moment maximum (§3) — this is the section that earns it.
5. **Practical grace** — location with a *designed* map (custom-styled tiles or an
   illustrated map — never a default embed), hours, getting-there, contact. Award
   hospitality sites treat practical info as a design surface (the Badrutt's lesson:
   useful pages, richly made).
6. **Journal/updates** (optional but powerful for SEO + return visits): seasonal notes,
   events, press.
7. **Footer** — booking CTA repeated, newsletter ("Table notes, monthly"), address set
   beautifully, credits.

## Signature moves (choose 3–4 — restraint is the genre)

| Move | Recipe |
|---|---|
| Video hero with graceful fallbacks | poster image, reduced-motion still, `preload="metadata"` |
| Persistent booking bar that condenses on scroll | sticky bar → nav pill transition |
| Cinematic wide/detail rhythm | layout system above |
| Clip reveals + whisper parallax on imagery | §5, §4 at 0.08–0.12 |
| Menu/rates as typographic documents | editorial-studio's type craft applied to utility |
| Seasonal/time-of-day ambient shift | palette or hero variant by local time — subtle, cacheable |
| Custom-styled map | MapLibre/Mapbox styled to tokens, or commissioned SVG map (manifest) |

## Asset slots

| id | dimensions | role |
|---|---|---|
| hero-loop | 1920×1080 mp4/webm ≤4MB + poster 2880×1620 | homepage hero |
| sense-XX | 1600×2000 & 2400×1600 mix | detail/atmosphere pairs |
| room/dish/residence-XX | 1600×1200 | inventory imagery |
| story-portrait | 1600×2000 | the people/place story |
| map | SVG | illustrated or styled map |
| og-default | 1200×630 | share card |

**Real photography is non-negotiable for the inventory** (rooms, dishes, residences —
misrepresentation is a legal and trust problem): mark `awaiting-user` and spec the shoot
list (golden hour exteriors, window-light interiors, 3 details per room/dish). Generated
imagery is acceptable ONLY for atmosphere/mood slots, marked `role: illustrative`, and
art-directed to match the real photography's grade.

## Do / Don't

- DO protect the booking path: reachable in one interaction from every scroll position;
  the engine handoff styled as far as the vendor allows.
- DO write sensory, specific copy (site-copywriter: "wood smoke and old stone" beats
  "unforgettable luxury experience").
- DO make practical info excellent — hours/directions/parking answered beautifully.
- DON'T autoplay audio; don't gate content behind the video; don't let the loop exceed 4MB.
- DON'T use stock photos of *other places* — an empty room shot honestly beats a borrowed
  paradise.
- DON'T bury rates/menus in PDFs alone — HTML first, PDF as courtesy.

## Mini-QA

- Time from landing → booking engine (or enquiry sent): ≤ 3 interactions, keyboard included
- Video hero: poster paints < 1.5s; page fully usable before video arrives; reduced-motion
  shows the still
- Menu/rates readable at 360px without pinching; map has an address-text fallback
- The hero screenshot sells the *feeling* of the place to someone who's never heard of it
- Local SEO basics: schema (`Hotel`/`Restaurant`/`Place` + address/hours/geo), correct NAP
