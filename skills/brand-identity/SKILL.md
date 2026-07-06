---
name: brand-identity
description: Build the identity system that the website expresses — wordmark/logo system, color and type decisions as brand (not just site) assets, voice definition, and a compact brand guidelines deliverable (BRAND.md + kit files). Use when a client has no usable identity, when rebranding is in scope, or when the engagement should deliver "brand + site" — the classic premium agency package.
---

# Brand Identity

At agency tier, the site usually *is* the brand's most complete expression — and half of
premium clients arrive with no real identity system (a logo JPEG and a favorite color).
This skill produces a compact, honest identity system that the style skills can express,
and packages it so it outlives the website: business decks, socials, signage, packaging
briefs all draw from the same kit.

**Scope honesty:** this is identity design *at web-agency scope* — a wordmark system, color
and type architecture, voice, and guidelines. A full brand strategy engagement (naming,
research-driven positioning studies, trademark work) is a different contract; say so when
the client needs it.

## Inputs

`DISCOVERY.md` (the adjectives, the refused competitors, verbatim customer quotes) and
`RESEARCH.md` (the visual landscape — the identity must be distinguishable *within it*).

## Workflow

### 1. Identity strategy (one page, before any visuals)

```md
# IDENTITY-STRATEGY.md
- Positioning line: <what only this brand can say — from discovery>
- Personality: the 5 adjectives, ranked; the 3 nevers
- Archetype register: <e.g. the craftsman, the guide, the maverick — one, committed>
- Landscape gap: <from RESEARCH.md — what the identity must look UNLIKE>
- Expression priorities: <where the brand lives most: screen? menus? packaging? signage?>
```

### 2. Wordmark system

Follow code-assets §3 (typographic wordmark, hand-tuned, converted to paths) with identity-
grade rigor:

- Explore 3 directions in the chosen display face's register (tight/confident, spaced/
  refined, heavy/loud); pick with the client via client-delivery's presentation method.
- The ONE distinguishing move (modified glyph, clipped counter, accent mark) — ownable,
  describable in a sentence, visible at 16px.
- Deliver the system: primary wordmark · monogram (favicon/avatar/stamp) · stacked and
  horizontal lockups · clearspace rule (x-height based) · minimum sizes · single-color,
  reversed, and mono variants. All SVG (paths, not text), plus PNG exports.
- If a symbol/mark beyond the monogram is truly needed, spec it via asset-creation
  (Recraft for vector exploration, then hand-refine) — but most premium brands under 50K
  are best served by a superb wordmark, and saying so is part of the value.

### 3. Color architecture (brand level, not just site level)

- Core: 1 dominant + 1 ink + 1–2 accents, chosen in OKLCH, with the design-taste rules
  (temperature commitment, 85/10/5 usage).
- Extended: the tints/shades scale for UI states, and the "never" list (colors adjacent
  competitors own — from RESEARCH.md).
- Define per-context: screen (hex/OKLCH), print (CMYK approximations, noted as untested
  unless proofed), and accessibility pairings (which text colors sit on which fields —
  pre-validated contrast pairs the site inherits for free).

### 4. Typography as brand asset

- The pairing (per design-taste's logic) PLUS licensing reality: name the exact licenses
  (Fontshare/Google = free including commercial; foundry faces = webfont + desktop seats
  priced into the SOW). License risk is an agency-tier deliverable — clients get sued for
  font misuse, agencies get fired for it.
- Usage rules: display/body/mono roles, the scale, casing policy, and the "voice in type"
  examples (a headline set right vs. wrong).

### 5. Voice (with site-copywriter)

The VOICE.md from site-copywriter is elevated to a brand asset: comparison persona,
say/never-say pairs, three worked examples (a headline, an error message, an Instagram
caption) — the caption proves the voice works beyond the site.

### 6. Package: `BRAND.md` + `/brand-kit`

`BRAND.md` — the compact guidelines (10–15 sections, screenshots/embeds of real usage from
the site once built): strategy page · wordmark system + rules · color architecture ·
typography + licenses · voice · imagery art direction (the manifest's block, promoted to
brand law) · motion personality (the site's easing/duration tokens described as brand
behavior) · application examples · file index.

`/brand-kit` — the files: `svg/` (all lockups + variants) · `png/` (standard exports) ·
`tokens.css` + `tokens.json` (the same tokens the site uses — one source of truth) ·
`fonts/` (licensed files or acquisition instructions) · social avatar/banner crops ·
`og-template` (from code-assets §6).

## Working relationship with the site

- Identity phase runs between discovery and site-builder Phase 1: DIRECTION.md then
  *expresses* the identity rather than inventing one per-site.
- Tokens flow one way: brand-kit → site. When the site's build reveals a token problem
  (contrast failure, accent inflation), fix it in the kit and re-flow — never fork.
- The asset manifest's art-direction block and BRAND.md's imagery section are the same
  text, maintained in the kit.

## Do / Don't

- DO show identity directions in *context* (on a hero mock, a menu, an Instagram grid) —
  never as a logo floating on white; approval quality depends on it.
- DO version BRAND.md; identities evolve and the kit is the changelog.
- DON'T deliver 40-page brand books for a 3-person business — compact and used beats
  comprehensive and ignored.
- DON'T generate logos with image models — vector exploration via Recraft is a sketch
  tool; the shipped mark is deliberately constructed, path-clean, and license-clear.
- DON'T let the client's old logo quietly veto the new system — if keeping it is the
  brief, scope this skill down to "system around an existing mark" explicitly.
