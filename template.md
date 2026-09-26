---
marp: true
theme: cpu
paginate: true
---

<!--
   CPU Marp 模板示例 · 每页开头的注释即该页使用说明（也是演讲者备注）
   frontmatter 中 theme: cpu 必须保留；VS Code 需注册主题（本仓库 .vscode/ 已配好）。
   全套仅封面页用 h1，其余页面一律 h2 起；标题保持单行；不建议使用 emoji。
-->

<!-- _class: lead -->
<!-- 封面页：h1 主标题（黄色横幅内）· h2 副标题 · p 出席人（<br> 分行）+ p 日期 ·
     h3 右下描边 mega 字 · h4 右下实心 mega 字（可省略其一） -->

# Presentation Title Here

## Subtitle — occasion, audience, or one-line summary

Speaker One (President)<br>Speaker Two (VP, Tech Group)<br>Speaker Three (VP, Publicity & Ideation Group)

Computer Psycho Union · 1 January 2027

### OUTLINE

#### CPU 2026/27

---

<!-- _class: agenda -->
<!-- 议程页：有序列表 2–6 项（不超过 9 项，编号 01–09 自动生成，首行自动黄色高亮）；
     斜体 *text* 渲染为灰色副文本 -->

## What we'll cover today

1. First Section *one-line note for the section*
2. Executive Team *the new team — who is who*
3. Activity Plan *key activities for the year*
4. Support & Discussion *where the School can help*

---

<!-- 普通内容页（无需 class）：h2 标题自动带虚线与 </> 符号 · 列表为黄色方块标记 ·
     **粗体**作引导词 · 嵌套列表更小更浅 -->

## 01 · Regular content slide

- **Bold lead-in** — one line of description text
- **Bold lead-in** — one line of description text
   - *nested note renders in gray*
- **Bold lead-in** — one line of description text

---

<!-- _class: roster -->
<!-- 名单页：表格黄头黑框、隔行浅黄；首列固定 350px（适合 名字|角色|职责 三列）·
     单元格内 **名字**<br>`邮箱` · *学号* 的组合 -->

## 02 · Roster table

| Member | Role | Key responsibilities |
| --- | --- | --- |
| **Name One**<br>`email1@nottingham.edu.cn` · *20999999* | President | duty · duty · duty |
| **Name Two**<br>`email2@nottingham.edu.cn` · *20999999* | VP, Tech Group | duty · duty · duty |

- *footnote line in gray italics*

---

<!-- _class: side -->
<!-- 侧边图页：图片是纯右侧背景（右贴边、满高、不占布局空间），需在本页加 scoped
     <style> 指定图片与 --side-gap（图片宽度 + 余量，窄图可用 360px）·
     h3 黄标签块自动垂直均分 · h4 为左下描边 mega 字 -->

<style scoped>
section {
  --side-gap: 540px;
  background: #ffffff url('assets/poster.png') no-repeat right center / auto 100%;
}
</style>

## 03 · Side-image slide

### TAG BLOCK ONE

One short sentence under the tag.

### TAG BLOCK TWO

One short sentence under the tag.

#### MEGA

---

<!-- _class: yellow -->
<!-- 章节分隔页：h2 右上白色描边大字（全大写英文）· h3 白色大编号 ·
     h4 黑色大标题 · p 底部署名行 -->

## SECTION NAME

### 04

#### Section Headline

Credit line — Name One · Name Two · Name Three

---

<!-- _class: activities -->
<!-- 分组时间线页：h3 黄标签分组 + 列表，比普通页更紧凑，适合 3 组左右的清单 -->

## 04 · Grouped timeline

### AUTUMN

- **Activity name** — one-line description
- **Activity name** — one-line description

### SPRING

- **Activity name** — one-line description

### ALL YEAR

- **Activity name** — one-line description

---

<!-- _class: todo -->
<!-- TODO 页：h3 标签块自动垂直均分，句后可接列表 -->

## TODO

### ITEM ONE

What to arrange, and where.

### ITEM TWO

What to check, and when.

- Room A — purpose
- Room B — purpose

---

<!-- _class: yellow -->
<!-- 结束页：结构与章节分隔页相同 -->

## THANK YOU

### Q&A

#### Closing Headline

Closing line — Computer Psycho Union · 1 January 2027
