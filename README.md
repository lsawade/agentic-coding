# Agentic AI for Research — slides

Marp deck for the Princeton Research Computing session on agentic AI (two presenters, ~42 minutes, 35 slides).
The talk outline lives in the shared Claude Doc; this repo is the deck itself.

## Preview and build

```bash
npm install          # once; installs Marp CLI
npm run dev          # live preview server for slides.md (http://localhost:8080)
npm run build        # dist/index.html + dist/assets (open in any browser; press P for presenter view with notes)
npm run pdf          # dist/slides.pdf  (needs Chrome, Edge or Chromium installed)
npm run png          # review/slide.NNN.png, one image per slide, for a quick visual pass
```

In VS Code, install the "Marp for VS Code" extension; `.vscode/settings.json` already points it at the
theme and enables HTML, so `slides.md` previews correctly without any setup.

Every push to `main` runs the GitHub Action in `.github/workflows/build.yml`, which uploads
`index.html` and `slides.pdf` as a build artifact.

## Layout

| Path | What |
|---|---|
| `slides.md` | the whole deck, one file; sections are marked with `<!-- ===== N · title ===== -->` comments |
| `themes/princeton.css` | the theme (orange `#E87722`, black, white; seal embedded; classes documented in `CLAUDE.md`) |
| `assets/diagrams/*.svg` | one hand-written SVG per schematic |
| `assets/logo/` | the Princeton seal |
| `starter-kit/` | the template folder the audience clones (slide 31 links to it) |
| `research/numbers.md` | every number in the deck with its source URL and access date |

## Presenters

Congyue Cui and Lucas Sawade. The natural split is slides 1–19 (bridge, model landscape, tokens and delegation,
reviewing agent output) and slides 20–35 (workspace setup, working patterns, starter kit, discussion); who takes
which half is decided on the day. The handoff is slide 19, on the line "Verification is the hardest job to delegate."
Presenter notes are on every slide: open `dist/index.html` and press `P`.

## Editing conventions

- One slide per `---` block. Keep the `<!-- _header: "N · Section" -->` line on every content slide.
- Tips from colleagues on campus are quoted exactly as submitted (typos included) in `<div class="tip">` cards.
- A slide must not overflow 1280×720: run `npm run png` and look before you push.
- Numbers go in `research/numbers.md` first, with a source, then on the slide.

## Still to do by hand

- Decide live whether slide 21 (tour of `.claude/`) becomes a 60-second screen share.
