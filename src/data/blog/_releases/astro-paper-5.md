---
pubDatetime: 2025-03-08T08:18:19.693Z
title: AstroPaper 5.0
slug: astro-paper-v5
featured: true
ogImage: ../../../assets/images/AstroPaper-v5.png
tags:
  - release
description: "AstroPaper v5：保持简洁外观，内部更新。"
---

终于，期待已久的 AstroPaper v5 终于来了。AstroPaper v5 延续了简洁明了的外观，但在底层进行了重大更新。

![AstroPaper v5](@/assets/images/AstroPaper-v5.png)

## Table of contents

## 主要变更

### 升级至 Astro v5 [#455](https://github.com/satnaing/astro-paper/pull/455)

AstroPaper 现已搭载 Astro v5，带来了其全部新特性与性能改进。

### Tailwind v4

AstroPaper 已升级至 Tailwind v4，其中包含了许多底层的样式变更。`tailwind.config.js` 文件已被移除，现在所有的配置都位于 `src/styles/global.css` 文件中。与排版相关的样式已被提取并移至 `src/styles/typography.css`。

由于 TailwindCSS v4 的新行为，组件内 `<style>` 块中的样式已被移除，并替换为内联的 Tailwind 类。

此外，整个用户界面的调色板也已更新。新的调色板现在仅包含五种颜色：

```css
:root,
html[data-theme="light"] {
  --background: #fdfdfd;
  --foreground: #282728;
  --accent: #006cac;
  --muted: #e6e6e6;
  --border: #ece9e9;
}

html[data-theme="dark"] {
  --background: #212737;
  --foreground: #eaedf3;
  --accent: #ff6b01;
  --muted: #343f60bf;
  --border: #ab4b08;
}
```

### 移除 React + Fuse.js，转而采用 Pagefind 搜索

在旧版本中，搜索功能和 OG 图片生成使用了 React.js 和 Fuse.js。在 AstroPaper v5 中，React.js 已被移除，并由静态网站搜索工具 [Pagefind](https://pagefind.app/) 取代。

搜索体验与旧版几乎完全相同，但得益于 Pagefind，现在所有内容——而不仅仅是标题和描述——都会被索引和搜索。

在开发模式下使用 Pagefind 的灵感来源于[这篇博客文章](https://chrispennington.blog/blog/pagefind-static-search-for-astro-sites/)。

### 更新了导入别名

导入别名已从 `@directory` 更新为 `@/directory`，这意味着您现在需要像这样导入：

```astro
---
import { slugifyStr } from "@/utils/slugify";
import IconHash from "@/assets/icons/IconHash.svg";
---
```

### 切换至 `pnpm`

AstroPaper 已从 `npm` 切换至 `pnpm`，后者提供了更快、更高效的包管理。

### 用 Astro 的 Svg 组件替换内联 SVG

AstroPaper v5 用 Astro 实验性的 [SVG 组件](https://docs.astro.build/en/reference/experimental-flags/svg/)替换了内联 SVG。此更新减少了在 `socialIcons` 对象中预定义 SVG 代码的需求，使代码库更整洁、更易于维护。

### 分离常量与配置

项目结构已进行重组。`src/config.ts` 文件现在只包含 `SITE` 对象，该对象持有项目的主要配置。所有常量，如 `LOCALE`、`SOCIALS` 和 `SHARE_LINKS`，已被移至 `src/constants.ts` 文件。

## 其他值得注意的变更

-   博客文章目录已从 `src/content/blog/` 更新为 `src/data/blog/`。
-   集合定义文件 (`src/content/config.ts`) 现已替换为 `src/content.config.ts`。
-   多个依赖项已升级，以提升性能和安全性。
-   移除了 `IBM Plex Mono` 字体，并切换至系统默认的等宽字体。
-   “返回”按钮的逻辑已更新。现在，AstroPaper v5 不再触发浏览器的历史记录 API，而是使用浏览器会话（session）来临时存储返回的 URL。如果会话中不存在返回 URL，它将重定向到主页。
-   还有一些细微的样式和布局变更。

## 结语

AstroPaper v5 带来了许多变更，但核心体验保持不变。在保留 AstroPaper 闻名的简洁与极简设计的同时，享受一个更流畅、更高效的博客平台吧！

欢迎随时探索这些变更并分享您的想法。一如既往，感谢您的支持！

如果您喜欢这个主题，请考虑为仓库点亮一颗星 (star)。您也可以通过 GitHub Sponsors 支持我，或者如果您愿意，可以请我喝杯咖啡。当然，这些行为完全是可选的，并非强制要求。

祝您使用愉快！
