# Generative Editorial Product Page

Fashion-editorial layout for an AI product, every image a gooey generative composition.

![Generative Editorial Product Page](preview.jpg)

**Open it:** [`index.html`](index.html) runs straight from disk — one file, every asset inlined, no build step. [Live demo](https://instalanding.ai/demos/prism-evals-editorial.html) · [Page on InstaLanding](https://instalanding.ai/prompt/generative-editorial-product-page)

**The prompt:** [`PROMPT.md`](PROMPT.md) is this same file with a short instruction on top: keep the design, replace the brand and copy, convert to your stack. Paste it into Claude Code, Cursor, ChatGPT or any builder and it builds this page.

| | |
| --- | --- |
| Best for | LLM eval platforms, AI quality and CI gates, developer tools, editorial product launches |
| Style | light, editorial, generative-art, gooey, serif |
| Sections | nav → hero → ticker → hero-art → logos → about → runs → product → ticker-2 → testimonials → pricing → cta → contact → footer |
| Libraries | gsap 3.12.5 |
| Fonts | Asul, Cabin, Covered By Your Grace, IBM Plex Mono (Google Fonts) |
| Uses | inline-svg, inlined-images, reduced-motion |
| Size | 103 KB · prompt ~25,852 tokens |

Every region is tagged `data-section`, and the file opens with a header comment that maps its design tokens, sections and scripts, and lists what breaks when you edit it. Read that first.

The brand, copy, numbers and testimonials on this page are fictional. Replace them before you ship.
