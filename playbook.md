# The AI Image Bible

**Current to April 25, 2026. Every prompt pattern, every payload, every decision for the three flagship image models: OpenAI gpt-image-2, Midjourney V8.1, and Google Gemini 3 Pro Image (Nano Banana Pro).**

---

## Who this is for

Anyone generating images with AI in 2026. Solo creators, agency teams, product designers, marketers, engineers shipping image-generation features in production SaaS. Equally applicable whether you generate one image a week or one hundred thousand a month.

This is a bible, not a quick guide. Eight parts. Dense. The three flagship models have fundamentally different prompt grammars, payload shapes, pricing, and strengths; using one's patterns on another produces mediocre output in every direction. This reference covers all three properly, plus the production techniques (interleaved payloads, character consistency, brand palette locking) that apply across all three.

Paired with a companion GitHub repository (`AI-BrandFactory/ai-image-bible`) that ships organized prompt templates, payload structures, and Python reference implementations for each model.

---

## What is in this Bible

- **Part 1**, The 2026 Model Landscape
- **Part 2**, Prompting Fundamentals Across All Models
- **Part 3**, Gemini 3 Pro Image / Nano Banana Pro Full Breakdown
- **Part 4**, Midjourney V8.1 Full Breakdown
- **Part 5**, OpenAI gpt-image-2 Full Breakdown
- **Part 6**, Character Consistency Across Models
- **Part 7**, Production Workflows
- **Part 8**, Validation and the 8 Common Mistakes

---

## Part 1, The 2026 Model Landscape

As of April 25, 2026, three image models lead by a meaningful margin.

### The three flagships

**OpenAI gpt-image-2**, released April 21, 2026. Replaces gpt-image-1 and the interim gpt-image-1.5. Replaces DALL-E 3 entirely (DALL-E 2 and 3 retire May 12, 2026). Launched at #1 on LM Arena Image with a +242-point Elo lead, the largest in the arena's history. Key strengths: near-perfect multilingual text rendering, native reasoning (Thinking Mode) for composition planning, up to 10-image batch consistency, multi-turn editing via the Responses API.

**Midjourney V8.1 Alpha**, released April 14, 2026. Refines V8 (March 17, 2026) with a more V7-inspired aesthetic, stable moodboards, restored image prompts, and a Prompt Shortener. Native 2K (2048x2048) output, sub-10-second generation, 95 percent accuracy on complex multi-subject prompts. Key strengths: best-in-class aesthetic quality for editorial and artistic work, improved text rendering, Omni Reference (`--oref`) for character consistency, V1 Video for 5-to-20-second animation.

**Google Gemini 3 Pro Image (Nano Banana Pro)**, model ID `gemini-3-pro-image-preview`. The flagship Google image model as of April 2026. Native 1K/2K/4K output, multilingual text rendering that often beats even gpt-image-2 on long in-image text, character consistency across up to 5 characters and up to 14 reference images, Google Search grounding for factual visuals. The Nano Banana 2 Flash variant (`gemini-3.1-flash-image-preview`) offers Pro-class features at faster speed and lower cost.

![Gemini 3 Pro Image cinematic portrait demonstrating atmospheric lighting and realistic skin rendering](embedded-visuals-optimized/deepmind-gemini-image-pro-01.jpg "Gemini 3 Pro Image. Source: deepmind.google/models/gemini-image/pro/")

![Nano Banana Pro live-radar weather infographic showing in-image text rendering for Dallas Texas at 79F cloudy, pop-art comic style](embedded-visuals-optimized/google-nano-banana-pro-02.jpg "Nano Banana Pro text rendering. Source: blog.google/technology/ai/nano-banana-pro/")

### The rest of the landscape

Models that are still relevant but not flagship:

- **Imagen 4 family** (Google, pure diffusion): Fast, Standard, Ultra variants. Ultra still beats Nano Banana Pro on pure photorealism (product shots, realistic portraits). Scheduled shutdown June 24, 2026; budget a migration.
- **Flux 1.1 Pro / Flux 2** (Black Forest Labs): API-driven, fastest technical generation (~4.5s), widely used in production pipelines. Open-weight Schnell variant runs locally.
- **Stable Diffusion 3.5** (Stability): complete control, local execution, zero recurring cost. Required when privacy or fine-tuning matter.
- **Ideogram 3, Recraft V4, Seedream, Reve AI**: specialized competitors with narrow wins (typography, vector output, specific aesthetics).

These are covered briefly in Part 7 under production alternatives.

### The capabilities matrix (April 2026)

| Capability | gpt-image-2 | Midjourney V8.1 | Gemini 3 Pro Image |
|---|---|---|---|
| Max native resolution | 2K (2000px) | 2K (2048x2048) | 4K |
| Aspect ratio range | 3:1 to 1:3 | Any, via `--ar` | 1:8 to 8:1 |
| Text-in-image accuracy | Near-100% Latin, strong multilingual | Improved V8, good for 1-3 word labels | Best-in-class, long multilingual passages |
| Character consistency | 10-image batch, same character | `--oref` single-image reference | Up to 5 characters, 14 references |
| Multi-turn editing | Yes (Responses API) | Yes (Editor) | Yes (conversational API) |
| Native reasoning | Yes (Thinking Mode) | No | Yes (Thinking) |
| Real-world grounding | Knowledge cutoff Dec 2025 | None | Google Search as tool |
| API access | Full | No public API | Full |
| Video generation | No | V1 Video, 5-20 sec | No |
| Best-in-class for | Text-heavy, UI mocks, multi-image sets | Editorial, artistic, cinematic | Infographics, 4K, multi-character scenes |
| Per-image cost (standard) | ~\$0.21 | \$10-\$120/mo plans | \$0.067-\$0.24 |
| Access model | API | Web/Discord, no API | API, Vertex AI |

### The decision framework

Three questions pick the model:

1. **Do I need in-image text?** Long paragraphs, multilingual, or fine-typography overlays: Gemini 3 Pro Image. Short headlines and labels: gpt-image-2 or Gemini both work. Artistic text integration (stylized signage in a scene): Midjourney V8.1.
2. **Do I need programmatic API access?** Yes: gpt-image-2 or Gemini 3. No: Midjourney V8.1 wins on aesthetic quality.
3. **What's the dominant use case?**
   - Editorial or artistic hero images: Midjourney V8.1
   - Product mockups, UI mocks, slide content, infographics: gpt-image-2 or Gemini
   - High-volume production at the lowest cost: Gemini Nano Banana 2 Flash or Imagen 4 Fast
   - Multi-character scenes with consistency: Gemini 3 Pro Image
   - Text-heavy marketing assets with precise intent: gpt-image-2

Most professional pipelines in 2026 run two or three of these in parallel, picking the right model per task.

