# Making slides with this template

First install the tooling: the [Marp for VS Code](https://marketplace.visualstudio.com/items?itemName=marp-team.marp-vscode) extension, or `npm i -g @marp-team/marp-cli` for the command line.

Every deck starts with this frontmatter:

```markdown
---
marp: true
theme: cpu
paginate: true
---
```

## Where to write

**Inside this repo**: copy `template.md`, rename it, and start editing. The comment at the top of each page explains how that page is written; left in place it becomes a presenter note, and deleting it changes nothing visually. Opening the repo in VS Code gives you a live preview — `.vscode/` already registers the theme. Export with:

```bash
marp slides.md --theme-set themes/cpu.css --allow-local-files -o slides.pdf
```

**Inside your own project**: copy `themes/cpu.css` over (into the project's `themes/`, say). Point the CLI at the theme file when rendering; in VS Code, add one line to the project's `.vscode/settings.json`:

```json
{
  "markdown.marp.themes": ["themes/cpu.css"]
}
```

If your deck references local images (the side-image pages do), exports must pass `--allow-local-files` or the images won't come through. The VS Code preview doesn't have this restriction.

## Slide types

Pick a layout with `<!-- _class: xxx -->` at the top of the page. Eight of them:

| Class | For | How to write it |
| --- | --- | --- |
| `lead` | Cover | `#` main title (sits in the yellow band), `##` subtitle, two paragraphs (speakers, date), `###`/`####` the two mega words bottom-right — one outlined, one solid |
| `agenda` | Agenda | `##` plus an ordered list; numbers from 01 are generated, first row gets a full highlight |
| no class | Regular content | `##` plus a list; the title brings its own rule and `</>` |
| `roster` | People tables | `##` plus a table; first column is fixed at 350px, just right for name + email + student ID |
| `side` | Side image | `##` plus a few `###` tag blocks with one sentence each, `####` is the mega word bottom-left; the image works differently, see below |
| `yellow` | Section dividers, closing | `##` outlined word, `###` number, `####` headline, last line a credit |
| `activities` | Grouped lists | `##` plus several `###` group tags, each with its own list, packed tighter than a regular page |
| `todo` | Action items | `##` plus `###` tag blocks; blocks spread out automatically |

### Side images

The image is a pure background pinned to the right edge: full height, original ratio, no layout space taken. Text keeps clear through `--side-gap`, set by a scoped style on the page:

```html
<style scoped>
section {
  --side-gap: 540px;
  background: #ffffff url('assets/poster.png') no-repeat right center / auto 100%;
}
</style>
```

`--side-gap` is the image width plus a little margin: a regular portrait poster is about 509px wide at full height, so use 540; a narrow roll-up banner is about 320px, so use 360.

## Writing conventions

- Only the cover uses `#`; every other page starts at `##`, and heading levels don't skip;
- Titles stay on one line; no emoji — visual emphasis is the job of the big numbers and yellow tags;
- `*italics*` render as small gray text for notes and footnotes, not emphasis;
- The agenda holds at most 9 items — beyond that the numbering (a `0` plus the counter) breaks;
- Nested lists indent 3 spaces and code fences declare a language; `.markdownlint.json` is already set up for both;
- Don't drop a global `<style>` into a deck to tweak the theme — that path has bitten us (see the implementation README). Change the theme file itself.

## Migrating an old slides.md

Delete the whole `<style>…</style>` block at the end of the file, add `theme: cpu` to the frontmatter, replace `_class: recruit hf` and `recruit banner` with `_class: side`, point the scoped style at your image as shown above, and leave the rest of the content alone.

## Letting Claude write it

The repo ships an agent skill. Install it with the [skills CLI](https://github.com/vercel-labs/skills):

```bash
npx skills add CompPsyUnion/cpu-style-marp-template          # current project
npx skills add CompPsyUnion/cpu-style-marp-template -g       # all your projects
```

It symlinks the skill into every agent it detects — Claude Code, Cursor, Codex and friends. After that, just say "make a CPU deck with the template".
