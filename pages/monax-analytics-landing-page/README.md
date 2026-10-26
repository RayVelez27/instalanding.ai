# Monax Analytics Landing Page

Dithered WebGL halftone panels, glossy 3D orbs, tabbed product demo, bento + pricing.

![Monax Analytics Landing Page](preview.jpg)

**Open it:** [`index.html`](index.html) runs straight from disk — one file, every asset inlined, no build step. [Live demo](https://instalanding.ai/demos/monax-analytics.html) · [Page on InstaLanding](https://instalanding.ai/prompt/monax-analytics-landing-page)

**The prompt:** [`PROMPT.md`](PROMPT.md) is this same file with a short instruction on top: keep the design, replace the brand and copy, convert to your stack. Paste it into Claude Code, Cursor, ChatGPT or any builder and it builds this page.

| | |
| --- | --- |
| Best for | analytics SaaS, BI and data platforms, B2B dashboards, data team tools |
| Style | light, warm-paper, 3d-orbs, webgl, bento |
| Sections | nav → hero → fan-stack → logos → product → features → testimonials → pricing → resources → footer |
| Libraries | gsap 3.12.5 |
| Fonts | Inter (Google Fonts) |
| Uses | webgl, inline-svg, inlined-images, reduced-motion |
| Size | 130 KB · prompt ~33,489 tokens |

Every region is tagged `data-section`, and the file opens with a header comment that maps its design tokens, sections and scripts, and lists what breaks when you edit it. Read that first.

The brand, copy, numbers and testimonials on this page are fictional. Replace them before you ship.