![Midjourney V8 Alpha showcase collage, 8 outputs across styles: angelic figure in green light, cat on crescent moon, witch portrait, cloaked triangular figures, desert warrior, neon cyberpunk city, fantasy adventuring party, ghost rider silhouette](embedded-visuals-optimized/midjourney-v8-alpha-01.jpg "Midjourney V8 Alpha showcase. Source: updates.midjourney.com/v8-alpha/")

---

## Part 2, Prompting Fundamentals Across All Models

Before the model-specific deep dives, some patterns that apply everywhere.

### The universal prompt elements

Every effective AI image prompt, across every model, has the same 7 conceptual elements. What differs is how each model weights them and how you express them.

1. **Subject**: who or what is in the image. Always be specific ("a 30-something analyst in a charcoal blazer" beats "a person"). Specific subjects beat generic ones in every model.
2. **Action or pose**: what the subject is doing or how they are posed. "Examining a tablet" is more specific than "standing there."
3. **Environment / setting**: where the scene takes place. Include lighting cues if the environment is implicit (office vs sunset beach).
4. **Style / medium**: photorealistic, editorial photograph, oil painting, 3D render, vector illustration, infographic, manga. The medium sets the rendering approach.
5. **Lighting**: soft natural, dramatic studio, golden hour, overhead fluorescent, candlelight. Explicit lighting is the single biggest quality lift across models.
6. **Composition / framing**: close-up, wide shot, rule of thirds, negative space, eye-level, overhead. These govern where the subject lands in the frame.
7. **Technical quality**: 35mm lens, 85mm f/1.8, shallow depth of field, 4K, sharp focus. These push the model toward production-quality output.

### What the 3 models do differently with the same 7 elements

- **gpt-image-2** wants them in verbose prose, in order from scene to subject to details to intended use. Structured English. Responds strongly to "intended use" being declared (ad, UI mock, infographic, etc).
- **Midjourney V8.1** wants them compressed and evocative, with parameter flags for technical quality (`--ar 16:9 --stylize 150 --style raw`). Early words carry more weight.
- **Gemini 3 Pro Image** tolerates both styles but performs best with clear delimiters (JSON structure for complex briefs) and explicit "do not render this as text" guards.

### Word order matters more than word count

Across all three models, early words have more semantic weight. The first 10 words of a prompt influence the image more than the last 100. Lead with the subject, not the style. Lead with the specific, not the generic.

Bad: "A beautiful, cinematic, dramatic image featuring a person..."
Good: "A 30-something analyst in a charcoal blazer, examining a tablet, cinematic editorial lighting..."

### Negative prompts and constraints

Stating what you do NOT want is useful in all three models, but expressed differently.

- **gpt-image-2**: state constraints in plain language in the prompt: "Do not render additional text. No watermark. Avoid uncanny valley."
- **Midjourney V8.1**: use `--no` parameter: `--no watermark, text, logos, extra limbs`
- **Gemini 3 Pro Image**: include a constraints block in the prompt, use the "do not render these instructions as text" guard at the start of JSON-structured prompts.

### The text-rendering rule

When you need specific text rendered in an image:

1. Always wrap the text in quotes in the prompt: "Render the headline 'LAUNCH 2026' at the top."
2. Keep it short. Under 30 characters for headlines, under 100 characters for longer text blocks.
3. Specify font family as a description, not an instruction name: "clean sans-serif" not "Inter Bold."
4. Name the exact position: "top-left corner" not "somewhere on the image."
5. For any text that must exactly match, add a verification step in your pipeline (OCR check) and regenerate on mismatch.

gpt-image-2 and Gemini 3 Pro Image both render text accurately enough for production in 2026. Midjourney V8 improved significantly on text; V7 and earlier were unreliable.

### The "specific synonym" rule

Specific synonyms beat generic descriptors across all models:

- "Flock of birds" beats "birds"
- "Gigantic" beats "big"
- "Weathered oak desk" beats "old wooden desk"
- "Golden hour light" beats "warm light"
- "Rembrandt lighting" beats "dramatic lighting"

Specific words activate the model's richer training data for that concept. Generic words land in the middle of a wide semantic distribution.

---

