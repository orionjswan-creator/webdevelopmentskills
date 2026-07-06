# Motion recipes

Copy-paste recipes for the motion patterns that recur across Awwwards/FWA winners.
Stack: **GSAP + ScrollTrigger** (scroll choreography), **Lenis** (smooth scroll), **Three.js**
(WebGL moments). All vanilla-JS; adapt trivially to React (`useEffect`/`useGSAP`) or Astro
(client scripts).

```bash
npm i gsap lenis three
```

## 0) The reduced-motion guard (wrap ALL motion in this)

```js
const prefersReduced = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

export function withMotion(setup) {
  if (prefersReduced) return;       // content must be fully visible & usable without motion
  setup();
}
// CSS side: gate transitions/animations too
// @media (prefers-reduced-motion: reduce) { *, *::before, *::after {
//   animation-duration: 0.01ms !important; transition-duration: 0.01ms !important; } }
```

Design rule: reveals should *end* at the element's natural resting state, so killing the
animation loses nothing but flair.

## 1) Lenis smooth scroll + GSAP sync

```js
import Lenis from 'lenis';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
gsap.registerPlugin(ScrollTrigger);

const lenis = new Lenis({ lerp: 0.1, wheelMultiplier: 1 });
lenis.on('scroll', ScrollTrigger.update);
gsap.ticker.add((t) => lenis.raf(t * 1000));
gsap.ticker.lagSmoothing(0);
```

Keep native scroll semantics: never disable keyboard/anchor scrolling. Skip Lenis entirely on
touch devices if it fights the platform (`syncTouch: false` is the default — leave it).

## 2) Masked line reveal (the signature award-site text animation)

Split headings into lines, wrap each in an overflow-hidden mask, slide up with a stagger.

```js
// splitLines: wrap each visual line in <span class="line"><span class="line-inner">…</span></span>
function splitLines(el) {
  const words = el.textContent.trim().split(/\s+/);
  el.innerHTML = words.map(w => `<span class="w">${w}</span>`).join(' ');
  const lines = new Map();
  el.querySelectorAll('.w').forEach(w => {
    const top = w.offsetTop;
    if (!lines.has(top)) lines.set(top, []);
    lines.get(top).push(w);
  });
  el.innerHTML = [...lines.values()].map(ws =>
    `<span class="line"><span class="line-inner">${ws.map(w => w.textContent).join(' ')}</span></span>`
  ).join(' ');
  return el.querySelectorAll('.line-inner');
}
// CSS: .line{display:block;overflow:hidden} .line-inner{display:block;transform:translateY(110%)}

document.querySelectorAll('[data-reveal]').forEach(el => {
  const lines = splitLines(el);
  gsap.to(lines, {
    y: 0, duration: 1.1, ease: 'expo.out', stagger: 0.08,
    scrollTrigger: { trigger: el, start: 'top 85%', once: true },
  });
});
```

(If the project already ships GSAP's SplitText plugin, use it instead of the manual splitter.
Re-split on resize, debounced.)

## 3) Scroll-scrubbed pin (storytelling section)

```js
gsap.timeline({
  scrollTrigger: { trigger: '.story', start: 'top top', end: '+=200%', scrub: 0.8, pin: true },
})
  .from('.story .visual', { scale: 0.7, yPercent: 20 })
  .to('.story .headline', { yPercent: -30, opacity: 0 }, 0.4)
  .from('.story .caption', { opacity: 0, y: 40 }, 0.6);
```

Use for 1–2 hero moments only. `scrub: 0.8` (slight lag) feels more cinematic than `true`.

## 4) Parallax image

```js
document.querySelectorAll('[data-parallax]').forEach(el => {
  const speed = parseFloat(el.dataset.parallax || 0.15);
  gsap.to(el, {
    yPercent: speed * 100, ease: 'none',
    scrollTrigger: { trigger: el.parentElement, start: 'top bottom', end: 'bottom top', scrub: true },
  });
});
// markup: container overflow:hidden; img height:115%; data-parallax="0.15"
```

## 5) Clip-path image reveal

```js
gsap.utils.toArray('[data-img-reveal]').forEach(el => {
  gsap.fromTo(el,
    { clipPath: 'inset(0 0 100% 0)' },
    { clipPath: 'inset(0 0 0% 0)', duration: 1.2, ease: 'expo.inOut',
      scrollTrigger: { trigger: el, start: 'top 80%', once: true } });
  gsap.fromTo(el.querySelector('img'), { scale: 1.25 }, { scale: 1, duration: 1.4, ease: 'expo.out',
    scrollTrigger: { trigger: el, start: 'top 80%', once: true } });
});
```

