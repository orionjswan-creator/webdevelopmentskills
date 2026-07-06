---
name: client-delivery
description: Run the client-facing side of a premium engagement — presenting design work with rationale, managing structured feedback rounds, staging and walkthroughs, change-request discipline, and the final handoff package with training. Use when presenting concepts or builds to a client, processing client feedback, or closing out an engagement.
---

# Client Delivery

Agencies don't lose premium clients on design quality — they lose them on *process feel*:
work appearing without rationale, feedback spiraling, handoffs that leave the client
stranded. This skill is the delivery discipline that makes the same design work feel worth
agency pricing.

## Presenting work (concepts, directions, builds)

**Never send a bare link.** Every presentation is: context → rationale → the work → guided
questions.

Structure (write it as `PRESENTATION-<phase>.md` or the walkthrough script):

1. **Re-anchor** (3 sentences): the goal from DISCOVERY.md, the success metric, what phase
   this is and what's being decided today.
2. **Rationale before reveal**: the 2–3 decisions that shaped the work, each traced to a
   discovery fact or research finding ("You said prospects don't realize you handle X —
   that's why the hero leads with it"). Rationale traced to *their own words* is the
   single most effective approval tool.
3. **The work, in context**: staged link plus curated screenshots/recording of the key
   moments (hero at desktop + phone, one signature interaction, one deep page). For
   direction-stage work: shown in realistic context (see brand-identity's rule), 1–2
   directions max — three-plus options signals you don't have a point of view.
4. **Guided response**: ask decision questions, not "thoughts?" — "Does this feel like the
   5 adjectives we agreed?" / "Is anything here untrue to how you sell?" Frame feedback at
   the right altitude: direction feedback at direction stage, copy details at copy stage.
5. **Next gate**: what happens on approval, what today's decision unlocks, the date.

**Walkthrough recordings**: 3–6 minute screen recording with narration beats a meeting for
distributed clients — and becomes documentation. Record after each phase gate.

## Feedback rounds (the scope-protecting machinery)

- Per SOW: N rounds per phase (default 2), consolidated, from the named decision maker.
  When scattered feedback arrives from three stakeholders, merge it into one document and
  send it back for the decision maker's arbitration BEFORE acting — this single habit
  prevents most project death-spirals.
- Triage every comment into: **(a) execute** (clear, in scope), **(b) translate** (the
  client named a solution; find the problem behind it — "make the logo bigger" usually
  means "I can't find us on the page"), **(c) push back** (violates the agreed direction
  or quality bar — respond with rationale + an alternative that serves the underlying
  concern), **(d) change request** (new scope — price it kindly via the SOW's mechanism,
  never absorb it silently: silent absorption teaches clients that scope is free).
- Log every round: `FEEDBACK-LOG.md` — date, round #, comments, disposition, who approved.
  This file settles every "but we asked for…" dispute before it starts.

## Staging discipline

- Password-protected staging URL per phase gate; `noindex`; seeded with REAL content state
  (placeholders labeled honestly — clients judge lorem ipsum as broken, so ship the
  copywriter's draft copy instead).
- Never present from localhost or a half-deployed state; a broken staging moment costs
  more trust than a week's delay.
- Keep a `CHANGELOG-CLIENT.md` in plain language ("Added the seasonal menu section;
  booking bar now stays visible on phones") — clients read this, not git.

## The handoff package (what "done" means at agency tier)

Deliver `/handoff` containing:

1. **The property**: production access transferred (hosting, domain, DNS documented),
   repository access, all credentials rotated to client ownership.
2. **The documentation**: LAUNCH.md (from launch-seo) · BRAND.md + kit (if scoped) ·
   asset manifest with remaining `awaiting-user` items · CMS editor guide (from
   cms-integration) · "how to break glass" page (what to do when something's down, who
   to call).
3. **The training**: 30–45 min recorded session — editing content end-to-end (create,
   preview, publish), the 5 most common tasks, the 3 things never to touch. Recorded so
   staff turnover doesn't erase it.
4. **The measurement**: analytics access, the dashboard showing the discovery success
   metric, and a "first 90 days" reading guide.
5. **The care offer**: what the retainer covers (updates, trend-watch, performance
   monitoring, priority fixes), priced; and what self-service looks like if they decline.
   Present as continuity, not dependency.

Close with a **project retrospective note** (internal): what the client valued most,
where scope strained, what the next proposal should price differently — the compounding
asset of an agency is calibrated scoping.

## Tone rules (all client-facing artifacts)

- Plain language, zero jargon ("the menu that stays at the top" not "sticky nav"), short
  paragraphs, always leading with what it means for their goal.
- Confident, never defensive: feedback is information about their business, not a verdict
  on the work.
- Every "no" ships with an alternative; every delay ships with a new date; every surprise
  ships before they find it themselves.
