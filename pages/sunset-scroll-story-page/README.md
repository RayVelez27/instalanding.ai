# Sunset Scroll Story Page

A fusion company told as one long sunset: scroll and the sun goes down over a layered SVG landscape, night falls, then a live canvas tokamak takes over.

![Sunset Scroll Story Page](preview.jpg)

**Open it:** [`index.html`](index.html) runs straight from disk — one file, every asset inlined, no build step. [Live demo](https://instalanding.ai/demos/solstice-fusion.html) · [Page on InstaLanding](https://instalanding.ai/prompt/sunset-scroll-story-page)

**The prompt:** [`PROMPT.md`](PROMPT.md) is this same file with a short instruction on top: keep the design, replace the brand and copy, convert to your stack. Paste it into Claude Code, Cursor, ChatGPT or any builder and it builds this page.

| | |
| --- | --- |
| Best for | climate and energy startups, deep-tech company sites, hardware launches, storytelling homepages |
| Style | illustrated, parallax, scroll-driven, sunset-gradient, canvas, gsap |
| Sections | nav → hero → story → scene → stats → features → reactor → how-it-works → timeline → careers → cta → footer |
| Libraries | gsap 3.12.5 |
| Fonts | Space Grotesk, Inter, JetBrains Mono (Google Fonts) |
| Uses | canvas-2d, inline-svg, reduced-motion |
| Size | 162 KB · prompt ~41,729 tokens |

Every region is tagged `data-section`, and the file opens with a header comment that maps its design tokens, sections and scripts, and lists what breaks when you edit it. Read that first.

## Built on

- [Parallax scroll landscape by isladjan](https://isladjan.com/work/4/) — The layered SVG landscape and its sunset-to-night scroll choreography come from this piece.

Keep this attribution if you redistribute the component; the original's own terms apply to the parts taken from it.

The brand, copy, numbers and testimonials on this page are fictional. Replace them before you ship.
