---
name: cms-integration
description: Make a designed site client-editable without breaking the design — CMS selection, schema design from the content model, editor experience (previews, validation, guardrails), migration, and the editor guide deliverable. Use when the client will edit content post-launch (most premium engagements), when asked to add a CMS, or when wiring Shopify/Sanity/Payload/Keystatic into a build.
---

# CMS Integration

The premium-engagement truth: the site the jury sees is the site on launch day; the site
the client has in a year is the site the CMS allowed. This skill's job is **editability
that cannot break the design** — the client changes words, images, and entries; the system
defends tokens, layout, and craft.

## 1. Choose the engine (from discovery's "who edits, how often" answer)

| Situation | Engine | Why |
|---|---|---|
| Marketing team edits weekly, needs previews/scheduling | **Sanity** | Structured content, live preview, portable text, mature roles |
| Dev-adjacent client, TS stack, wants self-hosted | **Payload** | Code-first schema, admin included, owns their data |
| Rare edits, technical client, zero budget for services | **Keystatic / MDX in repo** | Git-based, no infra, PR-reviewable edits |
| Commerce | **Shopify** (products/orders) + one of the above for editorial | Never model products outside the commerce engine |
| Client already lives in WordPress and won't move | Headless WP (REST/WPGraphQL) | Meet them where they are; keep the front end ours |

Decision rules: the fewest moving parts that satisfy the *actual* editing cadence;
hosted-service costs go in the SOW's assumptions; "we might want to edit everything" is
answered with the guardrail principle below, not with a page builder.

## 2. Schema design (from ux-architecture's content model)

Translate ARCHITECTURE.md's content types 1:1 into schema — then apply the guardrails:

- **Structured fields, not rich-text oceans.** A Room is `name, strapline (max 90 chars),
  description (portable text, 2 block types), gallery (3–8 images), amenities (refs),
  rate, bookingUrl` — NOT one WYSIWYG blob. Every field the design depends on is a field,
  with validation (lengths, required, formats) mirroring what the design can hold.
- **Sections as a curated block library.** Page composition = an array of *designed*
  section types (the style skill's blueprint sections, parameterized). The client reorders
  and fills blocks; they do not invent layouts. No arbitrary-nesting page builders — that's
  how award sites become Frankenstein sites by month six.
- **Images carry the manifest contract**: image fields require alt text (validation, not
  convention), declare aspect ratio + min dimensions in the field description, and crop
  server-side to the design's ratios (hotspot/focal-point where the engine supports it).
- **Singletons for globals** (nav, footer, announcement, SEO defaults), documents for
  entries, references over duplication. Slugs auto-generated, editable with warning.
- **Editorial workflow**: draft → preview → publish; scheduled publish where the engine
  offers it; roles per discovery (who may publish vs. draft).

## 3. Front-end wiring

- Type the schema (codegen where available — Sanity typegen, Payload's TS types) so
  content and components stay contract-bound; a schema change that breaks a component
  fails the build, not production.
- Previews: draft-mode routes so editors see the REAL site (Next draft mode / Astro
  preview deploys). An editor who can't preview will publish to check — install previews
  before training.
- Revalidation: webhook → ISR/on-demand revalidate (or rebuild for SSG) — document the
  publish-to-live latency in the editor guide ("changes appear within ~2 minutes").
- Empty/overflow states: components handle missing optional fields and maximum content
  gracefully (the audit item nobody tests: 12 amenities, a 3-line strapline, zero journal
  posts). Test schema extremes before handoff.
- Performance holds: CMS images through the image pipeline (formats, sizes, lazy) —
  quality-bar budgets apply to CMS-fed pages at content extremes, not just launch content.

## 4. Migration & seed

Migrate existing content (old site, docs, spreadsheets) via script where count > ~20
entries; hand-enter below that. Every entry passes the same validation as new content —
migration is the moment to fix alt text, lengths, and naming, not to defer them. Seed
example entries for every type demonstrating *ideal* content (they double as training
material and the copy deck's voice reference).

## 5. The editor guide (deliverable, part of the handoff package)

`EDITOR-GUIDE.md` — written for the actual editor from discovery, plain language:

- The 5 most common tasks, step-by-step with screenshots (add a journal post, change a
  rate, swap a hero image, update hours, add a team member).
- The image rules (sizes, alt text, "portrait photos need to be at least…").
- Preview → publish → "when will it appear live".
- The 3 things never to touch, and why, kindly.
- What to do when something looks wrong (revert via version history — show them where).

This guide plus client-delivery's recorded training session is what "the client can run
their site" actually means.

## Don'ts

- Don't expose design decisions as content fields (no color pickers, no font dropdowns,
  no spacing sliders) — tokens are code, and that's the guardrail that preserves the
  award-level design.
- Don't model content the client will never edit (build-time constants stay in code).
- Don't hand over without previews, validation, version history verified, and at least
  one non-technical person having successfully completed task #1 unaided.
