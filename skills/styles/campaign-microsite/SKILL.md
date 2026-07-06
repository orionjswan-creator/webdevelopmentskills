---
name: campaign-microsite-style
description: FWA-territory experiential microsite style — product drops, launches, film/album/event promos, brand campaigns. One interactive signature moment built around a short-lived, high-intensity page designed to be experienced once and shared widely. Use via the site-builder skill for campaigns, drops, promos, teasers, and experiential one-offs.
---

# Style: Campaign Microsite

The FWA's home genre and the luxury-campaign register of recent SOTD winners (the "Gucci:
Mystery Unfolds" tier — see the award casebook): a page that exists for weeks, not years,
and exists to make people *feel* something and share it. The feeling to create:
**"you have to see this."** Everything the casebook says about winners applies double here:
one signature moment, fast on mid-range devices, and play that gets screen-recorded.

## Stack (this skill's choice)

**Vite + TypeScript + Three.js + GSAP.** A microsite is a single experience — no framework
routing, no CMS; the whole budget goes to the moment. Audio via Howler/WebAudio (opt-in).
If the campaign needs a data layer (drop countdown, RSVP, generative results), a single
serverless endpoint.

## The structure: an experience, not a page

Microsites are choreographed like a title sequence — design in **acts**:

1. **Arrival (0–5s)** — instant visual promise: the world/product/mystery is already
   moving. Preloader only if genuinely needed (≤ 2s, in-fiction: styled as part of the
   story, not a percentage bar). Campaign name + one line + a single instruction
   ("Scroll" / "Hold to reveal" / "Press play").
2. **The experience (the signature moment)** — choose ONE mechanic and build the whole act
   around it:
   - **Scroll-scrubbed sequence** — a product assembling, a story unfolding chapter by
     chapter (GSAP timeline, §3 at full ambition — this genre earns multi-pin).
   - **Held interaction** — press-and-hold reveals, drag-to-uncover, WebGL material that
     responds to touch (the "Mystery Unfolds" register: sequenced reveals + chapters).
   - **A toy** — throwable/drivable/playable object (§12 + physics: Rapier); score or
     outcome optional but shareable outcomes multiply reach.
   - **Generative personal result** — answer 3 questions / move a slider → a unique
     visual output the visitor can download/share (result card = designed asset).
3. **The payoff** — the single CTA the campaign exists for: pre-order, RSVP, trailer,
   playlist, store locator. One action. Oversized. Impossible to miss.
4. **The echo** — share affordances (download the result, copy link with personalized OG),
   credits (agency-style: client, team, tools — juries and peers read these), and a quiet
   link to the main brand site.

## Design tokens

- **Palette**: campaign-specific and *more extreme* than the parent brand — one dominant
  atmosphere color + one flare accent. Microsites may break the brand system deliberately;
  document the license taken in DIRECTION.md.
- **Type**: one display face with real presence (Clash Display, Zodiak heavy, Unbounded,
  or the campaign's licensed face) + mono for instructions/meta. Type is often IN the
  scene (3D extruded, shader-distorted, masked by the visual) rather than over it.
- **Motion**: this genre's ceiling is highest — longer cinematic durations (1.2–1.8s),
  full easing curves, sound-synced accents. But the 60fps floor is absolute: DPR clamp,
  draw-call budget, test on a mid-range phone FIRST, not last.

## Signature moves

| Move | Recipe |
|---|---|
| Multi-act scroll timeline | chained pinned ScrollTriggers, §3 |
| WebGL scene with interactive material | §12 + pointer uniforms |
| In-fiction preloader | act-1 styling, real asset progress |
| Opt-in sound design | muted-by-default toggle, WebAudio; UI ticks + one theme layer |
| Personalized OG/share card | serverless render of the visitor's result |
| Countdown (drops) | tabular-nums, timezone-correct, no fake urgency |
| Chapter navigation | dots/progress rail so the experience is seekable (usability inside spectacle) |

## Asset slots

| id | dimensions | role |
|---|---|---|
| scene-model | glTF ≤ 5MB total | the hero object/world (Meshy/Tripo spec or supplied) |
| textures/env | KTX2/HDR | scene materials + lighting |
| chapter-XX | 2400×1500 | non-3D chapter visuals |
| result-template | 1080×1920 + 1200×630 | shareable result (story + card crops) |
| audio-theme / ui-ticks | mp3/webm | opt-in sound |
| og-campaign | 1200×630 | the share card — designed as hard as the hero |

## The campaign clock (this genre's special constraints)

- **Deadline is absolute** (drop date, premiere) — scope acts to cut cleanly: act 2 can
  lose depth, acts 1/3 cannot lose polish. Build payoff CTA first, then arrival, then
  deepen the middle.
- **Traffic is a spike** — static hosting + CDN; the serverless endpoint is the only
  scaling risk; load-test it.
- **Life after the campaign**: plan the sunset — redirect to the brand site, or freeze as
  an archived piece (awards juries visit late; keep it live through judging windows).
- **Measure the share loop** — outbound share events + inbound `?via=` params; the echo
  act is instrumented, not decorative.

## Do / Don't

- DO storyboard the acts (even as text) before building — this genre is directed, not
  assembled.
- DO give the visitor agency within 5 seconds — watching-only openings lose the record-
  and-share behavior.
- DO keep a "skip to the point" path (chapter rail / skip button) — press, buyers, and
  reduced-motion users all need it; it's also the a11y fallback.
- DON'T ship without a phone-first test — campaign traffic is 70%+ mobile from social.
- DON'T fake the countdown or the scarcity; don't gate the payoff behind data collection
  the campaign doesn't need.
- DON'T let total payload exceed ~8MB for the full experience (progressively loaded);
  arrival act ≤ 1.5MB.

## Mini-QA

- Mid-range phone: 60fps through all acts, thermals sane after 2 minutes
- The signature moment survives a muted 3-second screen recording (viral-trending's test —
  this genre lives by it)
- Keyboard + reduced-motion path reaches the payoff CTA with full content
- Share card personalized/rendered correctly; sunset plan written in NOTES.md
- Credits complete — client, agency, team, tools (award submission needs them)
