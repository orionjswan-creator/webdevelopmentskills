---
name: ux-architecture
description: Information architecture and UX strategy before visual design — sitemap, user journeys, page-level content hierarchies (text wireframes), navigation model, and conversion strategy. Produces ARCHITECTURE.md, which site-builder consumes at Phase 0/4. Use after discovery on multi-page projects, or whenever a site's structure (not its look) is the open question.
---

# UX Architecture

Visual design answers "how does it look"; this skill answers **"what exists, in what order,
and why."** On a one-pager the style skill's blueprint is enough — but a premium multi-page
engagement lives or dies on structure: the wrong sitemap makes every later phase decorate a
broken skeleton. Output is one file: `ARCHITECTURE.md`.

## Inputs

`DISCOVERY.md` + `BRIEF.md` (goals, audiences, success metric) and `RESEARCH.md` if it
exists (table-stakes patterns per industry). No visual decisions here — that's DIRECTION.md's
job, later.

## Workflow

### 1. Journey mapping (start from people, not pages)

For each audience profile (2–3 from discovery), write the primary journey as a narrative:

```md
### Journey: <audience> — <goal>
Arrives from: <search / social / referral / press> with <question in their head>
Needs to believe: <the 2–3 things that convert this person, from discovery quotes>
Path: <entry page> → <what convinces> → <the action> (steps: N)
Failure risks: <what makes them leave — unanswered question, buried price, slow page>
```

The union of journeys defines the pages; anything no journey touches gets cut (the classic
premium-site bloat: pages that exist because a stakeholder wanted them, not because a
visitor needs them — flag these explicitly and let the client decide with eyes open).

### 2. Sitemap

- Every page: name, URL slug, journey(s) served, primary action, priority (P1 = built as
  designed template; P2 = uses an existing template; P3 = future/cut).
- Depth rule: any P1 content within 2 clicks of home; total top-nav items 3–5 (research
  shows premium sites trend shallow-and-curated, not deep-and-complete).
- Template inventory: the distinct page *designs* the SOW promised — sitemap pages map
  many-to-one onto templates; this mapping IS the scope control.

### 3. Navigation model

- Top nav (3–5 items + 1 CTA), footer taxonomy (fuller), and contextual nav (in-page
  next-steps at the end of every page — the "where do I go now" answer; dead-end pages are
  conversion leaks).
- Naming: visitor vocabulary, not org-chart vocabulary ("Menus" not "Culinary Offerings";
  discovery's misunderstanding answers tell you which words confuse).
- Decide the mobile model now (overlay vs. bar) — it constrains design later.

### 4. Page-level content hierarchy (text wireframes)

For every P1 template, the section stack in priority order — this is the artifact designers
and copywriters build from:

```md
## Template: <name>  (serves: <journeys>)
1. <Section> — job: <what it must accomplish> — content: <what goes here> — proof: <why believe it>
2. …
N. Next step: <contextual CTA>
```

Rules: one job per section; the primary action appears above the fold AND at the natural
decision point; objections (price, process, trust) answered *in order of intensity* from
discovery; every claim adjacent to its proof (metric, image, testimonial slot — feeds the
asset manifest).

### 5. Conversion strategy

- The ONE primary conversion per journey and its friction budget (form fields ≤ what the
  sales process truly needs; each extra field is a measured cost).
- Trust architecture: where proof lives on each template (social proof near CTAs, process
  transparency near price, guarantees near commitment).
- Measurement plan: the 3–5 events that map to discovery's success metric (feeds
  launch-seo's analytics step).

### 6. Content model sketch (feeds cms-integration)

List the structured content types the sitemap implies (Room, Dish, Project, Article,
Person…) with their fields — one line each. This becomes the CMS schema; writing it now
prevents the "the CMS can't express our design" collision later.

## `ARCHITECTURE.md` structure

Journeys → Sitemap table → Navigation model → Template wireframes → Conversion strategy →
Content model → Open questions for the client (each with your recommendation).

## Rules

- No visual language in this file — if you're describing colors or motion, you've drifted
  into DIRECTION.md's territory.
- Every section of every template must name its job; "About Us — content about us" is a
  failure state.
- Cut-list candor: present the pages you removed and why — clients buy structure work when
  they can see the reasoning, and it's the deliverable that most visibly separates an
  agency from a template vendor.
- Validate against RESEARCH.md's table stakes: missing an industry-expected page (menus,
  rates, floor plans, docs) is an architecture bug, not a content gap.
