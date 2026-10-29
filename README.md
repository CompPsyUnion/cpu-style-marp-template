# cpu-style-marp-template

The Marp slide theme for CPU (Computer Psycho Union) at UNNC.

To make slides, read [docs/usage.md](docs/usage.md). To let an agent do it, install the skill:

```bash
npx skills add CompPsyUnion/cpu-style-marp-template
```

That is the [skills CLI](https://github.com/vercel-labs/skills) — it symlinks the skill into every agent it detects (Claude Code, Cursor, Codex, …). Add `-g` for all projects, `-a claude` to target one agent, `--copy` if you prefer real files over symlinks. This README is about how the theme itself is put together, for whoever maintains it.

## Repository layout

```bash
tree -a --dirsfirst -I .git
.
├── .agents
│   └── skills
│       └── cpu-marp
│           └── SKILL.md             # agent skill body, cross-agent location
├── .claude
│   └── skills -> ../.agents/skills  # symlink so Claude Code picks it up in-repo
├── .vscode
│   └── settings.json                # Marp theme registration + cSpell dictionary
├── assets
│   └── poster.png                   # placeholder poster for the image demos
├── docs
│   └── usage.md                     # usage guide
├── themes
│   └── cpu.css                      # the theme — all styles live in this one file
├── .editorconfig                    # documentation standards
├── .markdownlint.json               # (paired with the line above)
├── .gitignore
├── LICENSE
├── README.md
└── template.md                      # sample deck, one page per slide type
```

## How the theme is organized

`themes/cpu.css` is a standalone Marpit theme (first line `/* @theme cpu */`), in four layers from top to bottom:

1. `:root` variables. Colors and fonts are defined here and nowhere else;
2. Base layer. Canvas size, guide lines, page numbers, plus default styles for paragraphs and inline elements. A standalone theme has no Marp default theme to fall back on, so all of this has to be written out;
3. Shared elements. Things every page runs into: the `h2` title (yellow, dashed underline, a `</>` hanging in the top-right corner), `h3` yellow tags, square list markers, tables;
4. Page classes. Layout rules under `section.<class>`, one class per slide type.

A few techniques worth knowing:

- Sparse pages (`side`, `todo`) use `display: flex; flex-direction: column` with `margin-top: auto` on the info blocks, so leftover space is split evenly between blocks instead of piling everything at the top and leaving a hole in the middle;
- The mega words are hollow letters made with `-webkit-text-stroke` and `color: transparent` (cover `h3`, divider `h2`, side-image `h4`); the cover `h4` is solid yellow;
- Images are ordinary inline images sized with Marp's `w:` / `h:` directives — unframed and never shrunk: the directive size is exact, and an oversized image simply overflows the slide edge. An image alone in its paragraph (below text) is centered horizontally; a `.columns` / `.column` div pair (as in the weekly-session decks) splits an area into two equal, vertically centered columns; the `side` class pins the page's image to the right edge at full height and caps the text column width, so nothing can overlap;
- Mermaid diagrams: a fenced `mermaid` block plus the loader `<script>` at the top of `template.md`. The theme draws the rendered diagram in the same window card as `pre` (one shared `pre, div.mermaid` rule), and the brand colors go in through `mermaid.initialize`'s `themeVariables` inside that script;
- The org name in the cover's top-right sits on `section.lead h2::after`. Why not `section::after` — see the pitfalls below.

## Design tokens

| Variable | Value | Used for |
| --- | --- | --- |
| `--yellow` | `#f7d447` | Brand yellow: banner, tags, list markers, table heads, divider pages |
| `--yellow-soft` | `#f9dd74` | Secondary yellow: nested list markers, agenda numbers |
| `--ink` | `#111111` | Body text |
| `--gray` | `#a3a3a3` | Secondary text (italics redefined as gray upright text) |
| `--grid` | `#e3d5a8` | Dashed guide lines, the rule under titles |
| `--sans` | Noto Sans SC, PingFang SC, … | Body |
| `--display` | Archivo Black, Arial Black, … | Mega words, big numbers |
| `--mono` | ui-monospace, SF Mono, … | Emails, page numbers, `</>` |

Recolors and font swaps only touch `:root`.

## Pitfalls we hit

Worth knowing before changing the theme — each of these was tracked down in actual renders:

1. Marpit reserves `section::before/::after` for pagination and strips literal `content` from `::after`. So text like the org name never paints if written into `section::after`; it has to ride on another pseudo-element — the theme uses `h2::after`. The old slides.md had its CSS inlined at the end of the file, and the empty rules left behind after content stripping took the page numbers and the cover banner down with it — they all vanished from PDF exports. Loading the theme as a file via `--theme-set` makes the whole problem go away.
2. Any `section::after` rule without a `content` property kills page-number rendering. To restyle the number on a specific page, follow `section.yellow::after` and repeat the attr() content; the cover hides its number with `color: transparent`, again with content present.
3. CLI exports referencing local images must pass `--allow-local-files`, otherwise the images are silently blocked by the security policy with nothing but a warning to tip you off.
4. Fonts load from Google Fonts; offline you get the system fallbacks, with `Arial Black` standing in when `Archivo Black` is unavailable.
5. `![bg]` background images render through Marp's advanced background layer (separate sections inside the slide's SVG), and that layer does not behave identically everywhere: in one pipeline a `![bg right:40%]` split left the text squeezed into a narrow column while another rendered it fine, and on `_class: yellow` pages the photo vanishes outright. The template therefore pins all images as ordinary inline images — same pixels in CLI, PDF and the VS Code preview — and avoids `![bg]` entirely.
6. The VS Code preview runs no custom scripts, so mermaid blocks stay as their source card there — the extension plugs into VS Code's built-in Markdown preview, which strips document scripts; nothing a deck can change. The rendered diagram appears in CLI exports (PNG and PDF — both verified pixel-wise), in HTML exports opened in a browser (verified headless), and in `marp --preview`'s live-reload server; the CLI renderer waits long enough for mermaid's async draw.

## Adding a slide type

Add a `section.<class>` rule block to `themes/cpu.css` — copy `todo` for a plain layout, `side` for one with an image. Any `::after` rule must carry content (see above). Then sync three places: an example page in `template.md`, a row in the `docs/usage.md` table, a row in the SKILL.md quick reference. Run the regression below before committing.

## Regression checklist

```bash
marp template.md --theme-set themes/cpu.css --allow-local-files -o /tmp/tpl.pdf
```

Check page by page (pixel sampling beats squinting at a clean export):

- Cover: yellow band `#f7d447` on top, org name top-right, mega words bottom-right;
- Agenda: first row highlighted yellow;
- Roster: yellow table head;
- Side-image page: poster full height at the right edge, text column clear of it with a comfortable gap;
- Inline-image page: two `.columns` columns, the image unframed and centered in its column, gray caption below;
- Mermaid page: a drawn diagram inside the window card, not the source fallback;
- Both divider pages solid `#f7d447`;
- Page number bottom-right from page 2 on, none on the cover;
- `npx markdownlint-cli README.md docs/usage.md template.md` passes.
