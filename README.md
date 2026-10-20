# Agentic AI for Research — slides

Marp deck for the Princeton McGraw Center session (two presenters, ~42 minutes, 34 slides).
The talk outline lives in the shared Claude Doc; this repo is the deck itself.

## Preview and build

```bash
npm install          # once; installs Marp CLI
npm run dev          # live preview server for slides.md (http://localhost:8080)
npm run build        # dist/index.html  (open in any browser; press P for presenter view with notes)
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
| `starter-kit/` | the template folder the audience clones (slide 30 links to it) |
| `research/numbers.md` | every number in the deck with its source URL and access date |

## Presenters

Presenter A: slides 1–18 (bridge, model landscape, tokens and delegation, your name is on it).
Presenter B: slides 19–34 (workspace setup, working patterns, starter kit, discussion).
The handoff is slide 18, on the line "Verification is the job you can't delegate."
Presenter notes are on every slide: open `dist/index.html` and press `P`.

## Editing conventions

- One slide per `---` block. Keep the `<!-- _header: "N · Section" -->` line on every content slide.
- Campus tips are quoted exactly as submitted (typos included) in `<div class="tip">` cards.
- A slide must not overflow 1280×720: run `npm run png` and look before you push.
- Numbers go in `research/numbers.md` first, with a source, then on the slide.

## Still to do by hand

- Presenter names on slide 1.
- Optional screenshot from the whisper+claude session on slide 2 (`assets/bridge.png`).
- Decide live whether slide 20 (tour of `.claude/`) becomes a 60-second screen share.
