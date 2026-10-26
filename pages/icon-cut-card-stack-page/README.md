# Icon-Cut Card Stack Page

Glass cards with their icon punched clean through, on gradient throughlines that travel as you scroll.

![Icon-Cut Card Stack Page](preview.jpg)

**Open it:** [`index.html`](index.html) runs straight from disk — one file, every asset inlined, no build step. [Live demo](https://instalanding.ai/demos/throughline-scroll-stack.html) · [Page on InstaLanding](https://instalanding.ai/prompt/icon-cut-card-stack-page)

**The prompt:** [`PROMPT.md`](PROMPT.md) is this same file with a short instruction on top: keep the design, replace the brand and copy, convert to your stack. Paste it into Claude Code, Cursor, ChatGPT or any builder and it builds this page.

| | |
| --- | --- |
| Best for | AI infrastructure, LLM ops and eval platforms, developer tools, model gateways |
| Style | dark, monospace, spectrum-gradient, scroll-driven, poster |
| Sections | nav → hero → card-stack → features → stats → pricing → faq → cta → footer |
| Libraries | gsap 3.12.5 |
| Fonts | Source Code Pro, Anton (Google Fonts) |
| Uses | inline-svg, inlined-images, reduced-motion |
| Size | 132 KB · prompt ~34,030 tokens |

Every region is tagged `data-section`, and the file opens with a header comment that maps its design tokens, sections and scripts, and lists what breaks when you edit it. Read that first.

The brand, copy, numbers and testimonials on this page are fictional. Replace them before you ship.
