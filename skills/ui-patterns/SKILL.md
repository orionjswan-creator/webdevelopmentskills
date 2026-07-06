---
name: ui-patterns
description: Award-grade UI component patterns — navigation, buttons, forms, cards, modals/drawers, accordions, footers, tables — with concrete specs and the taste rules that make each read premium instead of template. Use when building or polishing any individual UI component, alongside a style skill (which sets the tokens) and design-taste (which sets the judgment).
---

# UI Patterns

Component-level craft. The style skill decides *what things look like* (tokens); design-taste
decides *judgment calls*; this skill is the **spec sheet per component** — the details juries
and users feel but rarely name. Every pattern below assumes the site's tokens
(`--surface/--ink/--accent`, motion tokens) and works in any stack.

## Navigation

**Minimal bar (default for most styles)** — logo left, 3–5 text links, one CTA right.
- Height 64–80px; background transparent over hero → solid/glass after scroll
  (`IntersectionObserver` on a hero sentinel, class swap, 0.3s).
- Hide-on-scroll-down / show-on-scroll-up for long pages (translateY, 0.3s) — never on
  pages with anchor navigation.
- Current-page state visible (underline or ink shift). Link hover: underline draws in from
  left (`background-size` trick) or ink→accent, 0.25s.
- Glass variant (trend-report rules: nav is the legit use): `backdrop-filter: blur(12px)` +
  1px bottom border at 8% + surface at 60–70% opacity.

**Overlay menu (immersive/editorial styles)** — full-screen takeover:
- Trigger: "Menu" text or hamburger with a real morph to ✕ (two lines rotating, 0.3s).
- Panel: curtain from top or clip-circle from trigger, `expo.inOut` 0.6s; links as display
  type, masked line reveal with 0.06s stagger; mono meta (socials, email) at the edges.
- MUST: focus-trapped, Esc closes, scroll locked (`overflow:hidden` + scrollbar-gutter
  compensation), closes on route change.

**Mobile:** thumb-reachable CTA, 44px+ targets, the overlay pattern (drawer-from-side reads
dated unless brutalist).

## Buttons & links

The button system is 4 variants max: primary, secondary/ghost, text-link, icon.
- Primary: the accent, used ONCE per viewport ideally. Padding ratio ~1:2.6 (e.g. 14px/36px);
  radius per style system; label never wraps.
- Hover is a **composed micro-event** (pick per style, apply to ALL primaries identically):
  fill sweep (pseudo-element translateX), ink/surface inversion, letter-spacing +0.02em,
  or magnetic pull (motion-recipes §7). Press: scale 0.98 or brutalist depress. Focus:
  visible ring in accent, 2px offset — styled, never removed.
- Async buttons morph in place: label → spinner → "Done ✓" (min-width locked so no jump).
- Links in prose: underlined always (thickness 1–1.5px, `text-underline-offset: 3px`),
  accent or ink — never color-only differentiation.
- Arrow affordance: `→` that translates 4px on hover (0.25s) is the cheapest premium signal
  on text CTAs; `↗` for external.

## Forms & inputs

Forms are where "award site" most often collapses into "bootstrap page". Spec:
- Labels always visible above the field (never placeholder-as-label); placeholder shows
  *format* only (`you@studio.com`).
- Field style matches the design system: either underline-only (editorial/agency: 1px
  bottom border, focus = border draws to accent + label shifts up) or contained (product:
  surface + 1px border, focus = accent border + subtle ring).
- Inline validation on blur, not on every keystroke; errors say how to fix; error color
  pairs with an icon (not color-only). Success state is calm, not confetti.
- The submit journey: button morph (above) → success block replaces form (with next-step
  copy) — never a browser alert or a bare toast for the primary form.
- Newsletter one-liner: single field + inline arrow-button inside the field's right edge.

## Cards (work/product/article/bento)

- The whole card is the link (wrap or absolutely-positioned pseudo-link), cursor confirms.
- Image zone: fixed aspect (4:5 work, 4:3 article, 1:1 product alt), `overflow:hidden`,
  hover scale 1.04–1.06 @ 0.6–0.8s expo — the universal award hover. Text zone: meta (mono),
  title, one-liner; hover shifts title ink→accent or letter-spacing +0.02em.
- Never: drop-shadow-on-hover-only (lifts card off its own design), tilt-on-hover
  (dated), more than one animated property family per hover.
- Bento cells (viral/saas styles): border 1px at 10%, hover = border→accent-at-40% + inner
  spotlight following cursor (CSS vars from pointermove); one LIVE cell per grid.

## Modals & drawers

- Only three legit modals: cart drawer, media lightbox, command palette. Everything else is
  a page or inline disclosure.
- Drawer (cart/filter): from right, 420–480px, `expo.out` 0.5s, scrim at 40% ink + blur 4px,
  content staggers in 0.05s after panel. Scrim click + Esc close; focus trapped; underlying
  scroll locked with gutter compensation.
- Lightbox: opens FROM the clicked image (FLIP/View Transition morph), never from center-zero.
- Command palette (⌘K, saas/portfolio): instant (<50ms open), fuzzy match, keyboard-first.

## Accordions & disclosure

- The award accordion: full-width rows, hairline top borders, question in display-adjacent
  weight, `+` rotating to `×` (0.3s), panel height animated via `grid-template-rows: 0fr→1fr`
  (modern, no JS measuring) — or native `<details>` styled, with `interpolate-size` where
  supported.
- Row hover: background shifts one surface step. One open at a time on marketing pages;
  multi-open in docs/FAQ contexts.

## Footers

The footer is a designed destination, not a dump:
- Award pattern: oversized brand moment (giant wordmark, huge email link, or marquee) ABOVE
  the utility grid. The utility grid: 3–4 columns max, mono/small links, legal line.
- Include: the colophon habit (stack, typefaces, location — genre handshake), current year
  computed, one delight (local time, "back to top" with smooth scroll + focus reset).
- Footer-reveal effect (sticky-bottom parallax, agency styles): motion-recipes; skip on
  short pages.

## Tables & data

- Real `<th scope>`, sticky header row on long tables, tabular-nums for number columns,
  right-align numbers, zebra via 2–3% ink (not gray-200), row hover one surface step.
- Responsive: priority-drop columns or horizontal scroll INSIDE the table container with
  edge-fade hints — never squash to unreadable.

## Toasts & feedback

- One toast at a time, bottom-left or top-center, enters translateY+fade 0.35s, self-dismisses
  4s with a subtle progress, hover pauses. Toasts are for confirmations of *background*
  actions only — primary-flow feedback happens in place (button morphs, inline blocks).

## Universal component QA

- Keyboard: reachable, operable, visible focus, logical order, Esc where dismissible
- Touch: 44px min, hover-equivalents exist, no hover-trapped content
- Reduced motion: every animation above has a fade-or-instant fallback
- Density check: paste the component next to the style skill's blueprint — same radius,
  border, spacing tokens? Any stray value = fix the token usage, not the component
- The 100ms rule: something visibly responds within 100ms of every interaction
