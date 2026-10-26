# Machine Front Panel Page

The landing page is the front panel: it boots itself on load, runs a needle self-test, then hands the switches to you.

![Machine Front Panel Page](preview.jpg)

**Open it:** [`index.html`](index.html) runs straight from disk — one file, every asset inlined, no build step. [Live demo](https://instalanding.ai/demos/kiln-panel.html) · [Page on InstaLanding](https://instalanding.ai/prompt/machine-front-panel-page)

**The prompt:** [`PROMPT.md`](PROMPT.md) is this same file with a short instruction on top: keep the design, replace the brand and copy, convert to your stack. Paste it into Claude Code, Cursor, ChatGPT or any builder and it builds this page.

| | |
| --- | --- |
| Best for | on-prem AI hardware, AI infrastructure, self-hosted LLM appliances, live telemetry products |
| Style | dark, industrial, skeuomorphic, monospace, amber-accent |
| Sections | nav → menu → hero → why → inside → spec-sheet → compare → install → configurations → faq → cta → footer |
| Libraries | none — plain HTML, CSS and JS |
| Fonts | Archivo, JetBrains Mono (Google Fonts) |
| Uses | inline-svg, inlined-images, reduced-motion |
| Size | 140 KB · prompt ~36,100 tokens |

Every region is tagged `data-section`, and the file opens with a header comment that maps its design tokens, sections and scripts, and lists what breaks when you edit it. Read that first.

The brand, copy, numbers and testimonials on this page are fictional. Replace them before you ship.
