---
marp: true
theme: cpu
paginate: true
html: true
---

<!--
   CPU Marp template sample · the comment at the top of each page explains how
   that page is written (it doubles as a presenter note).
   Usage guide: docs/usage.md. Keep theme: cpu in the frontmatter.
   Only the cover uses h1; every other page starts at h2. Titles stay on one
   line. No emoji. Images go in with Marp's own sizing directives —
   ![height:720px](img) pinned by the side class, ![w:300](img) inline —
   with .columns divs for side-by-side layouts, never other HTML.
-->

<!-- Mermaid loader: turns fenced ```mermaid blocks into diagrams in the
     same window card as code blocks, in CPU brand colors. Diagrams render
     in CLI exports (PNG/PDF), HTML exports and `marp --preview` — every
     path that runs scripts; the VS Code preview strips document scripts
     (its own security policy) and shows the source card instead. Delete
     this block (and the demo page) for decks without diagrams. -->

<script src="https://cdn.jsdelivr.net/npm/mermaid@11/dist/mermaid.min.js"></script>
<script>
mermaid.initialize({
  startOnLoad: false,
  theme: 'base',
  themeVariables: {
    fontFamily: "'Noto Sans SC','PingFang SC','Hiragino Sans',sans-serif",
    fontSize: '24px',
    primaryColor: '#fdfaf0',
    primaryBorderColor: '#111111',
    primaryTextColor: '#111111',
    secondaryColor: '#f9dd74',
    secondaryBorderColor: '#111111',
    secondaryTextColor: '#111111',
    tertiaryColor: '#fdf6dd',
    tertiaryBorderColor: '#e3d5a8',
    tertiaryTextColor: '#111111',
    lineColor: '#111111',
    textColor: '#111111',
    edgeLabelBackground: '#f9dd74',
    clusterBkg: '#fdf6dd',
    clusterBorder: '#e3d5a8',
    actorBkg: '#fdfaf0',
    actorBorder: '#111111',
    actorTextColor: '#111111',
    actorLineColor: '#a3a3a3',
    signalColor: '#111111',
    signalTextColor: '#111111',
    noteBkgColor: '#f9dd74',
    noteBorderColor: '#111111',
    activationBkgColor: '#f9dd74',
    activationBorderColor: '#111111',
    sequenceNumberColor: '#111111',
    taskBkgColor: '#f9dd74',
    taskBorderColor: '#111111',
    taskTextColor: '#111111',
    todayLineColor: '#111111',
    gridColor: '#a3a3a3'
  }
});
const renderMermaid = () => {
  document.querySelectorAll('pre.mermaid, pre > code.language-mermaid').forEach((el) => {
    const pre = el.tagName === 'PRE' ? el : el.parentElement;
    const container = document.createElement('div');
    container.className = 'mermaid';
    container.textContent = pre.textContent.trim();
    pre.replaceWith(container);
  });
  mermaid.run();
};
if (document.readyState === 'loading') {
  document.addEventListener('DOMContentLoaded', renderMermaid);
} else {
  renderMermaid();
}
</script>

<!-- _class: lead -->
<!-- Cover: # main title (inside the yellow band) · ## subtitle · p speakers
     (<br> per line) + p date · ###/#### mega words bottom-right (outlined /
     solid; either can be dropped) -->

# Presentation Title Here

## Subtitle — occasion, audience, or one-line summary

Speaker One (President)<br>Speaker Two (VP, Tech Group)<br>Speaker Three (VP, Publicity & Ideation Group)

Computer Psycho Union · 1 January 2027

### OUTLINE

#### CPU 2026/27

---

<!-- _class: agenda -->
<!-- Agenda: ordered list of 2–6 items (9 at most; numbers 01–09 are generated,
     first row auto-highlighted); *italics* render as gray secondary text -->

## What we'll cover today

1. First Section *one-line note for the section*
2. Executive Team *the new team — who is who*
3. Activity Plan *key activities for the year*
4. Support & Discussion *where the School can help*

---

<!-- Regular content page (no class): the h2 title gets its rule and </> ·
     lists get yellow square markers · **bold** as the lead-in · nested lists
     are smaller and lighter -->

## 01 · Regular content slide

- **Bold lead-in** — one line of description text
- **Bold lead-in** — one line of description text
   - *nested note renders in gray*
- **Bold lead-in** — one line of description text

---

<!-- _class: roster -->
<!-- Roster page: yellow-headed table with black borders, zebra rows; the first
     column is fixed at 350px (fits name | role | duties) · inside a cell:
     **Name** + <br> + `email` + *ID* -->

## 02 · Roster table

| Member | Role | Key responsibilities |
| --- | --- | --- |
| **Name One**<br>`email1@nottingham.edu.cn` · *20999999* | President | duty · duty · duty |
| **Name Two**<br>`email2@nottingham.edu.cn` · *20999999* | VP, Tech Group | duty · duty · duty |

- *footnote line in gray italics*

---

<!-- _class: side -->
<!-- Side-image page: the image is a plain ![height:720px](image) line, put
     anywhere on the page — the theme pins it to the right edge at full
     height and keeps the text clear; a landscape image can use width:
     instead · ### tag blocks distribute vertically on their own · #### is
     the outlined mega word bottom-left -->

![height:720px](assets/poster.png)

## 03 · Side-image slide

### TAG BLOCK ONE

One short sentence under the tag.

### TAG BLOCK TWO

One short sentence under the tag.

#### MEGA

---

<!-- Regular content page with images: ![w:300]/![h:400] size an image
     (width:/height: long forms work the same) — no frame, no shrinking, it
     simply overflows the slide edge if too big · alone in its paragraph it
     is centered horizontally; in a .columns block it is centered
     vertically · the .columns block puts text and an image side by side -->

## 04 · Inline images

<div class="columns">
<div class="column">

- **Standalone image** — centered below text, sized by its directive
- **Side by side** — the `.columns` block lays text next to an image

</div>
<div class="column">

![w:300](assets/poster.png)

</div>
</div>

*Caption in gray — sizing comes from the directive, layout from the theme.*

---

<!-- Mermaid diagram: a fenced ```mermaid block (the loader script at the
     top of the file renders it) · same window card as code blocks, CPU
     brand colors come from the initialize() call · an unrendered diagram
     falls back to the source code card -->

## 05 · Mermaid diagram

```mermaid
graph LR
  A[Idea] --> B[Draft]
  B --> C{Review}
  C -->|ok| D[Ship]
  C -->|redo| B
```

---

<!-- _class: yellow -->
<!-- Section divider: ## outlined word top-right (all caps) · ### big white
     number · ## big black headline · p credit line at the bottom -->

## SECTION NAME

### 06

#### Section Headline

Credit line — Name One · Name Two · Name Three

---

<!-- _class: activities -->
<!-- Grouped timeline: ### yellow group tags each with a list, packed tighter
     than a regular page; good for around 3 groups -->

## 06 · Grouped timeline

### AUTUMN

- **Activity name** — one-line description
- **Activity name** — one-line description

### SPRING

- **Activity name** — one-line description

### ALL YEAR

- **Activity name** — one-line description

---

<!-- _class: todo -->
<!-- TODO page: ### tag blocks spread out vertically on their own; a list can
     follow the last sentence -->

## TODO

### ITEM ONE

What to arrange, and where.

### ITEM TWO

What to check, and when.

- Room A — purpose
- Room B — purpose

---

<!-- _class: yellow -->
<!-- Closing page: same structure as the section divider -->

## THANK YOU

### Q&A

#### Closing Headline

Closing line — Computer Psycho Union · 1 January 2027
