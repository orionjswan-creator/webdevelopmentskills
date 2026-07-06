---
name: starter-kits
description: Build and maintain the agency's own reusable starter templates — one original, fully-owned codebase per style skill, designed to be repopulated per client (tokens, copy, manifest assets) so every new project starts at ~60% done. The legitimate, compounding version of "grab a framework and reskin it." Use when creating a kit for a style, starting a client project from a kit, or harvesting improvements back into a kit after a project ships.
---

# Starter Kits

The speed the "download-and-reskin" fantasy promises actually comes from here: **original
starters we own**, one per style skill, engineered from day one for repopulation. A kit is
not a demo site — it's the style skill's blueprint implemented as clean, tokenized,
slot-driven code with placeholder everything. New client → new tokens + copy deck + asset
manifest → the site is 60% done in an afternoon, and 100% of it is ours to sell.

Kits live in `kits/<style-name>/` in this repo (or the agency's private kits repo).

## Anatomy of a kit (what "engineered for repopulation" means)

```
kits/<style>/
  README.md            # what's inside, repopulation steps, what to customize vs keep
  tokens/tokens.css    # THE swap surface: colors, type, spacing, radii, motion tokens
  src/sections/        # every blueprint section as a component with content SLOTS
  src/components/      # the ui-patterns set, tokenized (nav, buttons, forms, cards…)
  src/motion/          # motion-recipes pre-wired, reading motion tokens + reduced-motion
  content/copy.md      # the copy deck TEMPLATE (site-copywriter's slot structure)
  assets/manifest.md   # manifest STUB with every slot pre-listed + placeholder script wired
  demo/                # the kit running with fictional brand "Studio Norr" (proof + QA rig)
```

**The three rules that make a kit repopulatable:**
1. **No literal anywhere** — every color/size/duration reads a token; every string reads
   the copy deck; every image reads a manifest ID. `grep` for hex codes and quoted prose
   in components = kit bug.
2. **Sections take content, never contain it** — a section component's props/slots mirror
   ux-architecture's text-wireframe fields (headline, proof, CTA…), so ARCHITECTURE.md
   maps mechanically onto the kit.
3. **The demo brand is deliberately unlike any client** — fictional, neutral-but-complete
   (real copy voice, full manifest), so nothing from the demo ever leaks into a delivery
   and the kit is testable end-to-end at all times.

## Building a kit (once per style; ~the effort of one real site)

1. Read the style skill top-to-bottom; the kit implements its **blueprint, stack choice,
   and signature moves** exactly — the kit IS the style skill, compiled.
2. Scaffold per the style's stack (tech-stack-guide). Tokens first, from the style's
   token directions with the demo brand's choices.
3. Build every blueprint section + the ui-patterns component set, slot-driven.
4. Wire motion via motion-recipes with the style's choreography defaults — behind tokens
   (`--dur-reveal`, `--ease-reveal`) so motion personality is swappable too.
5. Fill the demo: fictional brand, copywriter-quality copy deck, full manifest with
   generated/placeholder assets.
6. QA the demo against quality-bar.md as if shipping it. A kit that doesn't pass can only
   mass-produce mediocrity.
7. Write the kit README: repopulation steps, the "keep vs customize vs replace" map
   (tokens/copy/assets always change; section order often changes; components rarely;
   motion grammar almost never).

## Repopulating for a client (the fast path this exists for)

1. Inputs: BRIEF.md + DIRECTION.md (+ ARCHITECTURE.md if multi-page). Copy the kit to the
   client repo — never build clients inside the kits repo.
2. **Token pass** (hours, not days): palette, type pairing, spacing/radius personality,
   motion tokens from DIRECTION.md. Because everything reads tokens, this alone re-skins
   the site coherently.
3. **Structure pass**: reorder/add/remove sections per ARCHITECTURE.md; a section the
   architecture needs but the kit lacks gets built fresh (and flagged for harvest).
4. **Content pass**: site-copywriter fills the copy deck; asset-creation regenerates the
   manifest for the client's art direction; placeholder script gives instant coherence.
5. **The 40% that makes it theirs**: DIRECTION.md's "one creative risk" — the signature
   moment is always custom-built per client, never from the kit. Kits deliver the floor;
   the signature delivers the fee.
6. Full pipeline QA (site-builder Phases 7–10) as usual — kits skip *rework*, never checks.

## The harvest loop (why kits compound)

After every shipped project, spend 30 minutes: which new sections/components/recipes were
built? Generalize the reusable ones back into the kit (slots, tokens, demo content),
version-bump with a changelog line. Teardown findings (site-teardown) and casebook
lessons land here too — implemented from scratch as kit improvements. Two years of this
loop is an agency's real technical moat: a private library that gets faster and better
per project, with zero provenance risk.

## Provenance rules (what keeps kits sellable at agency prices)

- Everything in a kit is written by us or licensed for unlimited client redistribution
  (MIT/permissive libs fine; "one-project" template licenses NOT fine in a kit).
- No code, markup, or assets from torn-down or downloaded sites, ever — patterns from
  TEARDOWN.md are re-implemented fresh (the teardown skill's line applies with zero
  exceptions here, because kit code multiplies across every future client).
- Track licenses in the kit README (fonts especially — demo fonts must be freely
  licensed; client fonts swap in per brand-identity's licensing step).
- A client buys the *delivered site* — the kit itself stays agency IP; say so in the SOW
  (client-discovery's assumptions section).
