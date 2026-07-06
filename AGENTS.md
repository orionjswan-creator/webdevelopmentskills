# Agent routing — award-winning website skills

You are working in (or alongside) a skill library for building websites at the quality level of
Awwwards/FWA/CSSDA winners. Route the task to the right skill and follow that skill **fully**
before writing code.

## Task routing

| The user asks you to… | Read and follow |
|---|---|
| Build / scaffold / redesign a website | `skills/site-builder/SKILL.md` |
| Create, spec, or plan assets (images, logos, textures, icons, 3D) | `skills/asset-creation/SKILL.md` |
| Write or improve website copy / headlines / microcopy | `skills/site-copywriter/SKILL.md` |
| Review, audit, score, or "make this site award-worthy" | `skills/site-auditor/SKILL.md` |
| Launch, deploy, SEO, share cards, award submission | `skills/launch-seo/SKILL.md` |
| "Make it look better/premium" — aesthetic judgment calls | `skills/design-taste/SKILL.md` |
| Build or polish a specific component (nav, form, modal, card…) | `skills/ui-patterns/SKILL.md` |
| Research competitors / trends before designing | `skills/competitive-research/SKILL.md` |
| Ship a site fast ("today", "ASAP", "quick MVP/landing page") | `skills/rapid-site-sprint/SKILL.md` |
| Scope, quote, or propose a client engagement; run discovery | `skills/client-discovery/SKILL.md` |
| Plan sitemap / IA / user journeys / wireframes | `skills/ux-architecture/SKILL.md` |
| Create a logo / identity system / brand guidelines | `skills/brand-identity/SKILL.md` |
| Present work to a client, process feedback, hand off a project | `skills/client-delivery/SKILL.md` |
| Formal WCAG audit / accessibility statement / compliance | `skills/accessibility-compliance/SKILL.md` |
| Add a CMS / make the site client-editable | `skills/cms-integration/SKILL.md` |
| An award-winning agency / studio / portfolio experience | `skills/styles/immersive-agency/SKILL.md` (via site-builder) |
| A luxury brand / e-commerce / shop experience | `skills/styles/ecommerce-brand/SKILL.md` (via site-builder) |
| A magazine / editorial / creative-studio site | `skills/styles/editorial-studio/SKILL.md` (via site-builder) |
| A launch page / waitlist / trending "viral" look | `skills/styles/viral-trending/SKILL.md` (via site-builder) |
| A SaaS / developer-tool / B2B product site | `skills/styles/saas-product/SKILL.md` (via site-builder) |
| A loud, raw, neo-brutalist statement site | `skills/styles/neo-brutalist/SKILL.md` (via site-builder) |
| A personal portfolio / CV site | `skills/styles/personal-portfolio/SKILL.md` (via site-builder) |
| A hotel / restaurant / venue / real-estate site | `skills/styles/hospitality-place/SKILL.md` (via site-builder) |
| A campaign / drop / promo / experiential microsite | `skills/styles/campaign-microsite/SKILL.md` (via site-builder) |
| VJ / concert / DJ-screen visuals, generative event art, interactive installations | `skills/live-visuals/SKILL.md` (standalone — not via site-builder) |

If no style is specified, ask the user to pick one (list the nine with one-line descriptions),
or infer from the brief and state your choice before building.

## Hard rules (apply to every task in this library)

1. **Patterns, not clones.** Reproduce techniques and quality, never a specific site's content,
   copy, logo, brand colors, or imagery. All output must be original to the user's brand.
2. **Read the chosen style skill top to bottom before writing any code.** The style skill decides
   the tech stack — respect its choice.
3. **Every image slot must reference an asset-manifest ID** (`assets/manifest.md`). If the
   manifest doesn't exist yet, run the asset-creation skill's manifest step first. Never ship an
   `<img>` without a manifest entry or a labeled placeholder.
4. **Never block on missing assets.** Generate labeled SVG placeholders and keep building.
5. **Motion must respect `prefers-reduced-motion`** and hold 60fps — see
   `skills/site-builder/references/motion-recipes.md`.
6. **Before declaring done**, self-score against
   `skills/site-builder/references/quality-bar.md` and fix anything below the bar.
