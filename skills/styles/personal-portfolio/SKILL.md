---
name: personal-portfolio-style
description: Personal portfolio style for designers, developers, and creatives — either "quiet craft" minimal or "playful signature" interactive. Small surface, maximum polish per pixel, built to get its owner hired or remembered. Use via the site-builder skill for individual portfolios, CVs, and personal sites.
---

# Style: Personal Portfolio

The most personal genre — and the one where a single well-executed idea wins awards (Bruno
Simon's drivable-car portfolio remains the reference for the playful pole; countless
SOTD-winning minimal developer/designer folios define the quiet pole). Small scope is the
advantage: **fewer pages, deeper polish.** The feeling to create: **"I need to work with this
person."**

## First decision: pick a pole (ask the user, or infer from their field)

- **Quiet craft** — typographic, restrained, work-first. For designers/developers whose work
  should speak. 90% of portfolios should pick this.
- **Playful signature** — one interactive idea IS the site (a toy, a 3D scene, a game
  mechanic). Only when the person's craft is interaction/3D/creative dev and the idea is
  genuinely theirs — a borrowed gimmick reads instantly.

## Stack

Quiet craft: **Astro (or Vite vanilla) + CSS + a pinch of GSAP.**
Playful signature: **Vite + TypeScript + Three.js** (R3F if React-based work samples embed).
Either way: tiny bundle, instant load — a slow portfolio is a self-review.

## Design tokens

- **Palette**: one confident decision — bone white + ink + a single personal accent, or a
  committed dark. The accent should feel like the person, not a brand system.
- **Type**: ONE excellent family used with range (weights, optical sizes, italics) —
  Fraunces, Instrument Serif + Sans duo, Cabinet Grotesk, or Zodiak. Mono for meta
  (role, years, stack). Name in the display cut at `clamp(2.5rem, 8vw, 7rem)`.
- **Layout**: narrow personal column (640–760px) for words; work images break wide.
  Generous line-height; the whole site should feel like a well-set letter.

## Section blueprint (single page + optional case-study pages)

1. **Intro** — name, one-line self-definition (specific beats grand: "Design engineer
   building creative tools" > "Digital creative"), availability status line (mono, honest:
   "Open to freelance from September"), location/timezone. Masked line reveal (§2) and
   that's nearly all the intro motion needed.
2. **Selected work** — 3–6 pieces MAX (curation is the skill being demonstrated):
   - Quiet: list rows (title, role, year) with hover preview image (§7 variant), or 4:3
     cards with §13 hover. Each links to a case study or live piece.
   - Playful: work embedded IN the interactive scene (billboards in the world, objects to
     collect) — but always with a plain-HTML list fallback below/behind (recruiters skim).
3. **Case study template** (the hiring page): problem → role → 2–4 key decisions with
   visuals → outcome with a real number if possible → next-project link. Short. Honest.
4. **About** — 2 paragraphs voice-forward + a real photo (or a personal illustration style),
   current stack/tools in mono chips, past clients/employers as a plain list.
5. **Contact/footer** — email as the biggest link on the page (magnetic §7), socials as
   text links, colophon ("Built with Astro + GSAP · Set in Fraunces · v3, 2026" — the
   colophon is a genre handshake).

## Signature moves

Quiet craft (choose 3): list-hover preview (§7) · masked reveals (§2) · view-transition
morphs into case studies (§9) · availability dot pulsing live · `::selection` in the accent ·
time-of-day greeting or local-time clock (mono) · one tasteful surprise (logo click →
palette flip).

Playful signature (choose the ONE idea + supports): the interactive centerpiece (drivable/
draggable/physics toy, §12-based scene) · progress/score element that makes exploration a
game · sound design (opt-in only) · plain-HTML mirror of all content for skimmers and SEO.

## Asset slots

| id | dimensions | role |
|---|---|---|
| work-XX-cover | 1600×1200 | per-project cover (real work screenshots — `awaiting-user`) |
| work-XX-case-N | 2000×1250 | case-study visuals |
| portrait | 1200×1500 | about photo (`awaiting-user`; generated portraits are banned — it's a personal site) |
| og-default | 1200×630 | name + one-liner card, code-generated |
| toy-assets | glTF/textures | playful pole only |

**Real work only.** This style's manifest is mostly `awaiting-user`: actual screenshots,
actual outcomes. The asset skill's job here is specing the shot list (crop, chrome, ratio)
and grading for consistency — not generating fictional work.

## Do / Don't

- DO cut the seventh project. And the sixth. Show the best 3–5.
- DO write case studies in first person with opinions ("I pushed back on X because Y").
- DO put email in plain text — no contact forms on a personal site.
- DON'T fake metrics, logos, or generate a fictional face/work. Credibility is the product.
- DON'T (playful pole) let the toy block content: 3-second rule to reach work, always a
  visible "skip" path, and the HTML fallback for reduced-motion/mobile.

## Mini-QA

- A recruiter finds name → best work → contact in under 15 seconds, keyboard-only included
- Case studies readable on a phone on a train (offline-tolerant images, no jank)
- Playful pole: toy at 60fps on a mid-range laptop, poster+list fallback verified
- The colophon is true (it will be checked by exactly the people the site targets)
- Lighthouse ~100 across the board — a personal site has no excuse
