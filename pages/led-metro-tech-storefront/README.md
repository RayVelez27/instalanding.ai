# LED Metro Tech Storefront

A big-tech devices homepage in warm clay and glass, with a live LED metro map for a hero, a Personal/Business switch that rewrites the page, and a dot-matrix ticker.

![LED Metro Tech Storefront](preview.jpg)

**Open it:** [`index.html`](index.html) runs straight from disk — one file, every asset inlined, no build step. [Live demo](https://instalanding.ai/demos/meridian-led-storefront.html) · [Page on InstaLanding](https://instalanding.ai/prompt/led-metro-tech-storefront)

**The prompt:** [`PROMPT.md`](PROMPT.md) is this same file with a short instruction on top: keep the design, replace the brand and copy, convert to your stack. Paste it into Claude Code, Cursor, ChatGPT or any builder and it builds this page.

| | |
| --- | --- |
| Best for | consumer electronics and hardware launches, big-tech style company homepages, software suites with personal and business audiences, AI assistant announcements |
| Style | light, claymorphism, glassmorphism, led-dot-matrix, editorial, gsap |
| Sections | nav → hero → quick-links → featured → travel → ai → faq → ballot → footer |
| Libraries | gsap 3.12.2 |
| Fonts | Bricolage Grotesque, Fraunces, Instrument Sans, Inter (Google Fonts) |
| Uses | inline-svg, inlined-images, reduced-motion |
| Size | 127 KB · prompt ~32,751 tokens |

Every region is tagged `data-section`, and the file opens with a header comment that maps its design tokens, sections and scripts, and lists what breaks when you edit it. Read that first.

## Built on

- [CSS LED Challenge by Ben Evans (ivorjetski) on CodePen](https://codepen.io/editor/ivorjetski/pen/01a07dcf-a1e8-7ab6-aea1-aa98135803b3) — The LED dot-matrix style the metro maps are adapted from

Keep this attribution if you redistribute the component; the original's own terms apply to the parts taken from it.

The brand, copy, numbers and testimonials on this page are fictional. Replace them before you ship.
