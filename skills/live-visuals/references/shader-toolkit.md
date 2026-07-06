# Shader toolkit — GLSL patterns for live visuals

The scene library's raw material. All fragments assume the standard rig: a full-screen
quad, WebGL2 (`#version 300 es`), and this uniform contract (keep it identical across
every scene so scenes are hot-swappable):

```glsl
uniform vec2  uRes;       // output resolution
uniform float uTime;      // seconds
uniform float uBass, uMid, uHigh, uLevel, uBeat, uEnergy;  // Signals, 0-1
uniform vec4  uParams;    // the scene's 4 performable knobs, 0-1
uniform sampler2D uPrev;  // previous frame (feedback scenes)
uniform sampler2D uLogo;  // SDF texture of the artist mark (optional)
```

JS side: one program per scene, one shared quad VAO, uniforms updated per frame from
Signals. Internal render scale from the quality governor: render to a framebuffer at
`scale × output`, blit up — LED walls hide upscaling completely.

## 1. Core utilities (paste into every shader)

```glsl
float hash(vec2 p){ p = fract(p*vec2(123.34,456.21)); p += dot(p,p+45.32); return fract(p.x*p.y); }
float noise(vec2 p){ vec2 i=floor(p), f=fract(p); f=f*f*(3.-2.*f);
  return mix(mix(hash(i),hash(i+vec2(1,0)),f.x), mix(hash(i+vec2(0,1)),hash(i+1.),f.x), f.y); }
float fbm(vec2 p){ float v=0., a=.5; for(int i=0;i<5;i++){ v+=a*noise(p); p*=2.02; a*=.5; } return v; }
mat2 rot(float a){ float c=cos(a), s=sin(a); return mat2(c,-s,s,c); }
```

## 2. Cosine palettes (the live-visuals color system)

One function, infinite genre-correct palettes — and palettes become performable:

```glsl
vec3 pal(float t, vec3 a, vec3 b, vec3 c, vec3 d){ return a + b*cos(6.28318*(c*t+d)); }
// Registers (swap via uniforms/param):
// acid techno:  pal(t, vec3(.5), vec3(.5), vec3(1.), vec3(.0,.33,.67))
// fire/playa:   pal(t, vec3(.5,.36,.25), vec3(.5,.36,.25), vec3(1.), vec3(.0,.1,.2))
// aurora:       pal(t, vec3(.2,.5,.4), vec3(.2,.4,.3), vec3(1.), vec3(.3,.2,.1))
// Drive t with uEnergy for set-long palette arcs; snap d on uBeat for peak-time cuts.
```

## 3. Flow field (melodic/organic workhorse)

```glsl
// domain-warped fbm — the aurora/smoke/silk family
vec2 uv = (gl_FragCoord.xy*2. - uRes) / uRes.y;
vec2 q = vec2(fbm(uv + uTime*.05), fbm(uv + 1.7));
vec2 r = vec2(fbm(uv + 3.*q + uTime*.1 + uBass*.5), fbm(uv + 3.*q + 8.2));
float f = fbm(uv + 3.*r);
vec3 col = pal(f + uEnergy*.3, /* palette */);
col *= .6 + .8*uLevel;                       // breathe with the music
```

## 4. Raymarched tunnel (peak-time workhorse)

```glsl
// march a repeating SDF down -z; twist with mids, kick the camera with beats
float map(vec3 p){
  p.xy *= rot(p.z*.1 + uTime*.1);                      // twist
  p.z = mod(p.z, 4.) - 2.;                             // infinite repetition
  float d = length(max(abs(p.xy)-vec2(1.5 + uMid), 0.)) - .1;  // square ring
  return d;
}
// standard 64-step march; shade by iteration count (cheap glow):
// col = pal(float(i)/64. + uBeat*.2, ...) * exp(-dist*.15);
// beat kick: ro.z += uBeat*.6;  camera roll: rd.xy *= rot(uBeat*.1*sign(sin(uTime)));
```

