# Trend report — 2026

What's currently winning attention, what's held up, and what already reads as dated. Use trends
**deliberately**: a trend is a seasoning on a strong style-skill system, never the system itself.
Re-verify this file with fresh research if more than ~6 months old.

## Holding up — safe to build on

| Trend | How to use it well | Recipe |
|---|---|---|
| **Bento grids** | Information-dense sections (features, portfolio index, stats). Vary cell sizes with intention; every cell earns its size. Add one "live" cell (animated number, mini-demo, video loop) | CSS grid + `grid-template-areas`; hover: subtle lift + border glow |
| **Dark mode as first-class** | Commit fully — design dark *first* if the brand suits it; never auto-invert | Tokens per scheme; `color-scheme: dark light` |
| **Scroll storytelling** | The gold standard for launches/products: break the story into scroll-paced sequences | motion-recipes §3, §10 |
| **Kinetic/animated gradients** | Liquid, slowly-drifting color fields replace static gradients; always add grain to kill banding | motion-recipes §11 + grain from code-assets |
| **Big, characterful type** | Display serif or expressive grotesque at massive clamp() sizes remains the cheapest "expensive look" | style skills' type systems |
| **Glassmorphism (controlled)** | Nav bars and modals ONLY, communicating layer hierarchy — not decorating cards | `backdrop-filter: blur(12px)` + 1px inner border + low-opacity fill |
| **Grain/noise texture** | The universal "not a template" signal; overlay at 3–6% opacity | code-assets SVG turbulence |
| **Custom cursors (augmenting)** | Dot/label that *follows* the OS cursor and reacts to targets — never replaces it | motion-recipes §7 |
| **View-transition page morphs** | Elements that persist and morph across navigations feel native-app quality | motion-recipes §9 |

## Use with care — reality-check applies

| Trend | The catch |
|---|---|
| **3D / WebGL everywhere** | 2026's documented lesson: unbudgeted 3D drains performance and loses the Usability 30%. One budgeted WebGL moment (DPR clamp, lazy init, poster fallback) beats five |
| **Kinetic typography** | Scroll-scrubbed letter morphing is spectacle; juries now call it "polish over substance." Use for ONE headline moment, keep body text still |
| **Neo-brutalism** | Powerful as a committed identity (see the neo-brutalist style skill); half-applied it just looks unfinished |
| **AI-generated imagery** | Fine when art-directed consistently (one style block across the manifest); instantly recognizable and cheap-looking when mixed styles slip in |
| **Preloaders** | Only if load actually needs masking; ≤ 2.5s, skip on repeat visits |
| **Scroll-jacking** | Pinned scrub sections are fine; hijacking wheel speed/direction is a usability score killer |

## Reads as dated in 2026 — avoid

- Static hero gradient + centered headline + two buttons (the 2023 SaaS template)
- Parallax on everything; tilt-on-hover cards everywhere
- Fake glassmorphism cards on light backgrounds with no layer logic
- Lottie confetti explosions and floating blob SVGs as decoration
- Overused fonts (Inter/Roboto/Poppins/Montserrat/Space Grotesk as brand face)
- Dark-purple-to-blue "AI gradient" with sparkle emojis and orbit lines
- Cookie-cutter testimonial carousels; auto-playing background video with no poster/fallback

## Viral mechanics (what makes sites get shared)

Sites go viral for **one screenshot-able or clip-able moment**: an interaction people record
(Bruno Simon's drivable car), a hero that looks impossible (The Messenger's pocket planet), a
tool/toy embedded in the page, or extreme type/color commitment. Design that moment deliberately:
it must read in a 3-second clip with no sound and survive a Twitter/X compression. The OG image
is part of the design — make the share card itself beautiful (asset manifest includes it).
