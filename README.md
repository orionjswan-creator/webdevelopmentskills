# Award-Winning Website Skills

A skill library for AI coding agents (Claude Sonnet 5 / Codex 5.5 / Codex) that replicates the
*craft* of award-winning and viral websites — the layout systems, animation choreography,
typography, and interaction patterns behind Awwwards SOTD/SOTY, FWA, and CSSDA winners and
2026's trending sites — so you can build at that level with your own brand and content.

These skills encode **patterns and techniques, not clones**. Every site built with them is an
original design that meets the bar award juries score against:
**Design 40% · Usability 30% · Creativity 20% · Content 10%** (the Awwwards evaluation weights).

## The pipeline

```
1. BRIEF     Describe the site (brand, audience, pages, tone).
                  │
2. STYLE     Pick a style skill — it sets the aesthetic, the optimal tech
             stack, section blueprints, and motion language.
                  │
3. ASSETS    skills/asset-creation (built for Codex): generates every asset
             code can make (SVG, textures, gradients, shaders, favicons, OG
             images), writes assets/manifest.md with per-tool AI-image prompt
             specs, creates labeled placeholders, and interviews you for
             anything it can't infer — or leaves TODO(describe:) slots.
                  │
4. BUILD     skills/site-builder (built for Sonnet 5 / Codex 5.5): 10-phase
             pipeline — brief → written direction → scaffold → tokens →
             structure → asset wiring → motion → responsive → a11y → perf →
             self-scored QA against the award rubric.
                  │
5. WORDS     skills/site-copywriter: voice sheet + full copy deck + microcopy
             (can run any time after the brief).
                  │
6. LAUNCH    skills/launch-seo: technical SEO, share cards, analytics,
             deploy verification, award-submission kit.
                  │
   AUDIT     skills/site-auditor: score any existing site against the rubric
             and get a prioritized fix plan (entry point for improving sites
             not built with this library).
```

Cross-cutting partners: **competitive-research** runs before step 2 when the market matters;
**design-taste** and **ui-patterns** back every design decision in steps 2–4; and
**rapid-site-sprint** replaces the whole pipeline with a same-day fast path when speed is the
brief.

Steps 3 and 4 run in either order or in parallel — every image slot is wired to a manifest ID
and the site builds with placeholders; real images drop in later with zero code changes.

## The skills (16)

### Core pipeline

| Skill | For | What it does |
|---|---|---|
| [`site-builder`](skills/site-builder/SKILL.md) | Sonnet 5 / Codex 5.5 | Orchestrator: brief + style + manifest → finished site, self-scored against the award rubric |
| [`asset-creation`](skills/asset-creation/SKILL.md) | Codex | Code assets + asset manifest with AI-image prompt specs + placeholders + user interview |

### Styles (each picks its own optimal stack)

| Skill | Genre | Stack it chooses |
|---|---|---|
| [`immersive-agency`](skills/styles/immersive-agency/SKILL.md) | Awwwards-SOTD agency/portfolio: WebGL hero, scroll storytelling, custom cursor, huge type | Vite + vanilla TS + GSAP + Lenis + Three.js |
| [`ecommerce-brand`](skills/styles/ecommerce-brand/SKILL.md) | Luxury commerce: full-bleed imagery, editorial PLP/PDP, refined micro-interactions | Next.js + Tailwind + headless Shopify |
| [`editorial-studio`](skills/styles/editorial-studio/SKILL.md) | Magazine/studio: dramatic serif type, broken grids, kinetic type moment | Astro + GSAP islands |
| [`viral-trending`](skills/styles/viral-trending/SKILL.md) | The 2026 launch look: dark-first, bento, kinetic gradients, one engineered shareable moment | Next.js + Tailwind + Framer Motion |
| [`saas-product`](skills/styles/saas-product/SKILL.md) | Premium product site: real UI as hero, cinematic feature reveals, pricing/changelog | Next.js + Tailwind + Framer Motion + MDX |
| [`neo-brutalist`](skills/styles/neo-brutalist/SKILL.md) | Committed raw statement: hard borders/shadows, loud type, snappy mechanics | Astro / vanilla + plain CSS |
| [`personal-portfolio`](skills/styles/personal-portfolio/SKILL.md) | Individual folio, "quiet craft" or "playful signature" pole | Astro/Vite (+ Three.js for playful) |

### Support

| Skill | What it does |
|---|---|
| [`design-taste`](skills/design-taste/SKILL.md) | The judgment layer: typography pairing logic, color-system craft, spacing/hierarchy, "expensive look" heuristics, canonical taste failures — the art director in file form |
| [`ui-patterns`](skills/ui-patterns/SKILL.md) | Award-grade component specs: navigation, buttons, forms, cards, modals/drawers, accordions, footers, tables, toasts |
| [`competitive-research`](skills/competitive-research/SKILL.md) | Pre-design research pass: award/trend sweep + competitor teardowns → RESEARCH.md with a differentiation strategy that feeds DIRECTION.md; includes a recurring trend-watch mode |
| [`rapid-site-sprint`](skills/rapid-site-sprint/SKILL.md) | The move-fast partner: ship an excellent v1 in one session via decision defaults, parallel Codex-assets + Sonnet-build tracks, strict timeboxes, and a fixed quality floor |
| [`site-copywriter`](skills/site-copywriter/SKILL.md) | Voice sheet, copy deck, microcopy, meta/alt text — kills lorem ipsum for good |
| [`site-auditor`](skills/site-auditor/SKILL.md) | Scores any existing site 0–100 against the rubric with an evidence-backed, prioritized fix plan |
| [`launch-seo`](skills/launch-seo/SKILL.md) | SEO, share cards, analytics, deploy verification, Awwwards/FWA/CSSDA submission prep |