## 6) Marquee (infinite, pausable, CSS-only)

```css
.marquee { overflow: hidden; display: flex; }
.marquee-track { display: flex; gap: 2rem; flex-shrink: 0; min-width: 100%;
  animation: marquee 24s linear infinite; }
.marquee:hover .marquee-track { animation-play-state: paused; }
@keyframes marquee { to { transform: translateX(-100%); } }
/* duplicate the track content twice in markup for the seamless loop */
```

## 7) Magnetic button + custom cursor

```js
// magnetic
document.querySelectorAll('[data-magnetic]').forEach(el => {
  const strength = 0.35;
  el.addEventListener('mousemove', e => {
    const r = el.getBoundingClientRect();
    gsap.to(el, { x: (e.clientX - r.left - r.width / 2) * strength,
                  y: (e.clientY - r.top - r.height / 2) * strength, duration: 0.4, ease: 'power3.out' });
  });
  el.addEventListener('mouseleave', () =>
    gsap.to(el, { x: 0, y: 0, duration: 0.6, ease: 'elastic.out(1,0.4)' }));
});

// cursor follower (augments, never replaces, the OS cursor)
const dot = Object.assign(document.createElement('div'), { className: 'cursor-dot' });
document.body.appendChild(dot);
const setX = gsap.quickTo(dot, 'x', { duration: 0.35, ease: 'power3' });
const setY = gsap.quickTo(dot, 'y', { duration: 0.35, ease: 'power3' });
window.addEventListener('mousemove', e => { setX(e.clientX); setY(e.clientY); });
document.querySelectorAll('a,button,[data-magnetic]').forEach(el => {
  el.addEventListener('mouseenter', () => dot.classList.add('is-hover'));
  el.addEventListener('mouseleave', () => dot.classList.remove('is-hover'));
});
// .cursor-dot { position:fixed; top:0; left:0; width:12px; height:12px; border-radius:50%;
//   background:var(--accent); pointer-events:none; z-index:9999; translate:-50% -50%;
//   transition:width .3s,height .3s; mix-blend-mode:difference }
// .cursor-dot.is-hover { width:56px; height:56px }
// Only init on (hover:hover) and (pointer:fine) media queries.
```

## 8) Preloader with counter → curtain reveal

```js
const tl = gsap.timeline();
const counter = { v: 0 };
tl.to(counter, { v: 100, duration: 1.6, ease: 'power2.inOut',
    onUpdate: () => (document.querySelector('.loader-num').textContent = Math.round(counter.v)) })
  .to('.loader', { yPercent: -100, duration: 0.9, ease: 'expo.inOut' })
  .from('h1 .line-inner', { y: '110%', duration: 1.1, ease: 'expo.out', stagger: 0.08 }, '-=0.35');
```

Cap total pre-content time ≤ 2.5s; tie the counter to *real* asset loading when possible; skip
the loader entirely on repeat visits (sessionStorage flag).

## 9) Page transition (curtain)

```js
// SPA/Next: run 'leave' before route change, 'enter' after.
// MPA: use the View Transitions API first, curtain as fallback.
const curtain = document.querySelector('.transition-curtain'); // fixed, inset:0, translateY(101%)
export const leave = () => gsap.to(curtain, { yPercent: -101, duration: 0.6, ease: 'expo.inOut' });
export const enter = () => gsap.to(curtain, { yPercent: -202, duration: 0.6, ease: 'expo.inOut', delay: 0.1 });
```

Native cross-document View Transitions (progressive enhancement, zero JS):

```css
@view-transition { navigation: auto; }
::view-transition-old(root) { animation: fade-out .4s ease both; }
::view-transition-new(root) { animation: fade-in .4s ease both; }
```

## 10) Native CSS scroll-driven animations (2026-current, no JS)

```css
@supports (animation-timeline: view()) {
  .fade-in-view { animation: enter linear both; animation-timeline: view();
    animation-range: entry 0% entry 60%; }
  @keyframes enter { from { opacity: 0; transform: translateY(40px); } }
}
```

Great for simple reveals on content sites — reserve GSAP for choreography.

## 11) Kinetic gradient (animated, GPU-cheap)

