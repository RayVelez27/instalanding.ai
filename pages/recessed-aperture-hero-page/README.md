# Recessed Aperture Hero Page

Soft UI in a violet palette: an aperture sunk into the page, tokens drifting across it, and a working run dial below.

![Recessed Aperture Hero Page](preview.jpg)

**Open it:** [`index.html`](index.html) runs straight from disk — one file, every asset inlined, no build step. [Live demo](https://instalanding.ai/demos/mnemo-context-window.html) · [Page on InstaLanding](https://instalanding.ai/prompt/recessed-aperture-hero-page)

**The prompt:** [`PROMPT.md`](PROMPT.md) is this same file with a short instruction on top: keep the design, replace the brand and copy, convert to your stack. Paste it into Claude Code, Cursor, ChatGPT or any builder and it builds this page.

| | |
| --- | --- |
| Best for | agent memory infrastructure, LLM platform APIs, AI developer tools, usage-priced dev products |
| Style | purple, neumorphic, soft-ui, parallax, condensed-type |
| Sections | nav → hero → features → stats → how-it-works → console → pricing → faq → footer |
| Libraries | none — plain HTML, CSS and JS |
| Fonts | Barlow Condensed, Barlow (Google Fonts) |
| Uses | inline-svg, inlined-images, reduced-motion |
| Size | 103 KB · prompt ~26,636 tokens |

Every region is tagged `data-section`, and the file opens with a header comment that maps its design tokens, sections and scripts, and lists what breaks when you edit it. Read that first.

## Built on

- [Parallax 404 by Rafaela Lucas](https://www.rafaelalucas.com) — The recessed discs, the drifting pills and the doubled figure come from this pen.

Keep this attribution if you redistribute the component; the original's own terms apply to the parts taken from it.

The brand, copy, numbers and testimonials on this page are fictional. Replace them before you ship.