### Shared references (the research, distilled)

- [`site-builder/references/motion-recipes.md`](skills/site-builder/references/motion-recipes.md) — 14 copy-paste GSAP/Lenis/Three.js/CSS recipes (masked reveals, scrub pins, cursors, WebGL starter, kinetic gradients…)
- [`site-builder/references/quality-bar.md`](skills/site-builder/references/quality-bar.md) — the award rubric as concrete pass/fail checks + performance budgets
- [`site-builder/references/tech-stack-guide.md`](skills/site-builder/references/tech-stack-guide.md) — **which stack is optimal for which site**, and the standard toolkit
- [`site-builder/references/trend-report-2026.md`](skills/site-builder/references/trend-report-2026.md) — what's trending, what needs care, what reads as dated, and viral mechanics
- [`asset-creation/references/ai-image-tools.md`](skills/asset-creation/references/ai-image-tools.md) — **which AI tool for which asset** (Midjourney/FLUX/Ideogram/Recraft/Meshy…) and how to prompt each
- [`asset-creation/references/code-assets.md`](skills/asset-creation/references/code-assets.md) — grain, meshes, wordmarks, icons, favicons, OG generator, placeholder + compression scripts
- [`asset-creation/references/asset-manifest-template.md`](skills/asset-creation/references/asset-manifest-template.md) — the manifest contract between the two core skills

## Which AI tool generates the assets? (quick answer)

| Asset | Tool |
|---|---|
| Hero/editorial photography | **Midjourney** (best polish) |
| Exact compositions, product mockups | **FLUX** (best prompt adherence) |
| Images containing text | **Ideogram** (only reliable text renderer) |
| Icons, illustrations, vectors | **Recraft** (real SVG output) — or code them |
| Quick edits/iterations | **GPT-image** |
| 3D models for Three.js | **Meshy / Tripo** (glTF) |

Full matrix, per-tool prompt syntax, and the consistency workflow (anchor image → style-ref →
batch) in [`ai-image-tools.md`](skills/asset-creation/references/ai-image-tools.md).

## Prompting Codex to deliver the assets (copy-paste)

```text
Read skills/asset-creation/SKILL.md and follow it exactly, including its references.
Project: <one-line description or "see BRIEF.md">.
Style: skills/styles/<style-name>/SKILL.md.
Site code (if any): <path>.
Ask me your interview questions first in one batch; then generate all code assets,
write assets/manifest.md with prompt specs, and create placeholders at every path.
```

Autonomous variant: append `Do not wait for my answers — use todo-describe slots and finish.`

And to build the site (Sonnet 5 / Codex 5.5):

```text
Read skills/site-builder/SKILL.md and follow its 10 phases in order, including its
references and the style skill I name. Brief: <description>.
Style: skills/styles/<style-name>/SKILL.md. Asset manifest: assets/manifest.md
(create the stub per the template if missing). Do not stop until Phase 10's
self-score passes; write NOTES.md with anything awaiting me.
```

## Using with Claude Code

```bash
mkdir -p .claude/skills
cp -r skills/site-builder skills/asset-creation skills/site-copywriter \
      skills/site-auditor skills/launch-seo .claude/skills/
cp -r skills/styles/* .claude/skills/
```

Then: *"Use the site-builder skill to build a site for &lt;brand&gt; in the viral-trending style."*

## Using with Codex

`AGENTS.md` at the repo root routes Codex to the right skill — clone this repo into (or next
to) your project and say *"Follow AGENTS.md — build the site / create the assets."* All skills
are plain Markdown; any capable agent can follow them.

## Research grounding

Patterns distilled from award winners, jury criteria, and current trend/tool research:

- Awwwards [evaluation system](https://www.awwwards.com/about-evaluation/) — Design 40 / Usability 30 / Creativity 20 / Content 10, 18+ jurors, outlier scores dropped
- SOTY 2025: *The Messenger* (WebGL miniature world) and *Lando Norris* by OFF+BRAND (WebGL + Rive with an aggressive performance budget)
- Winner collections: [WebGL](https://www.awwwards.com/awwwards/collections/webgl/), [e-commerce](https://www.awwwards.com/websites/e-commerce/), [luxury](https://www.awwwards.com/websites/luxury/), [typography](https://www.awwwards.com/websites/typography/), [GSAP sites](https://www.awwwards.com/websites/gsap/); recent e-commerce honorees (Pixel Vault, Gielly Green, Belle Oaks, Weekend Max Mara, Bécane Paris)
- Studio bodies of work: Obys (type-first), Immersive Garden (kinetic type; Agency of the Year 2025), Lusion, Active Theory, Bruno Simon (playful 3D)
- 2026 trend reality-checks: bento grids and dark-mode-first held up; controlled glassmorphism (nav/modals only); kinetic gradients over static; unbudgeted 3D and scroll-jacking are documented score-killers
- Viral skill-ecosystem lessons (Anthropic's frontend-design skill and top community skills): commit to a written aesthetic direction **before** code; ban overused fonts; match design system to industry
- 2026 asset-tool comparisons: Midjourney (photographic polish), FLUX (prompt adherence), Ideogram (text rendering ~80%+), Recraft (true SVG output)
