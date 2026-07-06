---
name: saas-product-style
description: Premium SaaS / developer-product marketing style — the polished dark-or-light product site with cinematic feature reveals, real UI as the hero asset, and conversion-grade information architecture. Use via the site-builder skill for software products, dev tools, APIs, and B2B platforms with multiple pages (home, features, pricing, docs, changelog).
---

# Style: SaaS Product

The genre defined by the best product-company sites of the 2020s: engineering credibility
expressed as design precision. Distinct from viral-trending (a launch moment) — this is a
**durable multi-page product presence** where the product UI itself is the star asset. The
feeling to create: **"this tool is obviously well-built."**

## Stack (this skill's choice)

**Next.js (App Router) + Tailwind v4 + Framer Motion**, GSAP for the 1–2 scroll scenes,
MDX for changelog/blog, `@vercel/og` for share cards. This genre practically defines the
Next/Vercel deployment path. Docs: Fumadocs/Nextra or a `/docs` MDX route group.

## Design tokens

- **Palette**: pick a lane and commit — (a) engineering dark: layered `#0b0c0e`→`#15171a`
  surfaces, 10% borders, one precise accent (blue-violet, emerald, amber); or (b) crisp
  light: `#fbfbfa` canvas, `#111` ink, cool gray borders, saturated accent. Semantic tokens
  from day one (`--surface-1/2/3`, `--border`, `--accent`) — this genre demands theme rigor.
- **Type**: precision grotesques — Geist-adjacent but distinctive: Hanken Grotesk, Instrument
  Sans, or Switzer (Fontshare) for UI/body; headlines either the same family at −0.03em
  tracking and 600–700 weight, or a serif contrast (Fraunces) for a humanist brand. Mono is
  mandatory somewhere real: code snippets, keyboard shortcuts, API examples — JetBrains Mono
  or Geist Mono.
- **Layout**: 1200px container, centered hero, alternating full-width feature scenes;
  radius 8–12px; depth via borders + very soft large shadows (dark: borders only). Density
  is the tell: tighter than editorial, airier than a dashboard.

## Section blueprint

**Home**
1. **Hero** — headline states the job-to-be-done in ≤ 8 words (verb-first), subline names the
   user, primary CTA ("Start free" / "npm install …" copy-button for dev tools) + secondary
   ("Book demo" / "Docs"). Below: **the product itself** — a real, current UI screenshot in a
   browser/app chrome frame, slightly 3D-tilted or straight-on, with a soft accent glow
   behind it. Optionally a 15–30s silent product clip with poster.
2. **Logo row** — "Trusted by" (real logos only; omit the section entirely if none).
3. **Feature scenes ×3–4** — each: eyebrow label (mono), headline, 2 lines of copy, and a
   focused UI crop or micro-demo (animated cursor performing the action — a Framer Motion
   sequence over a screenshot, or a real embedded component). Alternate text/media sides.
   Reveal on scroll (§2/§10); ONE scene may be a pinned scrub (§3).
4. **The workflow/architecture moment** — for dev tools: a code block that types itself
   (real, runnable code) next to the visual result; for B2B: an integration/flow diagram in
   brand style (SVG, code asset — never a screenshot of a whiteboard tool).
5. **Proof** — one flagship case-study card with a real metric + short testimonial wall.
6. **Pricing teaser** → pricing page; **Final CTA** band with the install command/CTA repeated.

**Pricing page** — the conversion workhorse: 3 tiers max on screen, highlighted recommended
tier, feature-comparison table that collapses gracefully on mobile (sticky column headers),
honest FAQ (accordion) answering the real objections (limits, security, cancellation, SSO).

**Changelog** — dated MDX entries, mono dates, terse confident notes; this page signals a
living product — juries and buyers both check it.

## Signature moves (choose 4–5)

| Move | Recipe |
|---|---|
| Framed product shot with accent glow | CSS: chrome frame component + radial glow pseudo-element |
| Self-typing code block | rAF/Framer sequence; `aria-live="off"`, instant-complete on reduced-motion |
| Animated-cursor micro-demos | Framer Motion path animation over UI crop |
| One pinned scrub feature scene | motion-recipes §3 |
| Copy-to-clipboard install command | button + "Copied ✓" morph |
| Keyboard-shortcut chips | `<kbd>` styled to the token system |
| Gradient-border highlighted pricing tier | padding-box/border-box gradient trick |
| Command-palette easter egg (⌘K) | small; even a nav-only palette lands the "built by tool people" signal |

## Asset slots

| id | dimensions | role |
|---|---|---|
| ui-hero | 2880×1800 | main product screenshot — REAL UI, current version |
| ui-crop-XX | 1600×1200 | per-feature focused crops |
| demo-clip | 1920×1080 mp4/webm | optional silent hero clip + poster |
| diagram-flow | SVG | architecture/integration diagram (code asset) |
| case-logo-set | SVG | customer logos (`awaiting-user`) |
| og-default + og-template | 1200×630 | share cards (code-generated) |

**The cardinal rule of this style: never fake the product.** UI screenshots are `awaiting-user`
or produced by actually running the product and capturing it (an agent can often do this —
build, run, screenshot). A designed-but-fictional UI mock is acceptable ONLY for pre-launch
products and the manifest must mark it `role: concept-ui`.

## Do / Don't

- DO make the first fold answer: what is it, who's it for, what do I click. Buyers scan.
- DO show real product density — empty-state screenshots look like vaporware.
- DON'T ship feature-grid-of-icons sections (the 2022 template tell); every feature gets a
  visual proof instead.
- DON'T animate anything a buyer needs to read while it's still moving.
- DON'T use the dated "AI gradient + sparkles" packaging (trend-report ban list).

## Mini-QA

- A stranger can say what the product does within 5 seconds of the hero
- Install/CTA command actually works as written
- Pricing table honest, keyboard-navigable, readable at 360px
- All UI imagery reflects the real current product (or is marked concept-ui)
- LCP < 2s with the hero screenshot preloaded
