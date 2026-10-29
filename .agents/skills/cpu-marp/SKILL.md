---
name: cpu-marp
description: Create CPU (Computer Psycho Union) branded Marp presentations using the cpu-style-marp-template theme. Use when the user asks for CPU slides, a CPU deck/宣讲/汇报 PPT, or any Marp presentation that should follow the CPU visual style.
---

# Making CPU decks with the template

The template repo is `cpu-style-marp-template`, locally at `~/Documents/GitHub/CompPsyUnion/cpu-style-marp-template` — clone it if that path is missing.

## Workflow

**Set up.** Skip if the project already has `themes/cpu.css`:

```bash
mkdir -p <project>/themes
cp ~/Documents/GitHub/CompPsyUnion/cpu-style-marp-template/themes/cpu.css <project>/themes/
```

The frontmatter is always the same four lines: `marp: true`, `theme: cpu`, `paginate: true`, `html: true` (keeps raw HTML — the mermaid loader script, `pre.mermaid` blocks, `.columns` divs — alive in every pipeline). If the user works in VS Code, also register the theme in the project's `.vscode/settings.json` with `"markdown.marp.themes": ["themes/cpu.css"]`.

**Write.** Copy the skeleton from the template repo's `template.md` and pick classes from the quick reference below. For the text: all English unless the user says otherwise, no emoji, `#` only on the cover, titles on one line, `*italics*` as small gray notes. In roster tables, emails go in inline code and student IDs in italics. Place images with Marp's sizing directives — `![height:720px](img)` on side pages, `![w:300](img)` inline — never HTML `<img>`.

**Render and check.** Never skip this:

```bash
marp slides.md --theme-set themes/cpu.css --allow-local-files -o slides.pdf
```

Go over every page: cover band and mega words present; agenda's first row highlighted; table heads yellow; side image full height with text clear of it; the mermaid page shows a drawn diagram, not its source; page number bottom-right from page 2 on and none on the cover; nothing overflowing or leaving a big blank patch. Finish with `npx markdownlint-cli slides.md`.

## Quick reference

| Class | How to write it |
| --- | --- |
| `lead` | `#` title, `##` subtitle, two paragraphs (speakers, date), `###`/`####` mega words |
| `agenda` | `##` plus an ordered list, 9 items at most |
| no class | `##` plus a list |
| `roster` | `##` plus a table (first column: name, email, ID) |
| `side` | `##` plus `###` tag blocks, `####` mega word, `![height:720px](img)` anywhere on the page |
| `yellow` | `##` outlined word, `###` number, `####` headline, `p` credit |
| `activities` | `##` plus `###` group tags, each with a list |
| `todo` | `##` plus `###` tag blocks |

Images are ordinary Markdown images sized with Marp's directives — `w:` / `h:` (long forms `width:` / `height:`) — never HTML `<img>` or a scoped `<style>`. Side image, one line anywhere on a `_class: side` page (the theme pins it right at full height):

```markdown
![height:720px](assets/poster.png)
```

Inline images: `![w:300](img.png)`; alone in a paragraph they are centered horizontally, in a `.columns` block vertically — unframed and never shrunk (a too-big image simply overflows the slide edge). Text beside an image: a `<div class="columns">` with two `<div class="column">` children (see `template.md` page 04).

Diagrams: fenced `mermaid` blocks plus the loader `<script>` kept from the template's top render in the code-block card with brand colors — in CLI and HTML exports; the VS Code preview runs no scripts and shows the source card.

## Don't step on these

- Never inline the theme into a deck's `<style>`. Marpit strips literal `content` from `section::after`, and PDF exports lose the cover band, the org name and the page numbers all at once. The theme only loads via `--theme-set` or extension registration;
- Never write a `section::after` rule without `content` — page-number rendering dies with it. To restyle a number, follow `section.yellow::after` in the theme and repeat the attr() content;
- Local images in exports require `--allow-local-files`;
- Never place images with HTML `<img>` or a scoped `<style>` — use the `![h:]` / `![w:]` directives above, and skip `![bg]` entirely: its background layer renders differently between the VS Code preview and CLI/PDF exports (the split variant has squeezed text into a narrow column in the preview), and on `_class: yellow` pages the photo vanishes;
- The agenda tops out at 9 items.

More in the template repo: usage in `docs/usage.md`, implementation details and pitfall backstories in `README.md`.
