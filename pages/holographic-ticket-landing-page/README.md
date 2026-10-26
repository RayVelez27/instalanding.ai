# Holographic Ticket Landing Page

A WebGL agent swarm you can shove out of the way, and die-cut holographic tickets masked out of one conic gradient.

![Holographic Ticket Landing Page](preview.jpg)

**Open it:** [`index.html`](index.html) runs straight from disk — one file, every asset inlined, no build step. [Live demo](https://instalanding.ai/demos/murmur-swarm-tickets.html) · [Page on InstaLanding](https://instalanding.ai/prompt/holographic-ticket-landing-page)

**The prompt:** [`PROMPT.md`](PROMPT.md) is this same file with a short instruction on top: keep the design, replace the brand and copy, convert to your stack. Paste it into Claude Code, Cursor, ChatGPT or any builder and it builds this page.

| | |
| --- | --- |
| Best for | AI research labs, multi-agent platforms, model family showcases, early-access waitlists |
| Style | light, pastel, holographic, webgl, three.js |
| Sections | hero → marquee → lab → products → how-it-works → models → quote → cta → footer |
| Libraries | three r128, gsap 3.12.5 |
| Fonts | Oswald (Google Fonts) |
| Uses | inline-svg, reduced-motion |
| Size | 72 KB · prompt ~18,748 tokens |

Every region is tagged `data-section`, and the file opens with a header comment that maps its design tokens, sections and scripts, and lists what breaks when you edit it. Read that first.

The brand, copy, numbers and testimonials on this page are fictional. Replace them before you ship.
