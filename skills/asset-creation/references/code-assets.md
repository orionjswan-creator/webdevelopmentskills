# Code-producible assets — recipes

Everything here you generate directly, now, without any image model. All output is original,
brand-tokenized, and committed to `assets/`.

## 1. Grain / noise texture (the universal award-site overlay)

Inline SVG — zero network cost, infinitely tileable:

```html
<svg class="grain" aria-hidden="true">
  <filter id="n"><feTurbulence type="fractalNoise" baseFrequency="0.8" numOctaves="3"/></filter>
  <rect width="100%" height="100%" filter="url(#n)"/>
</svg>
```

```css
.grain { position: fixed; inset: 0; z-index: 9998; pointer-events: none;
  opacity: 0.045; mix-blend-mode: overlay; width: 100%; height: 100%; }
```

Tune: `baseFrequency` 0.6–0.9 (finer→coarser), opacity 0.03–0.06. For animated film grain,
swap between 3 pre-rendered `<rect>` frames with a steps() animation — never re-randomize per
frame in JS.

## 2. Gradient mesh backgrounds

Layered radial gradients from brand tokens (see motion-recipes §11 for the kinetic version):

```css
.mesh { background:
  radial-gradient(55% 70% at 20% 25%, color-mix(in oklch, var(--accent-1) 55%, transparent) 0%, transparent 65%),
  radial-gradient(45% 55% at 78% 65%, color-mix(in oklch, var(--accent-2) 45%, transparent) 0%, transparent 60%),
  radial-gradient(70% 90% at 55% 110%, color-mix(in oklch, var(--accent-1) 25%, transparent) 0%, transparent 70%),
  var(--bg); }
```

Always pair with the grain overlay (kills banding). For export-as-asset (email, OG), screenshot
at 2× or render the same stops in an SVG `<radialGradient>`.

## 3. Wordmark / logotype (when no logo exists)

A typographic wordmark in the display font, hand-tuned, beats a generic AI logo:

```html
<svg viewBox="0 0 320 64" role="img" aria-label="BRAND">
  <text x="0" y="48" font-family="var(--font-display)" font-size="48"
        font-weight="640" letter-spacing="-0.03em" fill="currentColor">BRAND</text>
</svg>
```

Then convert text to paths for portability (`fonttools`/Illustrator, or an SVG-text-to-path
lib) so it renders without the webfont. Add ONE distinguishing move: a clipped counter, a
swapped glyph, an accent-colored period, a custom ligature. Provide: full wordmark, monogram
(first letter in a tight square — reused for favicon), and both in light/dark `currentColor`.

## 4. Icon system

Consistency rules — every icon on the same skeleton:

- 24×24 viewBox, 1.5px stroke (or 2px for brutalist styles), `stroke="currentColor"`,
  `fill="none"`, `stroke-linecap` consistent (round OR square, per style skill), 2px padding
  inside the viewBox.
- Build the core set by hand (arrow-right, arrow-up-right, plus, close, menu, chevron-down,
  play, external-link, cart/bag, search — pick what the site needs).
- Ship as a sprite (`<symbol>` + `<use>`) or per-file imports. Don't mix icon libraries; if
  the set grows beyond hand-building, use ONE library restyled to these tokens (Lucide as base,
  adjusted stroke) or Recraft with the exact skeleton spec (see ai-image-tools).

## 5. Favicon pipeline

From the monogram SVG:

```bash
# assets/scripts/favicons.mjs — run: node assets/scripts/favicons.mjs
import sharp from 'sharp';
const src = 'assets/svg/monogram.svg';
for (const s of [16, 32, 180, 192, 512])
  await sharp(src).resize(s, s).png().toFile(`public/icons/icon-${s}.png`);
```

```html
<link rel="icon" href="/favicon.svg" type="image/svg+xml">
<link rel="icon" href="/icons/icon-32.png" sizes="32x32">
<link rel="apple-touch-icon" href="/icons/icon-180.png">
```

SVG favicon supports `prefers-color-scheme` inside it — do the dark variant.

## 6. OG / share image generator

The share card is part of the design (viral mechanics — see trend-report). Generate it from
code so it always matches the brand:

```js
// assets/scripts/og.mjs — SVG template → PNG via sharp. 1200×630.
import sharp from 'sharp';
import { readFileSync } from 'fs';
const svg = readFileSync('assets/svg/og-template.svg', 'utf8')
  .replace('{{TITLE}}', process.argv[2] ?? 'Default title');
await sharp(Buffer.from(svg)).png().toFile('public/og.png');
```

The template: brand background (mesh gradient or dominant color), wordmark, display-font title,
grain. In Next.js prefer `@vercel/og` (satori) for per-page dynamic cards; the SVG template
still defines the design.

## 7. Placeholder generator (run after writing the manifest)

Writes a labeled, brand-colored SVG at every non-final manifest path so the build never blocks:

```js
// assets/scripts/placeholders.mjs — node assets/scripts/placeholders.mjs
import { mkdirSync, writeFileSync, readFileSync } from 'fs';
import { dirname } from 'path';

// manifest lines like: | hero-main | assets/img/hero.avif | 2880×1620 | ... | placeholder |
const rows = readFileSync('assets/manifest.md', 'utf8').split('\n')
  .map(l => l.split('|').map(c => c.trim()))
  .filter(c => c.length > 5 && /^\d+×\d+$/.test(c[3] ?? '') && c.at(-2) !== 'final');

for (const c of rows) {
  const [ , id, path, dims ] = c;
  const [w, h] = dims.split('×').map(Number);
  const svg = `<svg xmlns="http://www.w3.org/2000/svg" width="${w}" height="${h}" viewBox="0 0 ${w} ${h}">
  <rect width="100%" height="100%" fill="#141414"/>
  <rect width="100%" height="100%" fill="none" stroke="#3a3a3a" stroke-width="4" stroke-dasharray="12 12"/>
  <text x="50%" y="48%" text-anchor="middle" fill="#8a8a8a" font-family="monospace"
        font-size="${Math.max(16, w / 40)}">${id}</text>
  <text x="50%" y="56%" text-anchor="middle" fill="#5a5a5a" font-family="monospace"
        font-size="${Math.max(12, w / 60)}">${w}×${h}</text>
</svg>`;
  const out = path.replace(/\.(avif|webp|png|jpg|jpeg)$/, '.svg');
  mkdirSync(dirname(out), { recursive: true });
  writeFileSync(out, svg);
  console.log('placeholder →', out);
}
```

(Site code should reference the final path; during development a helper or the framework's
image fallback points at the `.svg` twin. Swap the fill/stroke to brand tokens.)

## 8. Compression script (for generated images coming back in)

```js
// assets/scripts/compress.mjs — node assets/scripts/compress.mjs <in> <out.avif> [width]
import sharp from 'sharp';
const [ , , input, output, width ] = process.argv;
await sharp(input)
  .resize(width ? { width: +width } : undefined)
  .avif({ quality: 62 })
  .toFile(output);
```

Target ≤ 200KB per image, 2× display size, AVIF first / WebP fallback.

## 9. Decorative extras (pick per style skill)

- **Squircles/blob masks**: CSS `clip-path: shape()` (2026-supported) or an SVG `<clipPath>`.
- **Section dividers**: SVG paths, `preserveAspectRatio="none"`, colored by tokens.
- **Dot/line patterns**: tiny repeating SVG `background-image` data-URIs.
- **Loading spinners**: SVG stroke-dashoffset animations in brand colors — never a GIF.
- **Shader backgrounds**: motion-recipes §12 — token-colored, exported as the hero's
  "code asset" with a static poster render for fallback.
