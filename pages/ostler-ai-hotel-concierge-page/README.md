# Ostler AI Hotel Concierge Page

A late-night oxblood page for an AI hotel concierge: a giant "Ostler" springs apart letter by letter over a guest's phone chat, six module covers slide past sideways, "Awake" zooms into a hotel facade at night, and every phone, dashboard and room is drawn in SVG.

![Ostler AI Hotel Concierge Page](preview.jpg)

**Open it:** [`index.html`](index.html) runs straight from disk — one file, every asset inlined, no build step. [Live demo](https://instalanding.ai/demos/ostler-hotel-concierge.html) · [Page on InstaLanding](https://instalanding.ai/prompt/ostler-ai-hotel-concierge-page)

**The prompt:** [`PROMPT.md`](PROMPT.md) is this same file with a short instruction on top: keep the design, replace the brand and copy, convert to your stack. Paste it into Claude Code, Cursor, ChatGPT or any builder and it builds this page.

| | |
| --- | --- |
| Best for | hospitality software, AI agents and assistants, customer support automation, vertical B2B SaaS |
| Style | editorial, card-stack, fill-type, svg-illustration, scroll-driven |
| Sections | nav → hero → ticker → logos → story → modules → pricing → statement → process → changelog → voices → gallery → faq → contact → footer |
| Libraries | gsap 3.13.0, lenis 1.3.4 |
| Fonts | Gabarito, Instrument Sans (Google Fonts) |
| Uses | inline-svg, inlined-images, reduced-motion |
| Size | 138 KB · prompt ~35,574 tokens |

Every region is tagged `data-section`, and the file opens with a header comment that maps its design tokens, sections and scripts, and lists what breaks when you edit it. Read that first.

The brand, copy, numbers and testimonials on this page are fictional. Replace them before you ship.
