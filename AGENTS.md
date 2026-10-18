# AGENTS.md

Instructions for coding agents using this repository to build or restyle a landing page.

## What is here

`pages/<slug>/` holds one complete landing page per folder:

- `index.html` — the reference build. One file, every asset inlined, opens from disk, no build step.
- `PROMPT.md` — the one-shot brief it was built from: stack, design values as numbers, structure,
  and the things that break.
- `README.md` — what the page is best for, its style, sections, stack and credits.

`index.json` lists all of them with the same metadata. Read it first; it is small.

## The loop

1. **Choose.** Match the user's request against `bestFor` and `style` in `index.json`. Shortlist two
   or three and read their `README.md` files, not their HTML.
2. **Decide how to use it.**
   - The user has a framework (React, Vue, Svelte, Astro, …): build from `PROMPT.md` in that
     framework. This gives cleaner code than translating a 100 KB file.
   - The user wants this exact page, fast: copy `index.html` and adapt it.
3. **Before editing an `index.html`,** read its header comment (the first ~30 lines). It maps the
   design tokens (`:root` custom properties), the `data-section` names in order, what each script
   does, and lists what breaks when edited naively.
4. **Lift a section** by its `data-section` attribute: take that element, the CSS rules it uses and
   the tokens from `:root`. `data-component` marks widgets worth lifting on their own.
5. **Adapt.** Replace the fictional brand, copy, numbers, logos and testimonials with the user's.
   Keep the brief's design values and its warnings — they are why the result looks designed.
6. **Verify in a browser:** no console errors, no horizontal scroll at 390px wide, and
   `prefers-reduced-motion` respected.

## Rules

- Every brand, figure, logo and testimonial in these pages is invented. Never ship them as real.
- Where a page's `README.md` lists **Built on**, keep that attribution.
- Do not hotlink other sites' images or assets when adapting a page.
- License: MIT.

## Design systems

`systems/<slug>/` holds design systems extracted from the pages. To restyle a project in one,
read its README.md (conventions), link or copy `<slug>.css` (tokens + components scoped under its
root class), take component markup from `specimen.html` (`<section data-component>` blocks), and use
the tokens for every colour, font, radius, shadow and timing. Keep the project's logic as it is.
Live, with a copyable agent instruction: https://instalanding.ai/systems
