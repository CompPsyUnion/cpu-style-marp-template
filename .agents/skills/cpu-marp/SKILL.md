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

The frontmatter is always the same three lines: `marp: true`, `theme: cpu`, `paginate: true`. If the user works in VS Code, also register the theme in the project's `.vscode/settings.json` with `"markdown.marp.themes": ["themes/cpu.css"]`.

**Write.** Copy the skeleton from the template repo's `template.md` and pick classes from the quick reference below. For the text: all English unless the user says otherwise, no emoji, `#` only on the cover, titles on one line, `*italics*` as small gray notes. In roster tables, emails go in inline code and student IDs in italics.

**Render and check.** Never skip this:

```bash
marp slides.md --theme-set themes/cpu.css --allow-local-files -o slides.pdf
```

Go over every page: cover band and mega words present; agenda's first row highlighted; table heads yellow; side image full height with text clear of it; page number bottom-right from page 2 on and none on the cover; nothing overflowing or leaving a big blank patch. Finish with `npx markdownlint-cli slides.md`.

## Quick reference

| Class | How to write it |
| --- | --- |
| `lead` | `#` title, `##` subtitle, two paragraphs (speakers, date), `###`/`####` mega words |
| `agenda` | `##` plus an ordered list, 9 items at most |
| no class | `##` plus a list |
| `roster` | `##` plus a table (first column: name, email, ID) |
| `side` | `##` plus `###` tag blocks, `####` mega word, image as below |
| `yellow` | `##` outlined word, `###` number, `####` headline, `p` credit |
| `activities` | `##` plus `###` group tags, each with a list |
| `todo` | `##` plus `###` tag blocks |

Side images use a scoped style on the page; `--side-gap` is the image width plus margin (around 540 for posters, 360 for narrow banners):

```html
<style scoped>
section {
  --side-gap: 540px;
  background: #ffffff url('assets/poster.png') no-repeat right center / auto 100%;
}
</style>
```

## Don't step on these

- Never inline the theme into a deck's `<style>`. Marpit strips literal `content` from `section::after`, and PDF exports lose the cover band, the org name and the page numbers all at once. The theme only loads via `--theme-set` or extension registration;
- Never write a `section::after` rule without `content` — page-number rendering dies with it. To restyle a number, follow `section.yellow::after` in the theme and repeat the attr() content;
- Local images in exports require `--allow-local-files`;
- The agenda tops out at 9 items.

More in the template repo: usage in `docs/usage.md`, implementation details and pitfall backstories in `README.md`.
