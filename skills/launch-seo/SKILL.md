---
name: launch-seo
description: Take a finished site from "done" to "launched" — technical SEO, share cards, analytics, sitemaps, redirects, deploy verification, and award-submission prep. Use as the final step after site-builder Phase 10, or standalone when asked to launch, deploy, SEO-optimize, or submit a site for awards.
---

# Launch & SEO

The site passed the quality bar; now make sure the world (and the crawlers, and the juries)
receive it correctly. This skill is a checklist-driven pass — work top to bottom, verify each
item with a real request/screenshot, and finish with `LAUNCH.md` recording what shipped.

## 1. Technical SEO pass

- Unique `<title>` + meta description per page (copy from COPY.md's meta section — if absent,
  run the site-copywriter skill's meta pass first).
- Canonical URLs; one `<h1>` per page; heading outline reads as an argument.
- `sitemap.xml` + `robots.txt` (framework plugins: `@astrojs/sitemap`, Next `sitemap.ts`).
- Structured data where honest: `Organization`/`Person`, `Product` + price on PDPs,
  `Article` + author/date on editorial pages, `BreadcrumbList` on deep sites. Validate with a
  schema validator; no invented ratings/reviews.
- Clean URLs (no `/index.html`, consistent trailing-slash policy), 301s from any legacy URLs
  (collect from the user or old sitemap), custom 404 verified to return HTTP 404.
- Images: descriptive filenames (`ceramic-studio-workbench.avif`, not `img_012.avif`) — align
  with asset-manifest paths at generation time when possible; alt text everywhere (audit
  against the manifest).
- Performance IS SEO: re-run the quality-bar budgets on the **production** build/host —
  numbers differ from dev.

## 2. Share layer (the launch's front door)

- OG + Twitter card meta on every page; per-page dynamic OG images where the style skill
  provides a template (verify with actual card-validator tools or a manual fetch of the
  rendered image URL).
- Favicon set + `manifest.webmanifest` (name, theme color matching tokens).
- `theme-color` meta (both color schemes).
- Test the actual share: paste the URL into a validator/preview for X, Slack, iMessage
  formats (1200×630 renders cropped in some — keep critical content in the center 1000×524).

## 3. Analytics & feedback (lightweight, honest)

- Plausible/Fathom snippet (or the user's choice) — verify it doesn't ding the perf budget;
  no consent banner needed for cookieless analytics in most jurisdictions (flag if the user
  adds cookie-based tools — then a real consent flow is required).
- Track the 2–4 events that matter (primary CTA, form submit, outbound clicks) — not
  everything.
- 404 logging (Plausible custom event or host analytics) to catch broken inbound links in
  week one.

## 4. Deploy & verify

- Production deploy (Vercel/Netlify/Cloudflare per tech-stack-guide); custom domain + HTTPS;
  www→apex (or reverse) redirect chosen and enforced.
- Security headers: CSP (at least a report-only starter), `X-Content-Type-Options`,
  `Referrer-Policy`, `Permissions-Policy`. Frameworks/hosts have presets — enable them.
- Verify ON PRODUCTION: all quality-bar budgets, forms actually deliver (send a test
  submission), every external link 200s, no mixed content, no console errors.
- Cache headers: immutable hashed assets, sensible HTML revalidation.
- Post-launch: submit sitemap to Google Search Console + Bing Webmaster (user accounts
  required — provide exact instructions if you can't access them).

## 5. Award submission prep (when the user wants to submit)

- **Awwwards**: submission is paid; site must be live and stable. Prepare: title, 350-char
  description emphasizing the creative idea + tech, categories/tags, and a 1600×1200
  thumbnail — design the thumbnail like the OG card (juries browse a grid; the thumbnail is
  the first vote).
- **FWA / CSSDA**: similar kits, different crops — generate from the same template.
- Timing: submit early in the week; ensure no deploys during jury window; freeze a
  `submitted` git tag.
- Write the "making of" notes (idea, stack, one technical challenge) — often requested, and
  writing it exposes any story gaps before judges find them.

## 6. `LAUNCH.md`

Record: production URL, deploy target + config, DNS notes, analytics property, events
tracked, redirects list, submission assets location, remaining `awaiting-user` manifest
items, and a "first 48 hours" watchlist (analytics live? 404 log? form deliveries? card
renders on X/LinkedIn/Slack?).

## Don'ts

- No keyword-stuffed footers, hidden text, or schema for content that doesn't exist —
  penalties outlast launches.
- No tag-manager kitchen sinks; every third-party script re-justifies the perf budget.
- Don't launch with placeholder assets still visible above the fold — check the manifest
  status summary; below-fold placeholders need a conscious user sign-off.
