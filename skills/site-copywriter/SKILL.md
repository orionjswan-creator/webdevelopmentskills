---
name: site-copywriter
description: Write and polish all website copy to award standard — headlines, section copy, microcopy, CTAs, error states, 404s, meta descriptions, alt text. Use during site-builder Phase 4, or standalone when asked to write, rewrite, or improve website copy. Content is 10% of the award score but touches all four categories.
---

# Site Copywriter

Weak copy caps a site's ceiling: juries score Content directly (10%) and copy quality leaks
into Design (type is only as good as the words set in it), Usability (labels, errors), and
Creativity (voice). Your job: every word on the site sounds like ONE confident person who
knows exactly who they're talking to.

## Inputs

`BRIEF.md` + `DIRECTION.md` (the 3 mood adjectives are your voice spec) + the chosen style
skill (each genre has a register — agency copy is declarative, luxury copy is quiet, viral
copy is quotable, brutalist copy is blunt, portfolio copy is first-person).

## Workflow

### 1. Voice sheet (write this before any copy)

```md
# VOICE.md
- We sound like: <one vivid comparison — "a calm senior engineer", "a gallery curator">
- 3 adjectives (from DIRECTION.md): 
- We say / we never say: <5 word-pairs, e.g. "use" not "utilize", "people" not "users">
- Sentence rhythm: <e.g. short declaratives, occasional long build>
- Person & tense: <"we/you", present>
- Capitalization: <sentence case everywhere is the modern default — decide once>
```

### 2. Copy deck — write ALL copy in one file (`COPY.md`) before it enters components

Structure it by page → section → slot, so builders drop it in mechanically. Rules per slot:

- **Headlines**: ≤ 8 words, concrete, no "Welcome to". Test: would someone quote it? For
  display-type styles, write headlines knowing they'll be set at 10vw — every word must earn
  massive scale. Write 3 candidates per key headline, mark the pick.
- **Sublines**: one job — de-risk or specify the headline. ≤ 2 lines at 60ch.
- **Section copy**: 40–80 words max per block on marketing pages. Cut every third sentence —
  it's usually the one restating the first.
- **CTAs**: verb-first, specific outcome ("Start a project", "See the collection",
  "Read the case") — never "Learn more"/"Submit"/"Click here". Primary CTA identical
  everywhere it repeats.
- **Manifesto/statement lines** (agency/editorial styles): these are the hardest words on
  the site. Write 10, keep 3. Concrete beats abstract ("We make slow brands fast" beats
  "We craft digital experiences").

### 3. Microcopy pass (where craft is judged)

- Form labels, placeholders (never use placeholder AS label), inline errors (say how to fix:
  "Email needs an @ — e.g. you@studio.com"), success states with personality.
- Empty states, loading states ("Curating…" beats a bare spinner), cart states, search-no-results.
- **404 page**: a personality showcase + useful links. Award sites treat 404 as a canvas.
- Buttons' in-progress/done morphs: "Add to cart → Adding… → Added ✓".
- Cookie/consent (if needed): human, brief, honest.

### 4. Meta & semantic pass

- `<title>` per page: `Primary phrase — Brand` ≤ 60 chars; meta description ≤ 155 chars
  written as an inviting sentence, not keyword soup.
- OG title/description tuned for the share card design (short enough to set large).
- **Alt text**: write like an editorial caption (what + why it matters), not "image of".
  Feed these back into the asset manifest entries.
- Headings hierarchy reads as an outline of the argument when extracted alone.

### 5. Read-aloud QA

Read the whole COPY.md aloud (or simulate): flag anything you stumble on, any sentence that
sounds like every other website ("seamless", "elevate", "unlock", "empower", "supercharge",
"delve", "innovative solutions" — ban list), any claim without proof. Every superlative
either gets evidence or gets cut.

## Genre registers (quick reference)

| Style skill | Register | Example CTA |
|---|---|---|
| immersive-agency | Declarative, third-person-plural confidence, short | "Start a project" |
| ecommerce-brand | Quiet, sensory, material-focused | "Discover the collection" |
| editorial-studio | Literary, precise, bylined | "Read the story" |
| viral-trending | Quotable, direct, slightly audacious | "Get early access" |
| saas-product | Verb-first, outcome-literal, zero fluff | "Start free" |
| neo-brutalist | Blunt, honest, funny-sincere | "BUY IT" |
| personal-portfolio | First person, opinionated, warm | "Email me" |

## Don'ts

- No lorem ipsum survives this skill. If facts are missing, write the best draft and mark
  `<!-- FACT-CHECK: -->` for the user.
- Never invent testimonials, client names, press quotes, or metrics — mark slots
  `awaiting-user` instead.
- Don't write copy that contradicts the design's confidence (huge type + hedging words
  = broken spell).
