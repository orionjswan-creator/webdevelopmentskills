# Performance rig — outputs, venues, safety, show-night ops

The plumbing that turns shader scenes into a giggable instrument: windows, capture,
venue formats, the safety limiter, and the checklists that survive real booths.

## 1. Two-window architecture

```ts
// control window opens the output window; they talk over BroadcastChannel
const bc = new BroadcastChannel('rig');
const out = window.open('/output.html', 'output', 'width=1280,height=720');
// output.html: chromeless canvas, black background, cursor hidden, no UI whatsoever
bc.postMessage({ type: 'scene', id, crossfadeMs: 2000 });
bc.postMessage({ type: 'params', values });
bc.postMessage({ type: 'signals', s });   // control does audio analysis; output renders
```

- Output window goes on the second display; fullscreen via double-click handler
  (`canvas.requestFullscreen()` — must be user-gesture).
- Alternative single-window mode (`?output=1`) for capture setups without a physical
  second display.
- Crossfading: output holds TWO scene instances and mixes in the final grading pass
  (`mix(sceneA, sceneB, xfade)`) — never CSS opacity between canvases (double GPU cost,
  broken blending).
- Preview in the control window: a small canvas rendering the same scene at 25% scale —
  never `drawImage` from the output (cross-window canvas copies stall).

## 2. Getting pixels to the wall (in order of gig-likelihood)

| Route | How | Notes |
|---|---|---|
| **HDMI straight to screen/TV/projector** | laptop second output = the output window fullscreened | Bars, small clubs, house parties. Set display to mirror-off, native res |
| **Into Resolume/VDMX (the pro VJ route)** | window capture / Spout via OBS | The venue VJ mixes your piece with their rig. Deliver: your app runs locally + a one-page cheat sheet |
| **OBS → anywhere** | OBS window-capture of the output window → NDI plugin / virtual cam / recording | NDI reaches media servers over LAN. Also the route to pre-render loops (below) |
| **LED processor direct** | processor presents as a display with a custom EDID resolution | Festival walls: ask the LED tech for the *processor input res* (often 1920×1080 scaled) vs the *wall's native pixel map* — design for the native map's aspect |
| **Pre-rendered loops** | capture 1–4 bar loops at exact BPM as ProRes/HAP | For venues that only accept files (many big rooms and most Vegas-scale surfaces). Render deterministic time (fixed timestep), export via OBS or headless Chrome + ffmpeg |

**Vegas-scale / spherical / wrap-around surfaces** (Sphere-class rooms, strip billboards,
360° club walls): these run proprietary media-server pipelines with extreme custom
formats (multi-thousand-pixel-wide maps, equirect/fisheye projections for domes) and
content is commissioned/delivered as files through the venue's spec, not plugged in live.
Your browser piece is still the right *authoring* tool: render deterministic frames at
the delivered map's resolution in tiles if needed (fixed-timestep + `canvas.toBlob` frame
dumps → ffmpeg), and design with the venue's template/preview mesh. Get the spec sheet
first; never guess a dome projection.

## 3. Venue format presets (build these into the output window)

| Preset | Res/aspect | Design notes |
|---|---|---|
| Standard projector/TV | 1920×1080 | vignette OK, lift blacks |
| Club LED wall | often 1920×1080 into odd-aspect walls | ask for pixel map; crush blacks; no 1px detail |
| DJ booth strip | ultra-wide, e.g. 3840×720 or worse | design in bands; center-weighted (edges get cut) |
| Festival side wings | 2× portrait walls, mirrored | one scene, `kale`-mirrored per side |
| IMAG/broadcast overlay | 1080p keyed | design against black, alpha-friendly shapes |
| Dome/spherical | per venue spec | fisheye/equirect warp pass; author only with the spec |

Aspect is a *design input*: run every scene in every preset you'll gig — a tunnel
composed for 16:9 dies on a 12:1 booth strip; flow fields and particles survive
everything (compose scenes from center-out, nothing critical in outer 15%).

## 4. The safety limiter (non-negotiable, CPU-side, before uniforms)

Photosensitive-seizure guidance (WCAG 2.3 / broadcast practice): **≤ 3 general flashes
per second**, and no saturated-red full-field flashing. Implement as the ONLY path to
flash uniforms:

```ts
// output/limiter.ts — all flash/strobe requests route through here
class FlashLimiter {
  private times: number[] = [];
  request(intensity: number, now: number): number {
    this.times = this.times.filter(t => now - t < 1);
    if (this.times.length >= 3) return 0;          // budget spent this second
    this.times.push(now);
    return Math.min(intensity, 1);
  }
}
// Plus: master strobe-rate cap for oscillating brightness (no square-wave luma > 3Hz),
// a "strobe-safe mode" toggle (halves flash budget, for venues that require it),
// and clamp: full-field flashes never saturated red (shift hue or desaturate).
```

Log limiter interventions to the control panel so the operator learns the instrument's
limits in rehearsal, not on stage.

## 5. Show-night operations

**The rig checklist (soundcheck, in order):**
1. Power settings: sleep off, screen-blank off, notifications off (macOS Focus /
   Windows Focus Assist), auto-updates paused, WiFi OFF (nothing needs it; captive
   portals steal focus).
2. Audio: correct input selected, gain set against the mixer at show level, meters alive.
3. Output: correct display, fullscreen, native resolution confirmed (check the wall for
   scaling artifacts with a 1px checker test card — build one in as a scene).
4. Controller: MIDI bound (learn-mode persisted), blackout/logo/autopilot keys verified.
5. Run the strobe-bait track; watch the limiter log.
6. 10-minute burn with Activity Monitor/Task Manager open: GPU thermals, memory flat.

**During the set:** the three keys that matter are blackout (instant, also on spacebar),
logo/ident, autopilot. Everything else is performance, these are safety. Crash recovery:
app reopens into last state in < 2s (state in localStorage, output window auto-reopens).

**Kiosk/installation mode (Burning Man register):**
- Auto-start: OS auto-login + browser in kiosk mode (`chromium --kiosk --app=file://…`)
  on boot; watchdog script relaunches on crash; daily 5am scheduled reboot.
- Hardware: mini-PC or high-end SBC in a dust-sealed case (playa dust is conductive
  talc — filters + positive pressure), 12V power budget documented for the camp's solar,
  panel brightness scheduled (full at night, survival mode in day sun).
- No network, no accounts, no dialogs: test by power-cycling ten times.
- Interaction hardware per audio-reactive §6; physical controls beat touchscreens in
  dust and gloves.

## 6. Deliverables per gig type

| Gig | Deliver |
|---|---|
| DJ set (you/artist operates) | The instrument + controller map card + soundcheck checklist |
| Venue VJ integrates it | App + one-pager (launch, scenes, params, capture notes) + loop renders as fallback |
| File-spec venue (Vegas-scale) | Rendered files to spec + slate/versioning + preview renders on the venue template |
| Installation | Auto-boot image, hardware list, power budget, on-playa repair notes, teardown checklist |
| Livestream | OBS scene collection with the browser source pre-configured |
