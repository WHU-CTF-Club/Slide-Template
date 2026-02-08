# Slide Template (reveal-md)

基于 reveal-md 构建的幻灯片模板，支持本地预览和自动部署到 GitHub Pages。

## 快速开始

### 环境要求

- Node.js (推荐 v18+)
- npm
- reveal-md

### 安装依赖

```bash
npm install -g reveal-md
```

### 本地预览

在 `slides` 目录下运行：

```bash
# Linux/macOS
./build demo.md

# Windows PowerShell
wsl ./build demo.md
# 或
bash build demo.md
```

浏览器会自动打开 `http://localhost:1948`，修改 md 文件时会自动刷新。

---

## 创建新的幻灯片

### 1. 创建 Markdown 文件

在 `slides/` 目录下新建 `your-slide.md`：

```markdown
---
title: 你的幻灯片标题
theme: simple
highlightTheme: monokai-sublime
separator: <!-- s -->
verticalSeparator: <!-- v -->
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

# 第一页

这是你的第一页内容

<!-- s -->

## 第二页

这是你的第二页内容
```

### 2. Front Matter 配置说明

| 字段                | 说明                                 | 推荐值                   |
| ------------------- | ------------------------------------ | ------------------------ |
| `title`             | 幻灯片标题                           | 自定义                   |
| `theme`             | reveal.js 主题                       | `simple`                 |
| `highlightTheme`    | 代码高亮主题                         | `monokai-sublime`        |
| `separator`         | 横向切换分隔符                       | `<!-- s -->`             |
| `verticalSeparator` | 纵向切换分隔符                       | `<!-- v -->`             |
| `css`               | 自定义 CSS 文件列表                  | `[custom.css, dark.css]` |
| `revealOptions`     | reveal.js 配置项（过渡效果、尺寸等） | 见示例                   |

### 3. 幻灯片分页

- **横向切换**（新章节）：使用 `<!-- s -->`
- **纵向切换**（子章节）：使用 `<!-- v -->`

```markdown
# 章节一

内容

<!-- s -->

# 章节二

内容

<!-- v -->

## 章节二的子页面

子内容
```

### 4. 添加图片

**方法 1：创建资源目录（推荐）**

```bash
mkdir slides/your-slide
# 将图片放入 slides/your-slide/ 目录
```

在 Markdown 中引用：

```markdown
![图片描述](your-slide/image.png)
```

**方法 2：背景图**

```markdown
<!-- .slide: data-background="your-slide/background.png" -->

# 带背景的幻灯片
```

### 5. 多列布局

```html
<div class="mul-cols">
  <div class="col">- 左列内容 - 列表项</div>
  <div class="col">- 右列内容 - 列表项</div>
</div>
```

### 6. 代码块

````markdown
​`python
def greet(name: str) -> str:
    return f"Hello, {name}!"
​`
````

### 7. 数学公式

**行内公式**：`$a^2 + b^2 = c^2$`

**块级公式**：

```markdown
$$
\sum_{i=1}^{n} i = \frac{n(n+1)}{2}
$$
```

---

## 目录结构

```
slides/
├── build              # 本地预览/构建脚本
├── template.html      # reveal-md 模板
├── custom.css         # 全局样式（字体、布局）
├── dark.css           # 主题颜色配置
├── icon.png           # 网站图标
├── demo.md            # 示例幻灯片
└── your-slide/        # 幻灯片资源目录
    ├── image1.png
    └── background.png
```

---

## 样式自定义

### 修改主题颜色

编辑 `slides/dark.css`：

```css
:root {
  --r-background-color: #0a0e27; /* 幻灯片背景 */
  --r-main-color: #ffffff; /* 文字颜色 */
  --r-link-color: #64b5f6; /* 链接颜色 */
}
```

### 修改字体

编辑 `slides/custom.css`：

```css
@import url("https://fonts.googleapis.com/css2?family=Noto+Serif+SC:wght@400;700&display=swap");

:root {
  --r-main-font: "Noto Serif SC", serif;
  --r-code-font: "JetBrains Mono", monospace;
}
```

---

## 部署到 GitHub Pages

### 自动部署

1. Push 代码到 `master` 分支：

   ```bash
   git add .
   git commit -m "Update slides"
   git push origin master
   ```

2. GitHub Actions 会自动：
   - 安装 reveal-md
   - 编译所有 `.md` 文件
   - 部署到 GitHub Pages

3. 访问 `https://slide.jwmc.top` 查看幻灯片

### 配置自定义域名

在 GitHub Repo Settings → Pages：

- 确认 Source 为 **GitHub Actions**
- Custom domain 会自动设置为 `slide.jwmc.top`

---

## 常见问题

### 本地预览报错

**问题**：`reveal-md: command not found`

**解决**：

```bash
npm install -g reveal-md
```

### 图片无法显示

**原因**：图片路径不正确

**解决**：

- 确保图片在 `slides/your-slide/` 目录下
- Markdown 中使用相对路径：`your-slide/image.png`

### 样式不生效

**原因**：未在 front matter 中引入 CSS

**解决**：

```yaml
css:
  - custom.css
  - dark.css
```

---

## 参考

- [reveal-md 文档](https://github.com/webpro/reveal-md)
- [reveal.js 文档](https://revealjs.com/)
- [demo.md](slides/demo.md) 示例