<!-- abf-plug -->
> The rest of the AI BrandFactory library builds on patterns like this. See the full set at [aibrandfactory.com](https://www.aibrandfactory.com).


## Part 3, Gemini 3 Pro Image / Nano Banana Pro Full Breakdown

Flagship model: `gemini-3-pro-image-preview`. Alias: Nano Banana Pro. This is the most feature-complete of the three flagships for most production use cases in April 2026.

![Gemini 3 Pro Image atmospheric landscape with silhouetted figure in golden hour mist, lens flare, photorealistic](embedded-visuals-optimized/deepmind-gemini-image-pro-03.jpg "Gemini 3 Pro Image sample. Source: deepmind.google/models/gemini-image/pro/")

### API endpoint

```
POST https://generativelanguage.googleapis.com/v1beta/models/gemini-3-pro-image-preview:generateContent
```

Required headers:

```
x-goog-api-key: <YOUR_KEY>
Content-Type: application/json
```

### Case convention

The REST payload uses `snake_case` (`inline_data`, `mime_type`, `response_modalities`). Official SDKs in Python and JavaScript expose them as `camelCase` (`inlineData`, `mimeType`, `responseModalities`) and serialize internally.

Both are valid in the raw REST payload, but snake_case is the documented form. Use snake_case in direct curl / fetch calls; use camelCase in SDK code.

### Complete example request

```json
{
  "contents": [
    {
      "role": "user",
      "parts": [
        { "inline_data": { "mime_type": "image/png", "data": "<BASE64_CHARACTER_REFERENCE>" } },
        { "text": "Reference: main character, front-facing, neutral expression, 3/4 body." },
        { "inline_data": { "mime_type": "image/jpeg", "data": "<BASE64_SCENE_REFERENCE>" } },
        { "text": "Reference: rooftop bar setting, evening, warm string lights." },
        { "text": "Generate: place the character in the rooftop bar at golden hour, seated at the counter, 85mm portrait lens, shallow depth of field, cinematic warm grade. Render the headline 'CITY NIGHTS' integrated into the skyline architecture. 2K, 16:9." }
      ]
    }
  ],
  "tools": [ { "google_search": {} } ],
  "generationConfig": {
    "response_modalities": ["TEXT", "IMAGE"],
    "image_config": {
      "aspect_ratio": "16:9",
      "image_size": "2K"
    }
  },
  "safetySettings": [
    { "category": "HARM_CATEGORY_HARASSMENT", "threshold": "BLOCK_MEDIUM_AND_ABOVE" },
    { "category": "HARM_CATEGORY_HATE_SPEECH", "threshold": "BLOCK_MEDIUM_AND_ABOVE" },
    { "category": "HARM_CATEGORY_SEXUALLY_EXPLICIT", "threshold": "BLOCK_MEDIUM_AND_ABOVE" },
    { "category": "HARM_CATEGORY_DANGEROUS_CONTENT", "threshold": "BLOCK_MEDIUM_AND_ABOVE" }
  ]
}
```

### Supported aspect ratios

`1:1`, `2:3`, `3:2`, `3:4`, `4:3`, `4:5`, `5:4`, `9:16`, `16:9`, `21:9`, plus extreme bars `1:4`, `4:1`, `1:8`, `8:1`. All have been verified to reliably produce output at the requested ratio.

### Supported sizes

`512`, `1K`, `2K`, `4K`. Known bug: the Node SDK has been observed to silently ignore `image_size: "2K"` and return 1K in some preview-tier requests (open issue on discuss.ai.google.dev). Verify output dimensions in production; add a size check and retry if the model returns a smaller image than requested.

### JSON prompting for complex briefs

For prompts with many constraints (product campaigns, ad variants, multi-element infographics), JSON-structured prompts raise accuracy 60 to 80 percent on multi-constraint tasks compared to free-form English.

```json
{
  "task": "generate_image",
  "subject": {
    "type": "portrait",
    "gender": "female",
    "age_range": "30-35",
    "ethnicity": "south asian",
    "distinguishing_features": "dark wavy shoulder-length hair, confident smile"
  },
  "style": {
    "medium": "editorial photograph",
    "lighting": {
      "setup": "rembrandt three-point",
      "color_temperature_k": 3200,
      "intensity": 0.85
    },
    "lens": "85mm f/1.4",
    "color_grade": "teal and orange"
  },
  "composition": {
    "framing": "waist-up",
    "rule_of_thirds": true,
    "negative_space_direction": "right",
    "background": "soft-focus modern office"
  },
  "text_overlay": {
    "content": "LAUNCH 2026",
    "font_family_description": "clean bold sans-serif",
    "placement": "bottom-right",
    "size": "medium",
    "color": "off-white"
  },
  "output": {
    "aspect_ratio": "3:2",
    "resolution": "4K",
    "format": "image/png"
  },
  "constraints": [
    "do not render any of these JSON fields as visible text",
    "no watermarks",
    "no additional text beyond the text_overlay content"
  ]
}
```

Send this inside a single `text` part of the `parts` array. The model parses the JSON and constructs the image to match.

### Reference image strategy

Up to 14 reference images per request. Best practices proven across 280+ production tests:

1. **Identity anchor (characters)**: send 2 to 3 photos of the same person from different angles. Front-facing, 3/4 profile, side profile. All evenly lit.
2. **Style anchor**: send 1 reference image for the visual aesthetic (color palette, composition style, rendering mood).
3. **Logo or brand mark**: send 1 reference of the logo at high resolution.
4. **Product shots**: send 1 reference per product from a neutral angle.
5. **Scene / environment**: 1 reference of the location or background.

Maximum: 14 total references. Practical max for most use cases: 6 to 8. Beyond 8, the model has trouble weighting which reference matters most for which part of the output.

### The interleaved payload pattern

Send parts in `[Image][Context][Image][Context][...][Main Prompt]` order, not all images followed by all text. The model binds each reference to its labeled role before the final instruction fires.

```json
"parts": [
  { "inline_data": { "mime_type": "image/png", "data": "<CHAR_A_FRONT>" } },
  { "text": "CHARACTER A, front-facing, neutral expression." },
  { "inline_data": { "mime_type": "image/png", "data": "<CHAR_A_PROFILE>" } },
  { "text": "CHARACTER A, 3/4 profile." },
  { "inline_data": { "mime_type": "image/png", "data": "<CHAR_B_FRONT>" } },
  { "text": "CHARACTER B, front-facing." },
  { "inline_data": { "mime_type": "image/jpeg", "data": "<SCENE_REF>" } },
  { "text": "SCENE: rooftop bar, dusk." },
  { "text": "Generate: Characters A and B seated at the rooftop bar from SCENE, talking. Keep A's and B's facial features exactly as in the references. 2K, 16:9." }
]
```

This pattern is the single biggest character-consistency upgrade on Gemini 3. Without it, character faces drift by generation 3 or 4. With it, faces remain identical across 50+ generations.

### Multi-turn editing

Gemini 3 supports conversational refinement:

- Turn 1: full reference images + detailed prompt
- Turn 2: "Using the previous image, change [element] to [new]. Keep the person's face and features IDENTICAL."
- Turn 3: "Refine lighting to [detail]. Preserve everything else."

Quality degrades after 3 to 4 sequential edits; faces start to drift. For longer edit chains, regenerate from the original references instead of chaining.

### Google Search grounding

Add `tools: [{ "google_search": {} }]` to the request. Gemini will call Google Search to verify factual elements before rendering. Use cases:

- Infographic showing current weather data
- Map with current events location markers
- Product comparison image pulling current pricing
- Recipe card with current ingredient availability

The grounded data appears correctly in the rendered image. Without grounding, Gemini falls back to training-data knowledge (cutoff varies by model).

### Pricing (April 2026)

| Tier | 1K | 2K | 4K |
|------|-----|-----|-----|
| Gemini 3 Pro Image (standard) | \$0.134 | \$0.134 | \$0.24 |
| Gemini 3 Pro Image (batch / flex, ~50% off) | \$0.067 | \$0.067 | \$0.12 |
| Nano Banana 2 Flash | Lower than Pro; exact pricing varies | | |
| Imagen 4 Fast | \$0.02 | | |
| Imagen 4 Standard | \$0.04 | | |
| Imagen 4 Ultra | \$0.06 | | |

At \$0.134 per 2K image on standard tier, Gemini 3 Pro Image is the cost leader among the flagship three for most quality tiers. Imagen 4 Fast is the cheapest option for drafts and thumbnails.

### Known limitations of Gemini 3 Pro Image

- Faces drift after 3 to 4 sequential edits in multi-turn
- Pushes surreal prompts toward photorealism unless explicitly overridden
- Complex text at small point sizes still breaks; long paragraphs and extreme multilingual mixing degrade
- Day-to-night lighting transforms and multi-angle camera consistency still weak
- Inputs over 7MB are auto-compressed
- SynthID watermarks (visible and invisible) on all outputs; rules out some commercial uses
- Imagen 4 Ultra still beats it for pure photorealism

### Gemini 3 Pro Image showcase

A curated set of official Gemini 3 Pro Image outputs. Note the range: photorealistic portraits, stylized illustration, infographic typography, atmospheric landscapes.

![Gemini 3 Pro Image portrait study 1](embedded-visuals-optimized/deepmind-gemini-image-pro-02.jpg "Gemini 3 Pro Image. Source: deepmind.google/models/gemini-image/pro/")

![Gemini 3 Pro Image portrait study 2](embedded-visuals-optimized/deepmind-gemini-image-pro-04.jpg "Gemini 3 Pro Image. Source: deepmind.google/models/gemini-image/pro/")

![Gemini 3 Pro Image prism refraction infographic demonstrating technical illustration with multi-step labels](embedded-visuals-optimized/deepmind-gemini-image-pro-05.jpg "Gemini 3 Pro Image infographic. Source: deepmind.google/models/gemini-image/pro/")

![Gemini 3 Pro Image portrait study 3](embedded-visuals-optimized/deepmind-gemini-image-pro-06.jpg "Gemini 3 Pro Image. Source: deepmind.google/models/gemini-image/pro/")

![Gemini 3 Pro Image landscape study](embedded-visuals-optimized/deepmind-gemini-image-pro-07.jpg "Gemini 3 Pro Image. Source: deepmind.google/models/gemini-image/pro/")

![Gemini 3 Pro Image extended study](embedded-visuals-optimized/deepmind-gemini-image-pro-08.jpg "Gemini 3 Pro Image. Source: deepmind.google/models/gemini-image/pro/")

### Nano Banana Pro showcase

Flagship outputs from the Nano Banana Pro launch. Text rendering, typography integration, and subject consistency across scenes are all on display.

![Nano Banana Pro character portrait](embedded-visuals-optimized/google-nano-banana-pro-01.jpg "Nano Banana Pro. Source: blog.google/technology/ai/nano-banana-pro/")

![Nano Banana Pro sample scene](embedded-visuals-optimized/google-nano-banana-pro-03.jpg "Nano Banana Pro. Source: blog.google/technology/ai/nano-banana-pro/")

![Nano Banana Pro BERLIN typography integrated into building facades, demonstrating in-image text at massive scale with natural lighting](embedded-visuals-optimized/google-nano-banana-pro-04.jpg "Nano Banana Pro typography. Source: blog.google/technology/ai/nano-banana-pro/")

![Nano Banana Pro additional sample](embedded-visuals-optimized/google-nano-banana-pro-05.jpg "Nano Banana Pro. Source: blog.google/technology/ai/nano-banana-pro/")

![Nano Banana Pro scene composition](embedded-visuals-optimized/google-nano-banana-pro-06.jpg "Nano Banana Pro. Source: blog.google/technology/ai/nano-banana-pro/")

![Nano Banana Pro TYPOGRAPHY demo, stylized halftone duotone lettering showcasing text as primary subject](embedded-visuals-optimized/google-nano-banana-pro-07.jpg "Nano Banana Pro typography. Source: blog.google/technology/ai/nano-banana-pro/")

![Nano Banana Pro additional composition](embedded-visuals-optimized/google-nano-banana-pro-08.jpg "Nano Banana Pro. Source: blog.google/technology/ai/nano-banana-pro/")

### Nano Banana 2 (Flash tier) showcase

Nano Banana 2 is the Flash variant, delivering Pro-class output at faster speed and lower cost.

![Nano Banana 2 TPU chip product shot with bokeh lighting](embedded-visuals-optimized/google-nano-banana-2-01.jpg "Nano Banana 2 (Flash). Source: blog.google/innovation-and-ai/technology/ai/nano-banana-2/")

![Nano Banana 2 sample](embedded-visuals-optimized/google-nano-banana-2-02.jpg "Nano Banana 2 (Flash). Source: blog.google/innovation-and-ai/technology/ai/nano-banana-2/")

![Nano Banana 2 additional sample](embedded-visuals-optimized/google-nano-banana-2-03.jpg "Nano Banana 2 (Flash). Source: blog.google/innovation-and-ai/technology/ai/nano-banana-2/")

### Nano Banana launch examples (precursor)

From the original Nano Banana launch gallery, showing the range that preceded the Pro release.

![Nano Banana launch example 1](embedded-visuals-optimized/google-nano-banana-examples-01.jpg "Nano Banana (launch). Source: blog.google/products/gemini/gemini-nano-banana-examples/")

![Nano Banana launch example 2](embedded-visuals-optimized/google-nano-banana-examples-02.jpg "Nano Banana (launch). Source: blog.google/products/gemini/gemini-nano-banana-examples/")

![Nano Banana launch example 3](embedded-visuals-optimized/google-nano-banana-examples-03.jpg "Nano Banana (launch). Source: blog.google/products/gemini/gemini-nano-banana-examples/")

---

## Part 4, Midjourney V8.1 Full Breakdown

Released April 14, 2026 as Alpha, on alpha.midjourney.com. Web-only (not in Discord during alpha). Refines V8 (March 17, 2026) with more V7-inspired aesthetic, stable moodboards, restored image prompts, Prompt Shortener.

![Midjourney V8 Alpha showcase collage, 8 diverse outputs spanning angelic figures, cat on a crescent moon, witch portrait, cloaked figures, desert warrior, cyberpunk city, fantasy group, and ghost rider](embedded-visuals-optimized/midjourney-v8-alpha-01.jpg "Midjourney V8 Alpha showcase. Source: updates.midjourney.com/v8-alpha/")

### How to access

- alpha.midjourney.com (web, V8 and V8.1)
- discord.com (Discord, V7 and earlier still work there)
- No public API; use Midjourney directly

Paid plans only; no free tier.

### Parameter reference (comprehensive)

| Parameter | Syntax | Effect |
|---|---|---|
| `--ar` | `--ar 16:9` | Aspect ratio. Any ratio from 1:4 to 4:1 |
| `--s` / `--stylize` | `--s 100` | Creative freedom, 0 to 1000, default 100 |
| `--p` | `--p` or `--p pID` | Apply personalization profile |
| `--style raw` | `--style raw` | Reduces Midjourney's default artistic bias, more literal output |
| `--oref` | `--oref URL` | Omni Reference (V7/V8). Character or object consistency |
| `--ow` | `--ow 0-1000` | Omni weight (default 100). `--ow 25` for loose style transfer, `--ow 400+` for strict face preservation |
| `--cref` | `--cref URL` | Character reference (legacy V6). Superseded by `--oref` on V7/V8 |
| `--cw` | `--cw 0-100` | Character weight (legacy) |
| `--sref` | `--sref URL` or `--sref 12345678` | Style reference (image URL or style code from Style Explorer) |
| `--sw` | `--sw 0-1000` | Style weight |
| `--weird` / `--w` | `--w 250` | 0 to 3000, adds quirky variations |
| `--chaos` / `--c` | `--c 25` | 0 to 100, variety between the 4 grid outputs |
| `--niji` | `--niji 7` | Niji 7 anime model |
| `--v` | `--v 8.1` | Model version selector |
| `--stop` | `--stop 50` | Halt at 10 to 100 percent progress |
| `--seed` | `--seed 12345` | 0 to 4,294,967,295; reproducibility |
| `--tile` | `--tile` | Tile-pattern output for repeating textures |
| `--no` | `--no trees, cars, people` | Negative prompt; comma-separated |
| `--q` | `--q 4` | Quality; V8 supports `--q 4` for extra coherence |
| `--hd` | `--hd` | NEW in V8: native 2K rendering, 3x faster/cheaper in V8.1 |
| `--exp` | `--exp 10` | Experimental aesthetic boost |

Mode toggles (UI-level, not prompt parameters):
- **Fast Mode**: paid GPU time, highest priority queue
- **Turbo Mode**: 2x fast cost, fastest priority
- **Relax Mode**: unlimited (on Standard+ plans), slower queue
- **Draft Mode**: removed in V8 (was in V7; cheap/fast low-quality)

Video-specific (V1 Video):
- `--motion low` (default) or `--motion high`
- `--raw` reduces stylization in video
- Most image parameters are stripped automatically when animating

### Prompt structure that works

V7/V8 prefer natural language over keyword lists. Proven formula:

```
Subject + Medium + Environment + Lighting + Mood + Composition --ar --s --style
```

Example:

```
A 30-something analyst in a charcoal blazer examining a tablet, editorial photograph,
modern office with morning light, soft three-point lighting, shallow depth of field,
waist-up framing with negative space right --ar 3:2 --s 150 --style raw
```

Best practices:

1. **Lead with the subject**, not the style. Early words carry more weight.
2. **Use specific synonyms**. "Weathered oak desk" beats "old wooden desk". "Gigantic" beats "big".
3. **Put text to render in "quotes"**. V8 reads this as explicit typography intent.
4. **Declare the medium explicitly**: "editorial photograph", "oil painting", "3D render", "vector illustration".
5. **Add lighting as its own phrase**. Single biggest quality lift.
6. **Include a lens spec for photographs**: "85mm portrait", "35mm wide", "f/1.8 aperture".

What to avoid:

- Keyword soup ("beautiful, stunning, epic, masterpiece, hyperrealistic, 8K, octane render, etc")
- Conflicting styles ("photorealistic oil painting anime")
- Vague modifiers ("really good", "amazing", "wow")
- More than 50 words of prompt without parameter flags; dilutes the semantic signal

### Omni Reference in detail

`--oref URL --ow [weight]` is the 2026 character consistency tool. Replaces `--cref` on V7/V8.

Rules:

- Only ONE image allowed per `--oref`. Multiple references require multiple runs or Style Reference for the style anchor.
- `--ow 25` for loose style transfer (e.g., photo reference into anime)
- `--ow 100` (default) for balanced reference use
- `--ow 400` to preserve faces, clothing, specific details strictly
- Competes with `--stylize` and `--exp`; if either is high, raise `--ow` to compensate

Example with Omni Reference + Style Reference together:

```
A 40-year-old woman in a navy suit delivering a keynote, editorial photograph,
conference stage with soft blue wash --oref https://cdn.example.com/headshot.jpg --ow 300
--sref 1234567890 --ar 3:2 --style raw
```

Here `--oref` locks the face and general appearance; `--sref` applies the aesthetic from style code 1234567890; prompt text describes the scene and composition.

### Style Reference in detail

`--sref URL` or `--sref 12345678`

- URL-based: send an external image URL; Midjourney uses it as the style anchor
- Code-based: use Midjourney's Style Explorer to find a code; reference by number
- Multiple: `--sref URL1 URL2` to blend aesthetics
- Weight: `--sw 0-1000` controls how strongly the style transfers (default 100)

Style Reference does NOT preserve subject content; it only transfers aesthetic, palette, texture, mood. For subject content use Omni Reference.

### Pricing (April 2026)

| Plan | Monthly | Annual | GPU Hours (Fast) | Key Features |
|---|---|---|---|---|
| Basic | \$10 | \$8/mo | 3.3 | Limited fast jobs, no Relax |
| Standard | \$30 | \$24/mo | 15 | Unlimited Relax |
| Pro | \$60 | \$48/mo | 30 | + Stealth mode, 12 concurrent |
| Mega | \$120 | \$96/mo | 60 | Max concurrency, priority |

Annual plans receive approximately 20 percent discount versus monthly. Commercial use for companies with over \$1M annual revenue requires Pro or Mega tier.

### Known limitations

- No public API (blocks automation in product pipelines)
- V8 Alpha is web-only on alpha.midjourney.com
- V8 dropped Draft Mode (users lost the cheap iteration path)
- V8 Alpha only runs in Fast mode (no Relax available yet)
- Hands are still imperfect, especially in complex gesture / interaction poses
- Video "melting": fine details warp during V1 animation
- Creative flatness: some users report V8 interprets prompts too literally versus V7's artistic flair
- Real people: Omni Reference does not match exact likeness (by design)
- Commercial use on Basic requires under \$1M company revenue

### When to use Midjourney V8.1 over alternatives

- Scroll-stopping social and ad imagery where aesthetic wins over precision
- Brand hero photography with cinematic mood
- Artistic concept work, illustration, surreal imagery
- Editorial magazine-style shots
- Anything where the image is the deliverable itself (not a pipeline ingredient)

Not the right tool when: you need API access, you need precise text rendering for production ads (gpt-image-2 wins), you need multi-character consistency (Gemini 3 wins), you need high-volume automated generation (Flux or Imagen wins on throughput and cost).

### Midjourney V8.1 Alpha showcase

![Midjourney V8.1 Alpha sample output demonstrating the refined V7-aesthetic direction](embedded-visuals-optimized/midjourney-v8-1-alpha-01.jpg "Midjourney V8.1 Alpha. Source: updates.midjourney.com/v8-1-alpha/")

---

## Part 5, OpenAI gpt-image-2 Full Breakdown

Released April 21, 2026. Launched at #1 on LM Arena Image. Replaces gpt-image-1 and DALL-E 3 entirely. DALL-E 2 and 3 retire May 12, 2026.

![OpenAI GPT Image 2 developer documentation banner](embedded-visuals-optimized/openai-model-doc-01.jpg "OpenAI gpt-image-2 model documentation. Source: developers.openai.com/api/docs/models/gpt-image-2")

### API endpoint

```
POST https://api.openai.com/v1/images/generations
```

Also available via Responses API for conversational editing:

```
POST https://api.openai.com/v1/responses
```

Required headers:

```
Authorization: Bearer <OPENAI_API_KEY>
Content-Type: application/json
```

### Core parameters

| Parameter | Values | Notes |
|---|---|---|
| `model` | `"gpt-image-2"` | Single model ID |
| `prompt` | string | See prompt patterns below |
| `size` | `"1024x1024"`, `"1536x1024"`, `"1024x1536"`, or custom WxH | 655,360 to 8,294,400 total pixels, aspect ratio within 3:1 |
| `quality` | `"auto" \| "low" \| "medium" \| "high"` | Quality tier |
| `n` | 1 to 10 | Number of images per request. 10-image batch preserves character across the set |
| `output_format` | `"png" \| "jpeg" \| "webp"` | Default png |
| `output_compression` | 0-100 | For jpeg / webp only |
| `background` | `"auto" \| "opaque"` | Transparent NOT supported on gpt-image-2 at launch |
| `stream` | boolean | Enables partial-image streaming |
| `partial_images` | integer | Number of intermediate frames pushed before final |
| `moderation` | `"auto" \| "low"` | Content moderation strictness |

Note: `response_format` is NOT supported on gpt-image-2; the API returns HTTP 400 if sent. Images always return as base64 in `data[0].b64_json`.

### Complete example request

```json
POST /v1/images/generations
{
  "model": "gpt-image-2",
  "prompt": "Editorial hero image for a fintech landing page. Scene: bright modern office, soft morning light filtering through floor-to-ceiling windows. Subject: a 30-something analyst in a charcoal blazer and open-collar shirt, examining a tablet with focused expression, seated at a walnut desk. Details: shallow depth of field, crisp UI on tablet reading 'Q2 Revenue +18%', muted teal accent, subtle glass-and-concrete office interior. Intended use: above-the-fold web hero for a B2B landing page, 16:9 crop-safe, clean space on the right for overlay headline. Constraints: no watermark, no extra text beyond the tablet UI, no additional logos.",
  "size": "1536x1024",
  "quality": "high",
  "n": 1,
  "output_format": "png",
  "background": "auto"
}
```

Python SDK:

```python
from openai import OpenAI
client = OpenAI(api_key=os.environ["OPENAI_API_KEY"])

result = client.images.generate(
    model="gpt-image-2",
    prompt="...",
    size="1536x1024",
    quality="high",
    n=1,
    output_format="png"
)

import base64
image_bytes = base64.b64decode(result.data[0].b64_json)
with open("out.png", "wb") as f:
    f.write(image_bytes)
```

### Instant Mode vs Thinking Mode

`gpt-image-2` has two inference modes accessed via product tier / parameter:

- **Instant Mode** (default): fast, standard generation. Used for most calls.
- **Thinking Mode**: spends extra reasoning tokens on composition planning, object counting, constraint validation before rendering. Used for layout-heavy prompts (infographics, slides, maps, dense scenes).

Thinking Mode costs more (variable reasoning tokens on top of image tokens) but dramatically reduces failures on prompts with multiple constraints. For a slide design with 7 text elements, 3 images, and a specific color palette, Thinking Mode is the difference between a one-shot success and a 3-retry workflow.

### Prompt patterns that work

OpenAI's cookbook recommends a structured, order-sensitive format. The model reads from context outward.

Structure in order:

1. **Scene / background** (sets mode and lighting)
2. **Subject** (specific, not generic)
3. **Key details** (materials, textures, colors, patterns, medium)
4. **Intended artifact** (ad, UI mock, infographic, slide, poster; sets polish level)
5. **Constraints** (no watermark, no extra text, specific aspect framing)

Example prompt template:

```
Scene: [environment, lighting, time of day].
Subject: [detailed description of person or object].
Details: [materials, colors, specific visual cues, text overlays].
Intended use: [what this is for - ad, UI, poster, slide, infographic].
Constraints: [what not to include, what to preserve, aspect framing].
```

### Multi-turn editing via Responses API

```python
response = client.responses.create(
    model="gpt-image-2",
    input="Generate an editorial portrait of an analyst at a walnut desk, 16:9.",
    tools=[{"type": "image_generation"}]
)

# Use the response_id in the follow-up for conversational edit
edit_response = client.responses.create(
    model="gpt-image-2",
    previous_response_id=response.id,
    input="Keep everything. Change the background to a blurred bookshelf instead of an office.",
    tools=[{"type": "image_generation"}]
)
```

Multi-turn editing preserves identity, pose, lighting, framing across turns when explicitly told to "preserve" those elements.

### Multi-image batch generation

`n: 10` produces 10 images from one prompt that are consistent in character, style, and composition. Use cases:

- Product lineup: 10 views of the same product with slight variations
- Character sheet: one character across 10 poses / outfits
- Storyboard: 10 sequential scenes with consistent art style
- Ad variants: 10 different headlines on the same base composition

Note that batch consistency differs from multi-turn consistency. Batch is "10 images generated together share attributes." Multi-turn is "image 2 inherits from image 1." Both are supported.

### Pricing (April 2026)

Token-based:

- \$5 per 1M input text tokens
- \$10 per 1M output text tokens
- \$8 per 1M input image tokens
- \$30 per 1M output image tokens
- \$2 per 1M cached image tokens

Per-image estimates (Instant Mode, high quality):

- 1024x1024: ~\$0.21
- 1024x1536: ~\$0.165

Thinking Mode adds variable reasoning tokens on top; budget variance required. Layout-heavy prompts (infographics, slides) cost more than loose illustrations.

### Known limitations

- Transparent backgrounds not supported on gpt-image-2 at launch (was supported on gpt-image-1)
- Brand logo consistency drifts across generations; use a dedicated logo overlay step for exact trademark reproduction
- Technical engineering diagrams (electrical schematics, CAD-style) need human QA
- Long-form embedded text (full paragraphs in-image) is less reliable than overlays; use for headlines and labels, not body copy
- Real identifiable people blocked by platform policy regardless of technical capability
- Hands are anatomically correct now but extreme gesture or interaction poses still occasionally fail
- Thinking Mode costs are non-deterministic; budget variance required

### When to use gpt-image-2 over alternatives

- Text-in-image accuracy (ads, posters, UI mocks, infographics, slides, multilingual)
- Photorealism with precise instruction-following
- Multi-image set consistency (storyboards, product families, character sheets)
- Conversational iterative edits via Responses API
- Any pipeline where you need API access and pay-per-image pricing
- Marketing assets where brand polish and text correctness matter

Not the right tool when: artistic hero art with editorial mood (Midjourney V8.1 wins), speed and cost dominate at high volume (Gemini Nano Banana 2 or Imagen 4 Fast wins), or you need transparent-background assets (fall back to gpt-image-1 legacy or Nano Banana 2).

---

<!-- abf-plug -->
> This pattern is one piece of a wider toolkit. Adjacent playbooks at [aibrandfactory.com](https://www.aibrandfactory.com).


## Part 6, Character Consistency Across Models

Keeping the same face, product, or brand across many generations is the hardest production problem in AI image generation. Each model has its own approach; they are not interchangeable.

![Midjourney Omni Reference character consistency demo, three before-and-after rows showing an anime elf boy, a renaissance swordsman, and an anime girl transformed into stylized variants while preserving facial features](embedded-visuals-optimized/midjourney-oref-01.jpg "Midjourney Omni Reference --oref. Source: updates.midjourney.com/omni-reference-oref/")

![Midjourney Omni Reference additional character consistency demo with varied style transfers](embedded-visuals-optimized/midjourney-oref-02.jpg "Midjourney Omni Reference. Source: updates.midjourney.com/omni-reference-oref/")

![Midjourney Omni Reference third demo set, character preservation across dramatically different art styles](embedded-visuals-optimized/midjourney-oref-03.jpg "Midjourney Omni Reference. Source: updates.midjourney.com/omni-reference-oref/")

### The Interleaved Payload Pattern (Gemini 3)

The Gemini-specific technique that moves character consistency from "drifts by generation 3" to "identical across 50+ generations."

Principle: send reference images and their context text alternating, so the model binds each reference to its labeled role before the final instruction.

```
[Image 1 bytes] → [Context 1 text] → [Image 2 bytes] → [Context 2 text] → ... → [Main prompt]
```

NOT:

```
[Image 1 bytes] → [Image 2 bytes] → [Image 3 bytes] → [All context as one block] → [Main prompt]
```

The first pattern works. The second produces drift because the model does not know which context belongs to which image.

Context text for each reference should be a labeled role:

- **Identity lock (primary character)**: "This person is the PROTAGONIST. Study their exact facial features, skin tone, hair texture, jawline, and build. They must be UNMISTAKABLY RECOGNIZABLE in the output."
- **Identity lock (secondary character)**: "This person is the SUPPORT CHARACTER. Keep their face identical."
- **Style transfer**: "Match this exact visual aesthetic, color palette, and composition style."
- **Logo**: "This is the brand logo. Preserve exact proportions, colors, and geometry."
- **Product**: "This is the product. Maintain exact shape, color, material, and proportions."
- **Scene**: "Reference for the location and atmosphere."

Best practices for character references:

- 2 to 3 photos of the same person from different angles (front, 3/4 profile, side profile)
- All evenly lit, similar exposure
- Include the primary character photo on EVERY generation in the series, not just the first
- Up to 14 reference images total per request; practical max 6 to 8

### Omni Reference (Midjourney V8.1)

The Midjourney equivalent. `--oref URL --ow [weight]`.

Rules:

- Only ONE image per `--oref` call
- `--ow 25` for loose style transfer (e.g., photo to anime conversion)
- `--ow 100` (default) for balanced reference use
- `--ow 400+` for strict face, clothing, detail preservation
- Works with external URLs or Midjourney-hosted images

For character consistency across a series, use the same `--oref URL` on every generation. Results are consistent but not identical; faces drift slightly between generations, less than with no reference but more than Gemini's interleaved payload approach.

For multi-character scenes, use `--oref` with one character and describe the other character in prompt text. Two-character scenes via Midjourney are weaker than via Gemini 3.

### Multi-image batch (gpt-image-2)

The OpenAI approach differs. `n: 10` generates 10 images together that share character and style attributes. Use case: one character across 10 poses or scenes.

Limitations:

- The 10 images are generated in a single call; you cannot mix multiple references across them
- Batch consistency is stronger within a single request than across separate requests
- For cross-request consistency, use the Responses API to chain requests with explicit "preserve face, identity" instructions in each follow-up

### The Character Anchor Prompt Template

Works across all three models. Include in the text portion of any prompt:

```
[age]-year-old [gender], [specific face shape], [specific hair description],
[specific distinguishing features], [specific skin details], [specific build],
[specific distinguishing clothing or accessory].
```

Example:

```
32-year-old woman with round face, shoulder-length dark wavy hair with subtle highlights,
warm brown eyes, prominent cheekbones, olive-toned freckled skin, average build,
almost always wearing a silver pendant necklace.
```

The more specific the descriptors, the more the model has to latch onto beyond reference images alone. This matters most when reference images cannot be sent (e.g., some Midjourney workflows without Omni Reference budget).

### The Hex-Code System (brand palette consistency)

For brand imagery that must use specific colors across many generations, include the exact hex codes in the prompt.

```
Use brand color palette:
- Primary: #1A0B4B (deep indigo) for backgrounds and primary surfaces
- Secondary: #06B6D4 (bright cyan) for accents
- Text / foreground: #FAF9FF (off-white)
- Avoid: any other colors; no warm reds, oranges, yellows; no neutral beiges.
```

All three models parse hex codes. Gemini 3 is most accurate; gpt-image-2 close behind; Midjourney requires occasional prompt reinforcement ("the cyan accent must be specifically #06B6D4, not teal or turquoise").

For logos, include a reference image of the logo plus the hex colors of each logo element in prompt text. Combining reference + hex prompt beats either alone.

### When character consistency fails

Four common failure modes:

1. **No identity anchor in prompt**: the model has a reference image but no text description of the face. Fix: add a prompt description of distinguishing features.
2. **Too many characters**: beyond 3 to 5 named characters, every model degrades. Fix: reduce character count per generation; compose multi-character scenes from multiple single-character generations.
3. **Extreme pose change**: the reference is a front-facing portrait; the target is a full-body action shot. The face latitude between the two is large enough that identity drifts. Fix: intermediate generations at moderate pose changes, building toward the target.
4. **Style transfer conflict**: generating a stylized caricature from a photographic reference. The style change is strong enough to erase identity. Fix: explicit "PRESERVE EXACT FACE/HAIR/BODY from reference. This is the comic hero version of the same person." plus raised `--ow` on Midjourney or stronger text anchors on Gemini.

---

## Part 7, Production Workflows

Everything above is per-image. At production scale (hundreds to thousands of images per campaign), four additional concerns dominate.

### Workflow 1, Batch generation with cost control

Running thousands of images per day requires cost discipline.

- **Draft then upscale**: generate at 1K resolution for initial variants (cheap, fast), upscale selected winners to 2K or 4K. Every model supports this workflow; Gemini Imagen 4 Fast at \$0.02 per image makes drafts nearly free.
- **Flex / batch tier**: Gemini 3 offers a flex tier at ~50 percent discount for async batch work. Use for anything that is not time-critical.
- **Mode tiering**: use Thinking Mode (gpt-image-2) or full-resolution Gemini 3 Pro only for the final-pass assets; use Instant Mode / Nano Banana 2 Flash / Imagen 4 Fast for everything upstream.
- **Cache aggressively**: if your pipeline can generate variants from a shared set of reference images, upload the references once and reuse them. gpt-image-2 caches input image tokens at \$2/1M (vs \$8/1M uncached).

Typical cost envelope: \$50 to \$500 for a 1,000-image campaign depending on model mix, tier, and resolution.

### Workflow 2, Brand consistency at scale

Running consistent brand imagery across many generations requires three locking mechanisms:

1. **Character Bible**: one document with photo references and detailed text descriptions for every recurring character, product, or brand element. This is the source of truth. Every prompt pulls from it.
2. **Style Bible**: one document with the brand palette (hex codes), lighting setups, typography style, composition rules. Every prompt enforces these.
3. **Reference Image Library**: organized by role (characters/, products/, scenes/, logos/, style-references/). Every prompt pulls the right references from the library by path.

All three live in the companion git repo under `config/` with examples.

### Workflow 3, Multi-model fallback pipeline

No single model wins on every task. Production pipelines in 2026 typically run all three flagships:

```
Task router
  |
  +-- Text-in-image needed? --> gpt-image-2 OR Gemini 3 Pro Image
  +-- Pure aesthetic hero? --> Midjourney V8.1 (manual)
  +-- Character consistency across set? --> Gemini 3 Pro Image
  +-- Multi-image batch? --> gpt-image-2 with n=10
  +-- Draft / low cost? --> Nano Banana 2 Flash or Imagen 4 Fast
```

The pipeline picks the right model per task, generates, validates, and returns the result. Where one model fails, retry with the next-best alternative.

### Workflow 4, Validation and quality gates

Auto-generated images need auto-validation before shipping to production.

Six checks to run on every generated image:

1. **Dimensions match requested size**. Specifically important on Gemini 3 where `image_size: "2K"` is occasionally ignored.
2. **Content moderation pass**. Run the image through moderation API (OpenAI moderation, Google Cloud Vision SafeSearch) before using.
3. **OCR text match**. If the prompt specified text to render, OCR the image and fuzzy-match against expected. Regenerate on mismatch.
4. **Brand palette match**. Sample the image at known regions; verify colors are within ~5 percent of brand hex codes.
5. **Face / subject presence**. For character generation, run face detection; verify one face is present (or the expected count).
6. **Artifact check**. Use a quality-detection model to flag obvious AI artifacts (weird fingers, distorted typography, contextually inappropriate elements).

Images failing any check are regenerated or routed to human review.

### Workflow 5, Attribution and watermarking

Legal / ethical layer, increasingly important in 2026:

- **Google Gemini** outputs carry SynthID (visible and invisible watermarks). Do not strip; required by ToS.
- **OpenAI gpt-image-2** outputs carry C2PA metadata in the PNG; ToS requires not to strip.
- **Midjourney** outputs do not carry identifying watermarks on Pro+ tiers but ToS still requires attribution for certain commercial contexts.

For brand use, add your own attribution or branding as a post-processing step. Keep the original unwatermarked version for audit purposes.

---

## Part 8, Validation and the 8 Common Mistakes

The eight most common mistakes that quietly kill image quality at scale, with the fix for each.

### Mistake 1, Using one model's prompt patterns on another

gpt-image-2 prose style on Midjourney produces mediocre Midjourney output. Midjourney-style parameter flags on gpt-image-2 fail entirely. Writing Gemini JSON prompts for Midjourney wastes tokens.

**Fix**: learn each model's grammar. Part 3 (Gemini), Part 4 (Midjourney), Part 5 (gpt-image-2).

### Mistake 2, Prompts that lead with style before subject

"A beautiful, cinematic, dramatic image of a person..." puts style first, subject last. The model spends most of its attention budget on "beautiful cinematic dramatic" and gets to the actual subject with weaker signal.

**Fix**: lead with the subject. "A 30-something analyst in a charcoal blazer..."

### Mistake 3, Under-specifying the subject

"A person" or "a woman" or "a guy". The model has a wide semantic distribution for these; output falls in the middle.

**Fix**: specific synonyms. "A 40-year-old Southeast Asian woman with shoulder-length dark hair and a confident smile, wearing a tailored navy suit."

### Mistake 4, No reference image for character consistency

Describing a face in text alone is insufficient for cross-generation consistency. Every generation produces a slightly different face.

**Fix**: use reference images. `--oref` on Midjourney. Interleaved payload on Gemini. Multi-image batch on gpt-image-2. Plus detailed text description as anchor.

### Mistake 5, No validation step on generated output

Auto-generated images shipped to production without validation carry risk: wrong dimensions, missing text, brand palette drift, policy violation.

**Fix**: automated validation pipeline (see Part 7, Workflow 4). Every generated image passes through 6 checks before it is considered production-ready.

### Mistake 6, Generating at full quality for drafts

Every draft at 4K on gpt-image-2 costs ~\$0.21 or on Gemini ~\$0.24. 100 drafts at full quality is \$20. 1000 drafts is \$200. Drafts should be cheap.

**Fix**: draft at 1K on Imagen 4 Fast (\$0.02) or Nano Banana 2 Flash. Upscale selected winners to 4K. Total cost for a 100-draft / 5-final workflow: ~\$3 instead of ~\$25.

### Mistake 7, Too many reference images

Beyond 8 references, every model has trouble weighting which reference matters for which part of the output. Faces drift. Styles conflict.

**Fix**: max 6 to 8 references per request. For complex scenes, compose from multiple simpler generations.

### Mistake 8, Ignoring model-specific limitations

gpt-image-2 cannot do transparent backgrounds. Gemini 3 Pro Image ignores `image_size: "2K"` in the Node SDK sometimes. Midjourney V8 drops faces for extreme pose changes. Each model has known failure modes that show up in production.

**Fix**: read the Known Limitations section of each model's Part (3, 4, 5). Include the workarounds in your pipeline (fallback model, retry logic, dimension validation). Plan for the limitations.

### The pre-production checklist

Before using AI image generation in production, verify:

- [ ] Model selection criteria documented per task type (what triggers which model)
- [ ] Character Bible exists with text descriptions + reference images for every recurring subject
- [ ] Style Bible exists with brand hex codes, lighting, typography conventions
- [ ] Reference image library organized by role (characters/, products/, scenes/, logos/)
- [ ] Prompt templates exist for each page type / asset type, reusable across generations
- [ ] Validation pipeline runs on every generated image (dimensions, OCR, palette, faces, moderation, artifacts)
- [ ] Fallback model chain defined (primary → secondary → tertiary) with retry logic
- [ ] Cost budgets defined per task tier; drafting uses cheap models, final uses flagship
- [ ] Watermark / attribution policy aligned with each model's ToS
- [ ] Legal sign-off on generated images for any identifiable people, trademarks, or copyrighted elements

When all of the above is true, the pipeline is production-ready.

---

There is more where this came from. For deeper playbooks on AI search visibility, conversion tracking, structured data, and marketing infrastructure, visit www.aibrandfactory.com.

The companion GitHub repository (`AI-BrandFactory/ai-image-bible`) ships the organized prompt templates, payload structures, and Python reference implementations for gpt-image-2, Midjourney V8.1, and Gemini 3 Pro Image. Clone it, configure your API keys, and start generating.

The three flagship models in April 2026 are more capable than anything that existed 18 months earlier. The gap between someone who uses them well and someone who uses them casually is larger now than it has ever been. This bible is the reference that closes that gap.
