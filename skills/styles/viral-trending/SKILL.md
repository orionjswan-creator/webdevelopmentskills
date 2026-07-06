---
name: viral-trending-style
description: The 2026 trending/viral look — dark-mode-first, bento grids, kinetic gradients, controlled glassmorphism, one screenshot-able signature moment engineered for sharing. Use via the site-builder skill for launches, waitlists, AI products, tools, drops, and anything meant to spread on social.
---

# Style: Viral Trending

Built from what's currently spreading (trend-report-2026.md is this skill's research base):
sites designed to be screenshot, clipped, and shared. The feeling to create: **"have you SEEN
this site?"** Everything serves one engineered shareable moment plus a conversion path.

## Stack (this skill's choice)

**Next.js (App Router) + Tailwind v4 + Framer Motion**, GSAP only if a scroll-scrub scene is
needed. Launch pages need OG-image generation (`@vercel/og`), fast global deploys (Vercel),
and A/B-able components — Next is optimal. Single static landing with no app? **Astro**.

## Design tokens

- **Dark-mode first** (fully committed): layered darks — canvas `#0a0a0c`, raised surfaces
  `#131318`, borders at 8–12% white. Text: 92% white primary, 60% secondary. Accent: one
  saturated hue used as **glow** (kinetic gradient + focus rings + key CTA), optionally a
  second for gradient blends. Avoid the dated purple-blue "AI gradient" — pick an unexpected
  pair (acid lime + deep teal, hot coral + amber…).
- **Type**: distinctive grotesque with personality — Bricolage Grotesque, Cabinet Grotesk, or
  Clash Display for headlines; Hanken Grotesk or Satoshi body; Geist Mono / JetBrains Mono for
  the code/stat/label layer (mono is a load-bearing style element in this genre).
- **Layout**: centered narrative column (720–840px) for the story + full-width bento sections;
  radius 12–16px on cards; 1px borders everywhere (borders, not shadows, define depth on dark).
  Grain overlay at 3–4%.

## Section blueprint (launch/product one-pager)

1. **Hero** — kinetic gradient field (motion-recipes §11) behind a huge headline that states
   the value in ≤ 7 words; subline ≤ 2 lines; primary CTA (waitlist/install/buy) + social-proof
   micro-row (avatars, count, one-line quote, or GitHub stars — real numbers only). Optional
   announcement pill above the headline ("Now in beta ↗").
2. **The signature moment** — the reason the site gets shared. Choose ONE and execute at
   demo-quality: an embedded interactive demo of the product; a playful WebGL toy (§12);
   a scroll-scrubbed product reveal (§3); or a live-data visual. It must read in a 3-second
   muted clip.
3. **Bento grid** — features as varied-size cells; every cell earns its size; at least one
   LIVE cell (animated counter, mini demo loop, real-time stat). Hover: lift + border glow
   (`box-shadow: 0 0 0 1px accent/40`) + optional spotlight (radial gradient tracking cursor).
4. **How it works** — 3 steps, mono-numbered, native scroll-driven reveals (§10).
5. **Proof** — testimonials as chat-style cards or a wall of short quotes; logos row
   (grayscale, hover→color); metrics with count-up on first view.
6. **Pricing** (if any) — 2–3 cards, one highlighted with the gradient border trick
   (`background: linear-gradient(canvas,canvas) padding-box, kinetic-gradient border-box`).
7. **Final CTA** — the headline restated as imperative + the same primary button; footer
   minimal with an easter egg (see below).

## Signature moves (choose 4–5)

| Move | Recipe |
|---|---|
| Kinetic gradient hero + grain | motion-recipes §11 + code-assets §1 |
| Bento with one live cell + hover glow | CSS grid + `grid-template-areas` |
| Glassmorphism nav ONLY (blur 12px, 1px inner border) | trend-report rules |
| Count-up metrics on first view | IntersectionObserver + rAF tween |
| Spotlight-follow on cards | CSS var `--mx/--my` from pointermove, radial-gradient |
| Announcement pill with shimmer sweep | CSS mask + translate animation |
| One scroll-scrub product scene | §3 |
| Easter egg (konami code / logo×5 click → toy mode) | small, hidden, clip-able |

## Viral mechanics (this style's special sauce)

- **Design the OG card as hard as the hero** — it's the first impression on every share.
  Per-page dynamic OG via `@vercel/og`, matching the kinetic-gradient look.
- **The 3-second rule**: signature moment must land in a muted 3-second screen recording at
  Twitter/X compression. Test exactly that.
- **Give people something to DO**: interactive beats watchable; a 10-second toy or live demo
  gets recorded and reposted (the Bruno Simon lesson).
- **Copy is screenshot bait**: one spicy/confident line people will quote-post — place it as
  a standalone styled section.
- **Speed IS the aesthetic**: this genre's audience notices load time; hit LCP < 1.5s here,
  stricter than the base budget.

## Asset slots

| id | dimensions | role |
|---|---|---|
| product-shot / demo-frames | 2400×1500 | the product, in the dark UI chrome |
| og-dynamic template | 1200×630 | code-generated, per-page title |
| avatar-set (if no real users) | 96×96 ×6 | ONLY real or clearly-illustrative — never fake real users |
| toy/3d asset | glTF | if signature moment is WebGL |

Most of this style's assets are code (gradients, bento content, UI shots via styled
screenshots) — the manifest should be short.

## Do / Don't

- DO commit to dark fully; DO keep the narrative column readable and the CTA always ≤ 1
  scroll away (sticky nav CTA after hero).
- DON'T fake social proof — invented user counts/avatars/testimonials destroy launches; use
  `awaiting-user` slots or design the section to work without numbers.
- DON'T stack every trend; this skill's list is a menu, and the trend-report's "dated" list
  is a hard ban.
- DON'T gate the signature moment behind the fold or a click.

## Mini-QA

- Muted 3-sec recording of the signature moment survives social compression and still wows
- OG card renders correctly in a card validator; looks designed, not defaulted
- LCP < 1.5s, bento hover 60fps, kinetic gradient doesn't bang (grain applied)
- Light-mode users aren't broken: either a real light theme or a deliberate, tested dark-only
  with `color-scheme: dark`
