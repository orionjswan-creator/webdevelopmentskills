# Tech stack guide — what's optimal for which site

Each style skill names its preferred stack; this file is the decision logic behind those picks
and the tie-breaker when a style offers options. The 2026 reality: award winners are built on
boring, fast foundations with the craft spent on design and motion — not on exotic frameworks.

## The decision matrix

| Site type | Optimal stack | Why |
|---|---|---|
| Immersive one-pager / agency site | **Vite + vanilla TS (or Astro) + GSAP + Lenis + Three.js** | No framework tax; full control of the render loop; fastest possible load for a site that's mostly custom motion |
| Multi-page marketing / SaaS product | **Next.js (App Router) + Tailwind + Framer Motion (+ GSAP for scroll scenes)** | Routing, image/font optimization built in, RSC keeps JS small, best Vercel deploy story |
| E-commerce | **Next.js + Tailwind + headless Shopify (Storefront API) or Shopify Hydrogen** | Cart/checkout solved; PDP/PLP as custom as you want; Medusa if avoiding Shopify |
| Editorial / magazine / blog-heavy | **Astro + Tailwind (+ GSAP islands)** | Content-first, zero-JS by default, MDX/content collections, best Core Web Vitals per effort |
| Portfolio (designer/dev) | **Astro or Vite vanilla** — Next.js only if it needs an app | Small surface, maximum craft per KB |
| Site needing a CMS | Add **Sanity** (structured, live preview) or **Payload** (self-hosted, TS-native); Keystatic for git-based simplicity | Match CMS to who edits: marketers → Sanity; devs → Keystatic |
| Interactive 3D experience / game-like | **Vite + Three.js** (vanilla) or **R3F (React Three Fiber) + drei** if React UI coexists | R3F only pays off when React state drives the scene |

## The standard toolkit (all styles)

- **Styling**: Tailwind v4 *or* vanilla CSS custom properties — pick per team preference; either
  way, tokens live in one file. Avoid CSS-in-JS runtimes (perf tax, no award winner needs them).
- **Motion**: GSAP + ScrollTrigger (scroll choreography), Lenis (smooth scroll), Framer Motion
  only inside React component UIs. Native CSS scroll-driven animations + View Transitions API as
  progressive enhancement.
- **3D/WebGL**: Three.js. Shader-only heroes can skip Three and use a raw WebGL quad. Rive for
  vector motion graphics (the Lando Norris SOTY site pairs WebGL + Rive). Spline only for
  prototypes — its runtime is heavy.
- **Fonts**: variable WOFF2, self-hosted, ≤ 2 families. Sources: Fontshare, Google Fonts (deep
  catalog, not the overused top-20), font foundry trials for mockups only (license before ship).
- **Images**: AVIF/WebP, `next/image` or Astro `<Image>`, `sharp` for pipelines.
- **Deploy**: Vercel (Next.js), Netlify or Cloudflare Pages (Astro/Vite). All fine — pick by
  what the user already has.
- **Analytics**: Plausible/Fathom (lightweight) — never let a tag manager eat the perf budget.

## Rules of thumb

1. **Static beats dynamic** until proven otherwise — most award sites are static output + client
   motion.
2. **The framework should disappear** in the shipped bundle: if the stack costs > 100KB before
   your own code, reconsider.
3. **One WebGL context per page.** Multiple canvases = multiple GL contexts = jank.
4. **TypeScript everywhere** — agents (and humans) make fewer errors with types.
5. If the user names an existing stack, adapt the style skill to it rather than fighting —
   these patterns are portable.