Budget: ≤ 80 steps, no nested marching, `exp()` fog instead of AO. A tunnel that runs at
1.0 scale beats a cathedral at 0.6.

## 5. Feedback / trails (the analog-video soul)

Ping-pong two framebuffers; sample `uPrev` with a transform — everything else is flavor:

```glsl
vec2 uv = gl_FragCoord.xy / uRes;
vec2 c = uv - .5;
c *= 1.0 - .015*(1.+uBass);          // zoom feedback (bass pushes deeper)
c *= rot(.005 + uMid*.02);           // rotation drift
vec3 prev = texture(uPrev, c + .5).rgb * (0.96 - uParams.x*0.1);  // decay knob
vec3 ink = /* this frame's fresh element: a beat-flash shape, particles, the logo SDF */;
fragColor = vec4(max(prev, ink), 1.);   // max() = additive trails that don't blow out
```

Hue-shift the feedback (`prev.rgb = prev.brg` mixed at 2–5%) for the classic VHS-bloom
drift. This ONE pattern, with different `ink` layers, is half of professional VJ packs.

## 6. Particles (GPU, no libraries)

Positions/velocities in two RG32F ping-pong textures updated by a simulation fragment
shader (curl-noise steering + `uBeat` impulse), drawn as `gl.POINTS` (size by depth,
additive blending). 100k points is comfortable on integrated GPUs at 1080p. Swarm rules:
attract to logo SDF at breakdowns (`uParams.y`), explode on beat, re-gather over 2 bars.

## 7. Kaleidoscope / mirror (instant stage-wear for any scene)

```glsl
vec2 kale(vec2 uv, float n){         // n segments; drive n with a param knob (2..12)
  float a = atan(uv.y, uv.x), r = length(uv);
  float seg = 6.28318 / n;
  a = abs(mod(a, seg) - seg*.5);
  return vec2(cos(a), sin(a)) * r;
}
// Apply to ANY scene's uv first. n snapping on phrase boundaries = free choreography.
```

## 8. Logo as participant (SDF ident moments)

Bake the artist SVG to an SDF texture offline (or at load: render SVG → canvas → JFA
pass). Then the mark is material, not a sticker:

```glsl
float d = texture(uLogo, uv).r - .5;                   // signed distance
float mark = smoothstep(.01, .0, d);                   // crisp fill
float glow = exp(-max(d, 0.)*8.) * (0.5 + uBeat);      // beat-pumped halo
// distort uv by fbm(uv*3.+uTime) * (1.-uParams.z) to melt/rebuild the mark
```

## 9. Strobe & flash elements — ALWAYS through the limiter

Never write `if (uBeat > .5) col = vec3(1.)` directly. Flash intensity routes through the
rig's safety limiter uniform (performance-rig §safety): `col += vec3(uFlash)` where
`uFlash` is computed CPU-side with rate capping. Design flashes as *local* (a shape, a
ring) rather than full-field whenever the register allows — reads bigger, safer by
construction.

## 10. Grading pass (one final full-screen pass over every scene)

```glsl
col = pow(col, vec3(1./1.9));                          // lift for LED gamma
col *= 1. - .35*dot(uv-.5, uv-.5)*4.;                  // vignette (projector) — SKIP for LED walls
col += (hash(gl_FragCoord.xy + uTime) - .5) * .02;     // dither: kills LED banding
// master intensity fader multiplies here — the fader must dim EVERYTHING
```

LED walls: crush blacks (`col = max(col-.02, 0.)`) — near-black noise looks like a broken
panel at 100ft. Projectors: the opposite — keep floors lifted, avoid pure black scenes.

## Scene assembly rule

A scene = **one base pattern (§3–6) + one transform (§7) + palette (§2) + grading (§10)**,
with 4 knobs exposed and every Signals field visibly doing something. If a knob doesn't
read on the preview from 10 feet, rewire it to something that does — performers only
touch knobs that visibly work.
