# cpu-style-marp-template

宁诺 CPU（Computer Psycho Union）的 Marp 幻灯片主题模板。

品牌视觉：CPU 黄 `#f7d447` + 墨黑 + 白 —— 瑞士海报风格，带蓝图虚线参考线、黄色标签块与描边 mega 大字。主题完整抽离自 2026-09-18 Dr Tesema 汇报用的 slides（经过逐页渲染验证）。

## 仓库结构

```text
themes/cpu.css    Marp 主题（全部样式，含 7 种页面类型）
template.md       示例文档：每种页面一页，页首注释即使用说明
assets/           示例素材（占位海报，替换为你自己的图）
.vscode/          VS Code Marp 插件主题注册 + cSpell 词典
```

## 快速开始

### VS Code

1. 安装 [Marp for VS Code](https://marketplace.visualstudio.com/items?itemName=marp-team.marp-vscode) 扩展；
2. 用 VS Code 打开本仓库（`.vscode/settings.json` 已把 `themes/cpu.css` 注册为主题）；
3. 新建 `slides.md`，frontmatter 写：

   ```markdown
   ---
   marp: true
   theme: cpu
   paginate: true
   ---
   ```

4. 打开 Markdown 预览即为所见即所得。

### 命令行（marp CLI）

```bash
npm i -g @marp-team/marp-cli

# 预览
marp slides.md --preview --theme-set themes/cpu.css

# 导出 PDF / PPTX / PNG
marp slides.md --theme-set themes/cpu.css --allow-local-files -o slides.pdf
```

> `--allow-local-files` 在引用本地图片（如侧边图）时必须加上；VS Code 预览不受此限制。

最快的方式：直接复制 `template.md` 开始改。

## 页面类型

每页用 `<!-- _class: xxx -->` 指令选择类型；`template.md` 中每种都有一页带注释的示例。

| class | 用途 | Markdown 结构 |
| --- | --- | --- |
| `lead` | 封面页 | `#` 主标题（黄色横幅内）· `##` 副标题 · 两个 `p`（出席人 + 日期）· `###`/`####` 右下 mega 字（描边 / 实心） |
| `agenda` | 议程页 | `##` 标题 + 有序列表（≤9 项，编号 01–09 自动生成，首行高亮，斜体为灰色副文本） |
| （无 class） | 普通内容页 | `##` 标题（自动带虚线与 `</>` 符号）+ 列表（黄色方块标记，嵌套列表更小） |
| `roster` | 名单 / 表格页 | `##` + 表格（黄头黑框，首列固定 350px；单元格内 **名字** + `<br>` + `` `邮箱` `` + ` · ` + `*学号*`） |
| `side` | 侧边图页 | `##` + `###` 标签块若干（自动垂直均分）+ `####` 左下 mega 字；图片用页内 scoped style 指定（见下） |
| `yellow` | 章节分隔 / 结束页 | `##` 右上白描边大字 · `###` 白色大编号 · `####` 黑色大标题 · `p` 底部署名 |
| `activities` | 分组时间线页 | `##` + 若干 `###` 分组标签 + 各自的列表（比普通页紧凑） |
| `todo` | 待办页 | `##` + `###` 标签块（自动垂直均分），可接列表 |

### 侧边图页（side）

图片是**纯右侧背景**：右贴边、满高、原始比例、不占布局空间，文字列通过 `--side-gap` 避让。在幻灯片内加 scoped style：

```markdown
<!-- _class: side -->

<style scoped>
section {
  --side-gap: 540px;
  background: #ffffff url('assets/poster.png') no-repeat right center / auto 100%;
}
</style>

## 03 · Side-image slide

### TAG BLOCK ONE

One short sentence under the tag.

#### MEGA
```

`--side-gap` = 图片在 1280px 宽画布上占的宽度 + 余量。竖版海报（约 0.7 宽高比）满高时宽约 509px，用 540；窄易拉宝（约 0.44）宽约 320px，用 360。

## 设计 token

| token | 值 | 用途 |
| --- | --- | --- |
| `--yellow` | `#f7d447` | CPU 品牌黄：横幅、标签、方块标记、表格头、分隔页底色 |
| `--yellow-soft` | `#f9dd74` | 次级黄：嵌套列表标记、议程编号 |
| `--ink` | `#111111` | 正文黑 |
| `--gray` | `#a3a3a3` | 灰色副文本（斜体 `*text*` 被重定义为灰色正体） |
| `--grid` | `#e3d5a8` | 蓝图虚线（左右参考线、标题下分隔线） |
| `--sans` | Noto Sans SC, PingFang SC, … | 正文字体 |
| `--display` | Archivo Black, Arial Black, … | mega 大字 / 大编号 |
| `--mono` | ui-monospace, SF Mono, … | 邮箱、页码、`</>` 符号 |

改色只需替换 `:root` 中的变量；正文 `p`、列表、表格等基础样式全部在 `themes/cpu.css`。

## 约定与注意

- 全套**只有封面页用 `#`**（h1），其余页面从 `##` 起，标题层级不跳级；
- 标题保持单行；不建议使用 emoji（视觉锚点由大编号、黄色标签承担）；
- `*斜体*` 不是斜体，是灰色小号副文本——用于备注、脚注、议程副标题；
- 议程编号格式为 `0` + 计数器，**最多 9 项**；
- 图片引用本地文件时，CLI 导出必须加 `--allow-local-files`；
- 字体经 Google Fonts 在线加载（Archivo Black + Noto Sans SC），离线环境自动回退到系统字体栈；
- Markdown 规范：3 空格缩进嵌套列表、代码块声明语言——`.markdownlint.json` 已配好（MD013 关闭、MD033 白名单含 `style`/`br`）。

## 从旧 slides.md 迁移

把原文件末尾的 `<style>…</style>` 块整段删除，frontmatter 加 `theme: cpu`，`_class: recruit hf` / `recruit banner` 改为 `_class: side` 并按上文加 scoped style 指定图片即可，其余 Markdown 无需改动。
