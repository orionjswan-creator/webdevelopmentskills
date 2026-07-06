# AI asset-generation tools — which to use and how to prompt each (2026)

The gap between models has widened, not narrowed: the winning workflow is **multi-tool** — pick
the model per asset type. Recommend the primary tool in each manifest entry; list the fallback
if the user doesn't have access.

## Tool selection matrix

| Asset type | Primary | Fallback | Why |
|---|---|---|---|
| Hero photography, atmosphere, editorial imagery | **Midjourney (v7)** | FLUX Pro | Best lighting/composition/color polish — closest to pro photography |
| Exact compositions, product mockups, "I need precisely this" | **FLUX (1.1 Pro Ultra / FLUX.2 Pro)** | GPT-image | Best prompt adherence — fewer regenerations to hit a spec |
| Anything containing legible text (posters, packaging, badges) | **Ideogram** | GPT-image | Only model that renders text reliably (~80%+ correct) — but prefer real HTML/SVG text when possible |
| Icons, illustrations, vector graphics | **Recraft (v3)** | code them as SVG | Outputs actual SVG that scales and takes CSS styling — design-system ready |
| Quick iterations, edits of existing images, inpainting | **GPT-image (ChatGPT)** | FLUX | Conversational refinement; good instruction following |
| Seamless textures, materials | FLUX or Midjourney with `--tile` | — | MJ's tile param makes true repeats |
| 3D models (glTF for Three.js) | **Meshy** or **Tripo** | commission | Text/image → usable glTF; budget cleanup time for hero objects |
| Video loops, hero background motion | **Runway / Sora / Veo** | CSS/WebGL instead | Only when the style skill calls for video; always compress + poster frame |
| Voice / ambient audio | **ElevenLabs** | skip | Rarely needed; must be user-initiated (autoplay audio is banned) |

Free-tier route if the user has no subscriptions: FLUX (schnell/dev) via fal.ai/Replicate
pay-per-image, Recraft free tier for vectors, Ideogram free tier for text images.

## The universal prompt spec (write this into every manifest entry)

```md
**Tool**: Midjourney v7  (fallback: FLUX Pro)
**Prompt**: <medium> of <subject>, <composition>, <lighting>, <palette as color names>,
<mood adjectives>, <art-direction constants>
**Exclude / negative**: text, watermark, logo, <art-direction exclusions>
**Aspect**: 16:9   **Target size**: 2880×1620 (2× display)   **Save to**: assets/img/hero.avif
```

Rules that make prompts hit first-try:

1. **Lead with the medium** ("35mm editorial photograph of…", "matte clay 3D render of…",
   "flat vector illustration of…") — it sets the whole distribution.
2. **Inherit the art-direction block** — same medium/lighting/palette/mood phrases in every
   prompt on the manifest. Consistency is what separates "designed" from "AI collage."
3. **Name colors, not hex** ("deep forest green and warm cream" — models don't read hex).
4. **One subject per image.** Composite in code (layout, overlays, text), not in the model.
5. **Specify negative space** where the design needs it ("large empty area upper right for
   headline overlay").
6. **Always exclude text** unless using Ideogram deliberately.

## Per-tool syntax notes

- **Midjourney**: append params — `--ar 16:9 --style raw` (raw = less MJ-flavored, better for
  brand work); `--sref <url>` to lock style across a batch (generate one anchor image first,
  then sref it everywhere); `--tile` for textures; `--no text, watermark` for negatives.
- **FLUX**: no param syntax — write long, literal natural language; state composition
  explicitly ("centered, shot from slightly below, 85mm lens look"). It follows instructions,
  so write instructions.
- **Ideogram**: put the exact text to render in double quotes inside the prompt; choose the
  Design style for graphic layouts; keep quoted text short (≤ 6 words render best).
- **Recraft**: select vector/SVG output mode; specify stroke weight and corner style to match
  the site's icon system ("2px rounded strokes, geometric, single color"); request each icon on
  the same grid for set consistency.
- **GPT-image**: iterate conversationally ("same image but wider negative space left"); good at
  respecting layout instructions; use for surgical edits of accepted images.

## Consistency workflow for a full site (do this, in order)

1. Generate the **hero image first** — it's the art-direction anchor. Iterate until it matches
   DIRECTION.md exactly.
2. Lock style: MJ `--sref` the approved hero (or reuse the exact prompt scaffold in FLUX) for
   all remaining images.
3. Batch-generate section images with only the `<subject>` clause changing.
4. Post-process uniformly: same crop ratios (from the manifest), one pass of the compression
   script (`sharp` → AVIF/WebP, quality ~62, ≤ 200KB each), optional unified grain overlay in
   code (which also masks minor style drift between images).
5. Drop files at manifest paths — placeholders are replaced, site updates with zero code change.

## Licensing note (put in the manifest handoff)

Commercial-use terms differ: Midjourney requires a paid plan for commercial rights; check the
current terms of whichever tool generates final assets. Never present generated people as real
team members/customers — use `role: illustrative` in the manifest for any generated humans, and
prefer real photos for team/testimonial slots (`status: awaiting-user`).
