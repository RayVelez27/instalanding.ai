# Manga Panel Dev Tool Page

A deploy CLI pitched as a black-and-white manga issue: a sliced retro sun over a city skyline, a typing terminal, three villains defeated and a reader-mail FAQ.

![Manga Panel Dev Tool Page](preview.jpg)

**Open it:** [`index.html`](index.html) runs straight from disk — one file, every asset inlined, no build step. [Live demo](https://instalanding.ai/demos/overclock-deploy.html) · [Page on InstaLanding](https://instalanding.ai/prompt/manga-panel-dev-tool-page)

**The prompt:** [`PROMPT.md`](PROMPT.md) is this same file with a short instruction on top: keep the design, replace the brand and copy, convert to your stack. Paste it into Claude Code, Cursor, ChatGPT or any builder and it builds this page.

| | |
| --- | --- |
| Best for | developer tools and CLIs, deploy and hosting platforms, indie dev launches, playful B2B SaaS |
| Style | black-and-white, manga, comic, halftone, hand-drawn, svg-animation, retro-sun |
| Sections | nav → hero → stats → features → how-it-works → pricing → faq → cta → footer |
| Libraries | none — plain HTML, CSS and JS |
| Fonts | Anton, Bangers, Barlow Condensed, JetBrains Mono (Google Fonts) |
| Uses | inline-svg, reduced-motion |
| Size | 70 KB · prompt ~18,053 tokens |

Every region is tagged `data-section`, and the file opens with a header comment that maps its design tokens, sections and scripts, and lists what breaks when you edit it. Read that first.

The brand, copy, numbers and testimonials on this page are fictional. Replace them before you ship.
