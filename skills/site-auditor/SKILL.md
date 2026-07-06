---
name: site-auditor
description: Audit an existing website against the award-jury quality bar (Design 40 / Usability 30 / Creativity 20 / Content 10) and produce a scored report with a prioritized fix plan. Use when asked to review, audit, score, critique, or "make this site award-worthy" — for sites built with these skills or any existing site/codebase.
---

# Site Auditor

You evaluate a real site the way an award jury and a performance engineer would — then turn
every finding into a concrete, ordered fix list that the site-builder skill (or any developer)
can execute. Be honest: an inflated score wastes everyone's time. Findings without evidence
don't count.

## Inputs

A running site (URL or local dev server) and, when available, its codebase. If you have a
browser tool (Playwright is available in most environments), USE it: screenshot at 360 / 768 /
1440 / 1920px, capture console errors, measure timings. If code-only, say so in the report and
mark unverifiable checks.

## Workflow

### 1. Establish intent

Read `DIRECTION.md`/`BRIEF.md` if present; otherwise infer: what is this site trying to be,
who for, and which style genre is it closest to (check `skills/styles/` — the matching style
skill's Do/Don't list and mini-QA become additional audit criteria).

### 2. Score against the quality bar

Run every check in `../site-builder/references/quality-bar.md`, category by category. For
each: **pass / fail / unverifiable + one line of evidence** (screenshot ref, measured value,
file:line). Compute category percentages honestly.

Measurements to actually take, not estimate:
- Lighthouse (or equivalent): LCP, CLS, INP, total JS transferred, image weights
- Scroll a full page with the performance panel: longest frame, dropped-frame clusters
- Keyboard-only pass: tab through the entire primary flow, note every trap or invisible focus
- `prefers-reduced-motion` pass: force it, screenshot what breaks
- Font waterfall: families × weights loaded, FOUT/FOIT on first paint
- Grep code for: images without dimensions, missing alt, `console.log`, dead links, lorem ipsum

### 3. The taste pass (what audits usually miss)

Beyond the checklist — judge like a juror:
- **Screenshot test**: hero at 1440px next to 2–3 current Awwwards SOTD screenshots (describe
  the comparison if you can't fetch them). Template-like? Say so and say why (font choice?
  spacing? stock imagery? default component shapes?).
- **Coherence**: count fonts, accent colors, easing styles, radius values, shadow styles in
  actual use. More than the token set = drift; list every stray.
- **The one memorable thing**: name it. If you can't name it, that IS the top finding.
- **Trend check** against `../site-builder/references/trend-report-2026.md`: anything on the
  "dated" list gets flagged; anything trendy-but-half-committed too.
- **Copy read-aloud**: read the hero + one section; flag template phrases ("seamless",
  "elevate", "welcome to").

### 4. Report → `AUDIT.md`

```md
# Audit — <site> — <date>
## Verdict (3 sentences: what it is, what it's closest to achieving, the one thing holding it back)
## Scores
| Category | Score | Weighted |
|---|---|---|
| Design | x/… (x%) | ×0.40 |
| Usability | … | ×0.30 |
| Creativity | … | ×0.20 |
| Content | … | ×0.10 |
| **Total** | | **x%** |
## Findings (every failed check: evidence → why it matters → the fix, one line each)
## Fix plan (ordered)
1. <P0: broken/measured failures — hours>
2. <P1: coherence & craft — a day>
3. <P2: the creative gap — the redesign-level item, scoped as small as honesty allows>
## Quick wins (≤ 1 hour total, do today)
```

Order the fix plan by **weighted impact ÷ effort** — a CLS fix (Usability ×0.30) usually
beats a nice-to-have animation. The "creative gap" item must be specific ("the hero needs
one signature interaction — e.g. X") — "be more creative" is not a finding.

### 5. Offer the follow-through

End by offering: "Want me to execute the fix plan?" — P0/P1 items are direct edits;
P2 creative items route through site-builder Phase 1 (a new DIRECTION.md decision) so the
fix is a committed direction, not a patch.

## Rules

- Every finding cites evidence. No vibes-only failures — and no vibes-only passes.
- Audit the site that exists, not the site you'd have built. Respect its chosen style; score
  execution of THAT style (a brutalist site doesn't fail for hard shadows).
- If the site is genuinely strong, say so specifically — a short list of real strengths
  teaches as much as the fix list.
