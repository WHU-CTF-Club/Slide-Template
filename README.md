# Slide Template (reveal-md)

本项目的在线课件基于 reveal-md 生成。下面整理了模板结构、样式编辑、内容写作、编译与预览流程。

## 目录结构

- slides/
  - build # 生成/预览脚本
  - template.html # reveal-md 模板
  - custom.css # 全局自定义样式
  - dark.css # 深色主题覆盖
  - <lecture>.md # 讲义源文件
  - <lecture>/ # 讲义资源目录 (背景图/图片等)

建议新增讲义时遵循：

- 新建 slides/<lecture>.md
- 新建 slides/<lecture>/ 并放入图片、背景等资源

## 模板与样式

### 1) reveal-md 模板

模板文件：slides/template.html

- 负责加载 reveal.js 本体与插件 (markdown/highlight/notes/math)
- 会合并每个讲义 front matter 里的 revealOptions
- 支持传入自定义 cssPaths 和 scriptPaths

### 2) 全局样式

- slides/custom.css: 全局布局与排版
- slides/dark.css: 深色主题覆盖

讲义中通过 front matter 引入：

```yaml
css:
  - custom.css
  - dark.css
```

### 3) 讲义内样式

可以在单个讲义里写内联样式：

```html
<style>
  .my-box {
    border: 1px solid #ddd;
    padding: 12px;
  }
</style>
```

适合个别页面的特殊排版。

## 内容写作

### 1) 基础 front matter

```yaml
---
title: 课程标题
separator: <!-- s -->
verticalSeparator: <!-- v -->
theme: simple
highlightTheme: monokai-sublime
css:
  - custom.css
  - dark.css
revealOptions:
  transition: "slide"
  transitionSpeed: fast
  center: false
  slideNumber: "c/t"
  width: 1000
---
```

### 2) 分隔符

- 横向切换：`<!-- s -->`
- 纵向切换：`<!-- v -->`

示例：

```markdown
# Page 1

<!-- s -->

# Page 2

<!-- v -->

## Vertical Page 2-1
```

### 3) 背景图

使用 reveal 的 data-background：

```markdown
<!-- .slide: data-background="./<lecture>/background.png" -->
```

图片建议放在同名资源目录中，例如 slides/crypto-lec1/。

### 4) 多列布局

custom.css 内置了多列布局：

```html
<div class="mul-cols">
  <div class="col">左列内容</div>
  <div class="col">右列内容</div>
</div>
```

## 编译与预览

### 1) 预览单个讲义

在 slides 目录执行：

```bash
./build <lecture>.md
```

这会使用 reveal-md 的 watch 模式启动本地预览。

### 2) 生成静态文件

生成单个讲义：

```bash
./build build <lecture>.md
```

生成全部讲义：

```bash
./build build
```

构建产物默认输出到 slides/dist/<lecture>/。

### 3) 资源打包

脚本会自动把 slides/<lecture>/ 复制到对应的 dist/<lecture>/，确保背景图与图片可访问。

## 部署提示

GitHub Actions 中通过执行：

```bash
slides/build build
```

生成后将 slides/dist/\* 移动到站点目录的 site/slides，最终发布到 GitHub Pages。

## 常见约定

- 讲义文件名与资源目录名一致
- 统一使用 custom.css / dark.css 保证视觉风格一致
- 尽量使用 front matter 管理 revealOptions 与主题
