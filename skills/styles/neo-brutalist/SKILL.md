---
name: neo-brutalist-style
description: Neo-brutalist / tactile-raw statement style — hard borders, hard shadows, raw type, deliberate rule-breaking as a committed identity. The 2026 counter-trend to polished minimalism. Use via the site-builder skill for creative tools, indie products, studios, events, zines, and brands that want to feel loud, honest, and human.
---

# Style: Neo-Brutalist

The committed counter-trend: raw, loud, structurally honest design that stands out in a feed
of polished sameness. Trend-report's warning is this skill's thesis — **half-applied
brutalism looks unfinished; fully-committed brutalism looks like a statement.** The feeling
to create: **"this was made by opinionated humans, on purpose."**

## Stack (this skill's choice)

**Astro (or Vite vanilla) + plain CSS.** Brutalism rewards a thin stack — semantic HTML with
visible structure is the aesthetic. Tailwind optional; motion is mostly CSS + a little
vanilla JS; GSAP only if a marquee/scroll moment needs it. Next.js only for app needs.

## Design tokens

- **Palette**: high-contrast and unapologetic — paper white or raw cream canvas, TRUE black
  ink, and 1–2 loud accents (safety yellow, signal red, cobalt, hot pink). Or full-bleed
  single-color pages (accent as canvas). No gradients except deliberate hard-stop ones
  (`linear-gradient(90deg, A 50%, B 50%)`).
- **Type**: big, bold, unpolished-on-purpose. Display: a heavy grotesque or slab — Archivo
  Black, Bricolage Grotesque (heavy), Zodiak heavy, or a characterful mono AS display
  (JetBrains Mono ExtraBold). Body: readable workhorse (Hanken Grotesk) or mono for full
  commitment. Underlines are thick (`text-decoration-thickness: 3px`). Uppercase liberally.
- **Structure (the actual aesthetic)**: `border: 2–3px solid black` on everything that is a
  thing; hard offset shadows (`box-shadow: 6px 6px 0 #000`) instead of blur; **radius: 0**;
  visible grid lines; tables used AS tables; default-looking form controls elevated with
  thick borders. Density is fine — brutalism doesn't need whitespace to breathe, it needs
  hierarchy through SIZE.

## Section blueprint

1. **Header** — thick bottom border; wordmark left (heavy, maybe rotated tag "EST. 2026");
   nav as bordered tabs/buttons; a ticking clock or visitor counter in mono (raw honesty
   motifs).
2. **Hero** — enormous stacked words filling the viewport (each line its own hover-reactive
   block, maybe alternating fill/outline via `-webkit-text-stroke`), or a giant bordered
   "poster" panel with hard shadow. One loud CTA button that visibly DEPRESSES on click
   (translate 3px + shadow shrink — the signature interaction).
3. **The stack** — content as a pile of bordered cards/panels, deliberately misaligned
   (±1–2° `rotate` on alternating cards), hard shadows, sticker/stamp elements
   ("★ NEW", price tags) absolutely positioned across borders.
4. **Marquee** — thick-bordered strip, uppercase, fast (motion-recipes §6).
5. **List/table section** — an actual `<table>` or definition list with full borders: specs,
   lineup, catalog. Brutalism celebrates tabular data.
6. **Footer** — oversized, bordered grid of links; colophon in mono ("HTML by hand.
   No cookies."); maybe the wordmark repeated gigantically and clipped.

## Signature moves (choose 4–5)

| Move | Recipe |
|---|---|
| Depress-on-click buttons | `:active { translate: 3px 3px; box-shadow: 3px 3px 0 #000 }` |
| Hard-shadow hover lift | hover: `translate: -2px -2px; box-shadow: 8px 8px 0` |
| Outline/fill text swap on hover | `-webkit-text-stroke: 2px #000; color: transparent` ↔ filled |
| Rotated stickers/stamps | absolute, `rotate(-6deg)`, border 3px, accent bg |
| Cursor-reactive tilt on the hero poster | small JS: pointer → `rotateX/Y` ≤ 3° |
| Instant page transitions | NO fade — brutalism cuts, doesn't dissolve. View transitions off or ≤ 100ms |
| Marquee strip | §6, thick borders top/bottom |
| Konami/click easter egg that inverts the whole palette | `filter: invert(1)` class on `<html>` |

Motion language: **snappy and mechanical** — durations 0.15–0.3s, `steps()` easing where it
fits, zero smoothness worship. Lenis is BANNED in this style; native scroll is the point.
Grain optional; harsh halftone/dither patterns (code-assets patterns) fit better.

## Asset slots

| id | dimensions | role |
|---|---|---|
| poster-hero | 2000×2400 | hero panel art — harsh-flash photo, halftone, or bold vector |
| stack-XX | 1600×1200 | card images, same harsh treatment |
| sticker-set | SVG | stamps/badges — code assets |
| og-default | 1200×630 | share card — looks like a printed flyer |

Art direction for generated images: "harsh direct flash photography, high contrast" or
"risograph/halftone print texture, 2 spot colors" — one treatment, all images. CSS can fake
the riso look on any source: `filter: grayscale(1) contrast(1.4)` + `mix-blend-mode`
duotone with the accent.

## Do / Don't

- DO keep usability pristine underneath the noise: this style still must pass the full
  quality-bar — contrast is easy (black on white), focus states are natural (thick outlines),
  semantics are the aesthetic.
- DO commit 100%: every border same weight, every shadow same offset — the system IS rigid,
  that's what separates "designed" from "broken."
- DON'T mix in soft shadows, rounded corners, or glassmorphism anywhere. One soft element
  breaks the spell.
- DON'T sacrifice reading comfort: body text still 16px+, measure still ≤ 75ch.
- DON'T use Comic Sans ironically. The style is sincere.

## Mini-QA

- Squint test: hierarchy still obvious when blurred (size does the work)
- Every interactive element has the depress/lift behavior — consistency check
- 360px: borders don't double up into mush; shadows scale down (4px offsets)
- The site is FAST (this style should score 100 on Lighthouse — it's mostly HTML/CSS)
- It looks like a decision, not an accident: show a stranger — they should say "cool," not "is it broken?"