```css
@property --g1 { syntax: '<percentage>'; initial-value: 20%; inherits: false; }
.kinetic-bg {
  background: radial-gradient(60% 80% at var(--g1) 30%, var(--accent-1) 0%, transparent 60%),
              radial-gradient(50% 60% at 80% 70%, var(--accent-2) 0%, transparent 55%),
              var(--bg);
  animation: drift 14s ease-in-out infinite alternate;
  filter: saturate(1.1);
}
@keyframes drift { to { --g1: 70%; } }
/* add a grain overlay (see asset-creation/references/code-assets.md) to kill banding */
```

## 12) WebGL hero starter (Three.js, performance-safe)

```js
import * as THREE from 'three';

export function initHero(canvas, fragmentShader) {
  const renderer = new THREE.WebGLRenderer({ canvas, antialias: true, alpha: true });
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));   // DPR clamp — always
  const scene = new THREE.Scene();
  const camera = new THREE.OrthographicCamera(-1, 1, 1, -1, 0, 1);
  const uniforms = { uTime: { value: 0 }, uMouse: { value: new THREE.Vector2() },
                     uRes: { value: new THREE.Vector2() } };
  scene.add(new THREE.Mesh(new THREE.PlaneGeometry(2, 2),
    new THREE.ShaderMaterial({ uniforms, fragmentShader })));

  const resize = () => {
    const { clientWidth: w, clientHeight: h } = canvas;
    renderer.setSize(w, h, false); uniforms.uRes.value.set(w, h);
  };
  resize(); addEventListener('resize', resize);
  addEventListener('pointermove', e =>
    uniforms.uMouse.value.set(e.clientX / innerWidth, 1 - e.clientY / innerHeight));

  let raf, running = false;
  const loop = (t) => { uniforms.uTime.value = t / 1000; renderer.render(scene, camera);
                        raf = requestAnimationFrame(loop); };
  new IntersectionObserver(([e]) => {          // pause off-screen — always
    if (e.isIntersecting && !running) { running = true; raf = requestAnimationFrame(loop); }
    else if (!e.isIntersecting && running) { running = false; cancelAnimationFrame(raf); }
  }).observe(canvas);
}
```

A flowing-gradient fragment shader to start from (swap colors for brand tokens):

```glsl
uniform float uTime; uniform vec2 uRes; uniform vec2 uMouse;
// simplex/value noise fn here (any standard 2D noise implementation)
float noise(vec2 p){ return fract(sin(dot(p, vec2(127.1,311.7))) * 43758.5453); }
void main() {
  vec2 uv = gl_FragCoord.xy / uRes;
  float n = noise(uv * 3.0 + uTime * 0.08) * 0.5
          + noise(uv * 6.0 - uTime * 0.05) * 0.25;
  vec3 a = vec3(0.05, 0.05, 0.08);           // bg
  vec3 b = vec3(0.85, 0.35, 0.15);           // accent 1
  vec3 c = vec3(0.20, 0.25, 0.95);           // accent 2
  vec3 col = mix(a, b, smoothstep(0.3, 0.8, n + uMouse.x * 0.15));
  col = mix(col, c, smoothstep(0.6, 0.95, n) * 0.6);
  gl_FragColor = vec4(col, 1.0);
}
```

Rules: DPR clamp ≤ 2, IntersectionObserver pause, lazy-init on idle
(`requestIdleCallback`), static poster fallback for reduced-motion / no-WebGL / low-end mobile.

## 13) Hover image distortion (work cards) — cheap version first

Prefer the CSS version (fast, no WebGL): crossfade + scale + clip.

```css
.card img { transition: transform 0.8s cubic-bezier(0.16,1,0.3,1), filter 0.6s; }
.card:hover img { transform: scale(1.06); filter: saturate(1.15); }
.card .title { transition: letter-spacing 0.5s; }
.card:hover .title { letter-spacing: 0.04em; }
```

Only reach for a WebGL displacement (plane per image + noise-displaced UVs in the fragment
shader, driven by hover progress) if the style skill calls for it AND the page has ≤ 8 such
cards. Reuse one renderer for all cards.

## 14) Choreography defaults (when a style skill doesn't override)

| Token | Value |
|---|---|
| Reveal duration | 0.9–1.2s display text, 0.6–0.8s UI |
| Ease (reveals) | `expo.out` / `cubic-bezier(0.16,1,0.3,1)` |
| Ease (transitions) | `expo.inOut` |
| Stagger | 0.06–0.1s |
| Hover response | ≤ 100ms start, 0.3–0.5s settle |
| Trigger point | `top 85%`, reveal once |
| Max simultaneous animating elements | ~12 (batch beyond that) |
