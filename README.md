# The AI Image Bible

As of April 25, 2026 three models lead AI image generation: OpenAI's gpt-image-2, Midjourney V8.1 Alpha, and Google's Gemini 3 Pro Image (Nano Banana Pro). Each has its own prompt grammar, its own payload structure, its own pricing, and its own category of strengths. This is the one reference that covers all three properly: API payloads, parameter syntax, JSON prompting, character consistency patterns, the interleaved payload technique, pricing at every tier, example outputs from each model, and the complete companion repo of prompts and payload templates.

---

> **Part of the AI BrandFactory open toolkit.**
> Free to use and adapt with attribution.
> More tools, templates, and AI systems at [aibrandfactory.com](https://www.aibrandfactory.com)

---

## What's Inside

- Full reference for all three 2026 flagship models: gpt-image-2 (OpenAI, April 2026), Midjourney V8.1 Alpha (April 2026), Gemini 3 Pro Image / Nano Banana Pro (Google, Nov 2025 to April 2026). With capabilities, pricing, and decision criteria for each.
- Complete API payloads: OpenAI Images endpoint for gpt-image-2 with all parameters; Gemini generateContent payload with interleaved reference images; Midjourney parameter reference (--ar --oref --sref --stylize and the rest).
- JSON prompting for Gemini 3: the structured prompt pattern that raises accuracy 60 to 80 percent on multi-constraint tasks, with complete schemas for subjects, styles, compositions, and text overlays.
- The Interleaved Payload Pattern: the [Image][Context][Image][Context][Prompt] structure, proven across 280+ tests, for character consistency across multi-image series.
- Character consistency in all three models: Midjourney Omni Reference, Gemini multi-image fusion (up to 14 refs), GPT Image 2 multi-image batch generation (up to 10). The hex-code system for brand palette consistency.
- The companion git repo: organized prompts and payload templates for each model, the Python reference implementations, the JSON schemas. Clone, configure keys, start generating.

## Files

- `playbook.md` — full playbook source in Markdown
- `playbook.pdf` — rendered PDF for download / sharing
- `copy.json` — title, hook, benefits, schema for re-publishing
- `image-prompts.json` — Gemini prompts for the brand 4 images (cover, hero, og, notion-cover)


## Read or Download

- Live page: [files.aibrandfactory.com/playbooks/ai-image-bible](https://files.aibrandfactory.com/playbooks/ai-image-bible)
- Notion duplicatable template: [https://massiveimpact.notion.site/The-AI-Image-Bible-34cfb27e663481869807cd0a96baf6c4](https://massiveimpact.notion.site/The-AI-Image-Bible-34cfb27e663481869807cd0a96baf6c4)

## Use

Fork this repo, edit `playbook.md` for your own audience or customize the prompts in `image-prompts.json` to re-skin for your brand. Attribution required per LICENSE.

## License

Free to use with attribution. See [LICENSE](LICENSE) for details.

Built by [AI BrandFactory](https://www.aibrandfactory.com), tools and systems for AI-powered content businesses.
