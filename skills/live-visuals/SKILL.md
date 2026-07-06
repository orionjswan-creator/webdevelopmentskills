---
name: live-visuals
description: Build interactive, audio-reactive virtual art for live events — EDM concerts, DJ sets, club and festival LED walls, Vegas-scale venue screens, and Burning Man-style interactive installations. For Sonnet 5 / Codex: produces a browser-based real-time visual instrument (WebGL/GLSL) with live audio analysis, MIDI/keyboard control, scene system, and a capture-ready output window. Use when asked for VJ visuals, concert/stage visuals, generative art for events, DJ screen content, or interactive installations.
---

# Live Visuals

You are building a **visual instrument, not a video** — a real-time generative piece that
listens to the music, responds to a performer's controls, and runs for hours without
dropping frames. The browser is a legitimate pro tool here (VJs run browser sources into
Resolume/OBS every weekend); everything ships as a self-contained web app that works on a
laptop plugged into anything from a bar TV to a festival LED processor.

**The one law of live visuals: 60fps is the artwork.** A beautiful shader at 40fps reads as
broken on a 60-foot wall. Every aesthetic decision defers to the frame budget.

## Inputs to gather (ask in one batch, or default and state)

1. **Context**: DJ set / concert stage / club ambient / art installation / festival wall?
2. **Output surface**: resolution + aspect (see performance-rig for venue formats), LED
   wall or projector, viewing distance.
3. **Music genre & energy arc** (a techno set and a melodic-bass set need different
   instruments), or for installations: the interaction concept.
4. **Who operates it**: performer with a MIDI controller / unattended autopilot / audience-
   interactive?
5. **Brand/motif constraints**: artist logo, palette, tour identity (asset-creation skill
   supplies logo/texture assets via the manifest as usual).

## Architecture (build exactly this separation)

```
src/
  engine/     renderer setup, render loop, resize, quality governor
  audio/      input → analysis → the Signals object        (references/audio-reactive.md)
  scenes/     each scene = shader(s) + params + its Signals mapping
  control/    keyboard/MIDI mapping, control panel UI, preset store
  output/     output window management, crossfader, safety limiter
```

- **The Signals object** is the contract between sound and picture:
  `{ bass, mid, high, level, beat, bpm, energy }` — every scene reads ONLY Signals +
  params, never raw audio. This is what makes scenes swappable mid-set.
- **Scenes** are full-screen shader pieces (or Three.js scenes) implementing:
  `init(gl)`, `render(t, signals, params)`, `dispose()`. 4–8 scenes = a set.
- **Two windows**: control window (panel, preview, meters) and a chromeless **output
  window** (visuals only, fullscreened on the second display / capture target).
  Sync via `BroadcastChannel`. Details + capture routes: performance-rig.

## Stack

**Vite + TypeScript + raw WebGL2 fragment shaders** for shader-driven pieces (fastest,
smallest); **Three.js** when the piece needs real geometry/particles/3D cameras. GLSL is
the medium either way — the shader toolkit reference is the core library. WebGPU/TSL only
if the target machines are known and modern; WebGL2 runs on every venue laptop.

## Build order

1. **Rig first** (one session): engine + one placeholder scene + audio meters + output
   window + crossfade between two scenes. A working instrument with ugly scenes beats
   beautiful shaders with no rig — the rig is what survives contact with a real gig.
2. **Signals tuning**: run real music of the target genre through the analyzer; calibrate
   band ranges and beat detection until the meters *feel* like the track (audio-reactive
   reference has the recipes and the tuning guide).
3. **Scenes** (the art): build each from the shader toolkit's patterns + the aesthetic
   directions below. Every scene must be playable: 3–6 exposed params (intensity, hue,
   speed, complexity…) mapped to knobs/keys, and a defined idle→peak range driven by
   Signals.
4. **Set design**: order scenes by energy (opener, builders, peaks, breakdown, closer),
   assign hotkeys/pads, define the autopilot rotation for unattended stretches.
5. **Endurance pass**: 2-hour soak test — memory flat? thermals stable? quality governor
   (below) engaging correctly? Then the venue checklist in performance-rig.

## Aesthetic directions (pick one register per piece; mixing reads as preset-pack)

- **Peak-time techno/EDM**: tunnels, strobing geometry (within safety limits), raymarched
  structures, harsh mono-chrome with one acid accent, beat-locked cuts between camera
  states. Motion is *quantized* — snap on beats, glide between.
- **Melodic/organic**: flow fields, fluid feedback trails, aurora gradients, particle
  swarms breathing with `energy`; movement legato, palette shifts across the arc.
- **Playa/installation** (Burning Man register): organic generative systems (reaction-
  diffusion, flocking, growth algorithms), warm fire/dust palettes, slow evolution that
  rewards 20 minutes of watching, and **audience interaction as the core mechanic** —
  camera silhouettes, phone-as-controller, sensor inputs (performance-rig covers the
  interaction plumbing and desert-proofing: offline-first, kiosk boot, no network).
- **Luxury/ambient club**: slow gradient fields, grain, caustics, kaleidoscopic geometry
  at low contrast — visuals as architecture, never demanding attention.
- **Logo/identity moments**: the artist mark as a shader participant (SDF of the logo
  distorted/rebuilt by Signals) — asset-creation supplies the SVG→SDF texture.

## Non-negotiables

- **Photosensitivity safety**: the output pipeline includes a flash limiter — no more than
  3 general flashes per second, no full-field saturated-red flashing, strobe params capped
  in code not convention (performance-rig has the implementation). Festival/venue work
  without this is a liability.
- **Quality governor**: auto-drop internal render scale (0.5–1.0×) when frame time exceeds
  budget for >30 frames, restore when stable. Resolution scales, never the frame rate.
- **No network dependency at showtime**: all assets local, fonts local, no CDN — venues
  have no wifi and the playa has nothing.
- **Deterministic recovery**: a crash/reload lands back in the last scene within 2 seconds
  (state in localStorage). The show must not die with a tab.
- **DPR clamp = 1 on output** (you're rendering to a known pixel grid — LED walls don't
  have retina), IntersectionObserver pause is NOT used (output must never pause).

## QA (per scene, then per set)

- 60fps at output resolution on the actual gig laptop (or its GPU class), 2-hour soak flat
- Signals mapping legible: a stranger watching meters + visuals sees the music
- Beat response latency under ~50ms feel (audio-reactive's latency notes)
- Flash limiter verified with a strobe-bait test track
- Blackout key (instant), logo key, and autopilot verified — the three keys every VJ
  actually hits under pressure
- Reads at distance: check scenes scaled to a phone-sized preview at 10ft — LED walls are
  viewed at 50–200ft; fine detail vanishes, silhouettes and motion survive
