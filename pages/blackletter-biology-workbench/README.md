# Blackletter Biology Workbench

A computational biology platform set like an illuminated manuscript: blackletter headings lit by a WebGL shader, spinning conic frame borders, and hand-drawn lab sketches in the margins.

![Blackletter Biology Workbench](preview.jpg)

**Open it:** [`index.html`](index.html) runs straight from disk — one file, every asset inlined, no build step. [Live demo](https://instalanding.ai/demos/mistfold-biology-workbench.html) · [Page on InstaLanding](https://instalanding.ai/prompt/blackletter-biology-workbench)

**The prompt:** [`PROMPT.md`](PROMPT.md) is this same file with a short instruction on top: keep the design, replace the brand and copy, convert to your stack. Paste it into Claude Code, Cursor, ChatGPT or any builder and it builds this page.

| | |
| --- | --- |
| Best for | biotech and life-science platforms, scientific and research software, computational tools for academic labs, brands with a literary or archival voice |
| Style | light, editorial, blackletter, webgl, hand-drawn, manuscript |
| Sections | nav → hero → modules → workflow → pricing → cta-footer |
| Libraries | roughjs 4.6.6 |
| Fonts | Fanwood Text, Cinzel, UnifrakturMaguntia, JetBrains Mono (Google Fonts) |
| Uses | webgl, canvas-2d, inline-svg, inlined-images, reduced-motion |
| Size | 57 KB · prompt ~14,682 tokens |

Every region is tagged `data-section`, and the file opens with a header comment that maps its design tokens, sections and scripts, and lists what breaks when you edit it. Read that first.

## Built on

- [Rough.js by Preet Shihn](https://roughjs.com) — The hand-drawn rendering library behind the margin sketches (MIT)

Keep this attribution if you redistribute the component; the original's own terms apply to the parts taken from it.

The brand, copy, numbers and testimonials on this page are fictional. Replace them before you ship.
