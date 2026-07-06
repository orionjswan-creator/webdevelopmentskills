# Audio reactivity — from sound to Signals

Everything between the mixer and the shader. The output of this file is the **Signals
object** every scene consumes: `{ bass, mid, high, level, beat, bpm, energy }`, all values
smoothed to 0–1.

## 1. Audio input (live sources, in order of preference)

```ts
// audio/input.ts
export async function getAudioStream(deviceId?: string) {
  // CRITICAL for music: disable all voice processing or the analyser hears mush
  return navigator.mediaDevices.getUserMedia({
    audio: {
      deviceId: deviceId ? { exact: deviceId } : undefined,
      echoCancellation: false,
      noiseSuppression: false,
      autoGainControl: false,
      channelCount: 2,
    },
  });
}
// List inputs so the operator picks "USB audio interface" not "MacBook Microphone":
export async function listInputs() {
  await navigator.mediaDevices.getUserMedia({ audio: true }); // permission first
  return (await navigator.mediaDevices.enumerateDevices())
    .filter(d => d.kind === 'audioinput');
}
```

Gig reality: the right feed is a **line out from the mixer into a USB interface**
(booth mic as fallback — it works surprisingly well but pumps with crowd noise). The
control panel MUST have an input selector + input gain slider; wrong-device is the #1
soundcheck failure.

## 2. Analysis → Signals

```ts
// audio/signals.ts
export class SignalEngine {
  private analyser: AnalyserNode;
  private bins: Uint8Array;
  readonly signals = { bass: 0, mid: 0, high: 0, level: 0, beat: 0, bpm: 120, energy: 0 };
  private smooth = { bass: 0, mid: 0, high: 0, level: 0 };
  private beatEnv = 0; private lastBeatT = 0; private beatIntervals: number[] = [];

  constructor(ctx: AudioContext, source: AudioNode) {
    this.analyser = ctx.createAnalyser();
    this.analyser.fftSize = 2048;                  // ~21.5Hz per bin @48kHz
    this.analyser.smoothingTimeConstant = 0;       // we do our own smoothing
    source.connect(this.analyser);
    this.bins = new Uint8Array(this.analyser.frequencyBinCount);
  }

  private band(lo: number, hi: number) {           // Hz → average magnitude 0–1
    const hzPerBin = this.analyser.context.sampleRate / this.analyser.fftSize;
    let sum = 0, n = 0;
    for (let i = Math.floor(lo / hzPerBin); i <= Math.min(Math.ceil(hi / hzPerBin), this.bins.length - 1); i++) {
      sum += this.bins[i]; n++;
    }
    return n ? sum / (n * 255) : 0;
  }

  update(t: number) {
    this.analyser.getByteFrequencyData(this.bins);
    const raw = {
      bass: this.band(20, 150),      // kick + sub
      mid: this.band(400, 2000),     // synths, vocals
      high: this.band(4000, 12000),  // hats, air
      level: this.band(20, 16000),
    };
    // Asymmetric smoothing: fast attack (feels tight), slow release (feels musical)
    for (const k of ['bass', 'mid', 'high', 'level'] as const) {
      const a = raw[k] > this.smooth[k] ? 0.5 : 0.08;
      this.smooth[k] += (raw[k] - this.smooth[k]) * a;
      this.signals[k] = this.smooth[k];
    }
    this.detectBeat(raw.bass, t);
    // energy: slow-moving set intensity (30s window) — drives palettes/autopilot
    this.signals.energy += (this.signals.level - this.signals.energy) * 0.002;
  }

  private detectBeat(bass: number, t: number) {
    // Envelope + threshold with refractory period — robust for 4/4 electronic music
    this.beatEnv = Math.max(bass, this.beatEnv * 0.95);
    const fired = bass > 0.35 && bass > this.beatEnv * 0.9 && t - this.lastBeatT > 0.25;
    if (fired) {
      const interval = t - this.lastBeatT; this.lastBeatT = t;
      if (interval > 0.3 && interval < 1.0) {            // 60–200 BPM plausible
        this.beatIntervals.push(interval);
        if (this.beatIntervals.length > 16) this.beatIntervals.shift();
        const med = [...this.beatIntervals].sort((a, b) => a - b)[this.beatIntervals.length >> 1];
        this.signals.bpm = Math.round(60 / med);
      }
    }
    // beat is a decaying impulse: 1.0 on hit → 0 (scenes use it as a kick envelope)
    this.signals.beat = fired ? 1 : this.signals.beat * 0.92;
  }
}
```

