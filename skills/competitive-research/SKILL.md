---
name: competitive-research
description: Research pass before designing — analyze award winners, trending sites, and the user's direct competitors to produce RESEARCH.md, which feeds DIRECTION.md with pattern insights and a differentiation strategy. Use before site-builder Phase 1 for high-stakes projects, when asked to "research competitors/trends," or when the brief needs a point of view on the market.
---

# Competitive Research

You research the landscape a new site will live in, extract *patterns* (never designs to
copy), and hand the site-builder a differentiation strategy. Output is one file:
`RESEARCH.md`. Timebox: this is a 30–60 minute pass, not a thesis — its only job is to make
DIRECTION.md sharper.

## Ethics line (hard rule)

Research extracts **techniques, structures, and market gaps** — layout archetypes, motion
grammar, content strategy, positioning language. It never extracts copy, logos, palettes to
reuse, or "rebuild this site." If the user asks to clone a specific site, redirect: identify
what they love about it (usually 2–3 patterns), then design original work using those
patterns via the style skills.

## Workflow

### 1. Frame (5 min)

From BRIEF.md: the industry, the audience, and 3–5 direct competitors (ask the user for
their list; supplement via search). Decide the research question — always some form of:
*"What does everyone in this space do, and where is the taste gap we can own?"*

### 2. Award & trend sweep (15 min)

Web-search the current state (do NOT rely on memory — this landscape moves quarterly):
- `awwwards <industry> site of the day <current year>` and the relevant Awwwards
  collections (e-commerce, typography, WebGL, portfolios…)
- `godly.website`, `land-book`, `siteinspire`, `dark.design`, `minimal.gallery` mentions
  for the genre
- `<industry> website design trends <current year>`
- Cross-check against `../site-builder/references/trend-report-2026.md`; note anything the
  live landscape shows that the trend report doesn't (and flag the report for update if so).

For each notable site found (aim 5–8), record: what genre archetype it is, its ONE memorable
thing, its stack tells (WebGL? scroll library? framework — check page source when fetchable),
and what it does badly (there's always something — usually performance or mobile).

### 3. Competitor teardown (20 min)

For each direct competitor (fetch their sites; screenshot if a browser tool is available):

```md
### <Competitor>
- Archetype: <closest skills/styles/* genre + how committed they are to it>
- First-fold message: <what they claim in 5 seconds>
- Type/color fingerprint: <e.g. "overused-font sans, blue accent, template feel" — 1 line>
- Signature (if any): <their one memorable thing, or "none — template">
- Weaknesses: <slow LCP / stock imagery / no mobile care / dated trends from the ban list>
- What they'd never dare: <the move that would instantly differentiate from them>
```

The last line is the gold — collect these across all competitors.

### 4. Pattern synthesis

Three lists:
- **Table stakes**: patterns EVERY credible player has (users expect these; include them,
  spend no creativity here — e.g. sticky nav, pricing table norms for the industry).
- **Differentiators observed**: patterns only the best sites have (candidates for us,
  raise-or-match).
- **The white space**: what NOBODY in this industry does that an adjacent genre does well
  (e.g. "no ceramics studio uses editorial-studio index lists; they all use shop grids").
  White space + brand fit = the "one creative risk" for DIRECTION.md.

### 5. Deliver `RESEARCH.md`

```md
# Research — <project> — <date>
## The landscape in 3 sentences
## Award/trend findings (5–8 sites: archetype · memorable thing · weakness)
## Competitor teardowns (per template above)
## Patterns
- Table stakes: …
- Differentiators worth matching: …
- White space: …
## Recommendation
- Style skill: skills/styles/<name> because <fit reason>
- The one creative risk: <specific, from white space>
- Positioning line the copy should own: <what competitors can't say>
- Avoid: <trends/patterns the landscape has burned out — with which competitor burned them>
## Sources
<links>
```

The Recommendation block maps 1:1 onto DIRECTION.md inputs — that's the handoff.

## Standing variant: trend-watch

When asked to "keep us current" (recurring runs): re-run step 2 only, diff against the
previous RESEARCH.md and trend-report-2026.md, and report only *changes* — new patterns
gaining steam, trends newly reading as dated, notable new winners in the genre. Propose
edits to trend-report-2026.md so the whole library stays fresh — that file is the single
place trend knowledge lives.
