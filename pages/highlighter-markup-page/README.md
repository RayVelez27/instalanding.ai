# Highlighter Markup Page

A marked-up document: every highlight is a real highlighter, rough-edged by an SVG displacement filter, with a colour per verdict.

![Highlighter Markup Page](preview.jpg)

**Open it:** [`index.html`](index.html) runs straight from disk — one file, every asset inlined, no build step. [Live demo](https://instalanding.ai/demos/footnote-grounding.html) · [Page on InstaLanding](https://instalanding.ai/prompt/highlighter-markup-page)

**The prompt:** [`PROMPT.md`](PROMPT.md) is this same file with a short instruction on top: keep the design, replace the brand and copy, convert to your stack. Paste it into Claude Code, Cursor, ChatGPT or any builder and it builds this page.

| | |
| --- | --- |
| Best for | LLM grounding and evals, RAG citation checking, AI trust and safety, document AI |
| Style | light, editorial, paper, serif, highlighter |
| Sections | nav → hero → verdicts → demo → stats → how-it-works → payload → uses → faq → cta → footer |
| Libraries | none — plain HTML, CSS and JS |
| Fonts | Source Serif 4, JetBrains Mono, Caveat, Mynerve, Special Elite (Google Fonts) |
| Uses | inline-svg, inlined-images, reduced-motion |
| Size | 141 KB · prompt ~36,345 tokens |

Every region is tagged `data-section`, and the file opens with a header comment that maps its design tokens, sections and scripts, and lists what breaks when you edit it. Read that first.

## Built on

- [Nice <mark> by Christian Alder](https://codepen.io/HejChristian) — The highlighter treatment - the displaced ::before, the pen blob and the --color hook - comes from this pen.

Keep this attribution if you redistribute the component; the original's own terms apply to the parts taken from it.

The brand, copy, numbers and testimonials on this page are fictional. Replace them before you ship.