## 3. Tuning guide (do this with real music of the target genre)

- Meters in the control panel for all seven signals — tune by eye against known tracks.
- **Bass band**: techno kicks live 40–100Hz; if `beat` double-fires on off-beat bass
  lines, narrow to 40–90Hz and raise the refractory to 0.3s.
- **Auto-gain option**: track a rolling max per band (`max = Math.max(raw, max * 0.999)`)
  and normalize by it — makes the instrument survive quiet openers and hot mixers alike.
- Genre presets: expose the band ranges + attack/release as a "genre" dropdown
  (techno / bass / melodic / ambient) rather than hardcoding.
- **Latency**: input → screen should feel < 50ms. Keep `fftSize ≤ 2048`, don't add
  Web Audio graph beyond source→analyser, and render beat reactions on the SAME frame
  the signal updates (update Signals at the top of the rAF loop, then render).

## 4. Beat-quantized choreography

```ts
// Musical clocks derived from bpm — snap scene changes to phrases
const beatDur = 60 / signals.bpm;
const bar = beatDur * 4, phrase = bar * 8;
// e.g. autopilot advances scenes on phrase boundaries; camera cuts on bars
```

Cutting on phrase boundaries (not on a timer) is the single biggest "this VJ knows the
music" tell — 30 minutes of implementation, disproportionate payoff.

## 5. MIDI control (WebMIDI — Chrome/Edge)

```ts
// control/midi.ts — map any knob/pad by learn-mode
export async function initMidi(onCC: (cc: number, v: number) => void,
                               onNote: (note: number, on: boolean) => void) {
  const access = await navigator.requestMIDIAccess();
  for (const input of access.inputs.values()) {
    input.onmidimessage = (m) => {
      const [status, d1, d2] = m.data!;
      const type = status & 0xf0;
      if (type === 0xb0) onCC(d1, d2 / 127);            // knobs/faders
      if (type === 0x90) onNote(d1, d2 > 0);            // pads down
      if (type === 0x80) onNote(d1, false);             // pads up
    };
  }
}
// Learn mode: click a param in the panel → wiggle a knob → bind (store cc→param in
// localStorage). Never hardcode a controller layout; every VJ's controller differs.
```

Standard performance mapping to implement regardless of controller: pads 1–8 = scenes ·
one fader = master intensity · one fader = crossfade · knobs = active scene's params ·
one pad = blackout · one pad = logo/ident · one pad = autopilot toggle. Mirror all of it
on the keyboard (1–8, space=blackout, L=logo, A=autopilot) — controllers get forgotten
in cars.

## 6. Audience interaction inputs (installation contexts)

- **Phones as controllers**: QR on a placard → tiny page with a fat slider/button →
  WebSocket (one `ws` relay on the local machine/hotspot) → aggregated into a Signals-like
  `crowd` object (mean + excitement variance). Aggregate, never map one phone 1:1 — mobs
  average into beauty, individuals troll.
- **Camera/body**: MediaPipe pose/segmentation → silhouette texture or motion-amount
  scalar into the shader (performance cost: run at 15–20fps on a worker, interpolate).
- **Hardware sensors** (playa installations): an Arduino/ESP32 reading PIR/ultrasonic/
  encoder speaks serial-over-USB (Web Serial API) or WebSocket over the ESP's own AP.
  Keep the sensor protocol dumb: one line of numbers per tick.

All interaction inputs merge INTO Signals (extra fields) so scenes stay source-agnostic —
a piece tuned for audio runs on crowd energy at a silent installation by remapping, not
rewriting.
