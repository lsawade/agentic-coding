# Agentic AI for Research — Marp deck

A Marp slide deck (`slides.md`) with a custom theme (`themes/princeton.css`) and hand-written SVG
schematics (`assets/diagrams/`). Built with `@marp-team/marp-cli`; config in `.marprc.yml`.

## Commands

- `npm run build` → `dist/index.html`; `npm run pdf` → `dist/slides.pdf`; `npm run png` → one PNG per slide in `review/`.
- PDF/PNG export needs a local Chrome. If Marp cannot find it, pass
  `--browser-path "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"`.
- After any slide edit, run `npm run png` and look at the affected slide images; overflow is the common failure.

## Slide conventions

- Canvas 1280×720, h1 44px, body 26px. Budget per slide: a title plus either one figure at `h:430`, or ~10 lines
  of text, or a figure at `h:330` plus two tip cards. Do not exceed it; move material to presenter notes.
- Every content slide starts with `<!-- _header: "N · Section name" -->`. Black slides use `<!-- _class: lead -->`
  or `<!-- _class: handoff -->` with `<!-- _header: "" -->`.
- Presenter notes are the last HTML comment of a slide, starting with `Notes:`.
- Theme classes: `cards` (+`one`/`two`) with `tip` cards; `cols`, `cols-3`; `stats`/`stat` (`.n`, `.c`);
  `quiz`/`task` (+`badge frontier|mid|small`, `why`); `callout`; `punch`; `big`; `small`; `muted`; `pill`;
  `kv`; `check`; `placeholder`; `timer`; `mark.bug`. HTML is enabled.
- SVG schematics: viewBox 1600×900 (full) or 1600×560 (half); palette orange `#E87722`, black, ink `#1f1f1f`,
  gray `#6b6b6b`, line `#d9d4cc`, card `#f6f3ee`; labels ≥ 30px; no gradients, filters or external fonts.
- Any number on a slide must appear in `research/numbers.md` with a source URL and access date.
