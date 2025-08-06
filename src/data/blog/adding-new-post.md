---
author: Sat Naing
pubDatetime: 2022-09-23T15:22:00Z
modDatetime: 2025-08-04T16:52:45.934Z
title: 在 AstroPaper 主题中添加新文章
slug: adding-new-posts-in-astropaper-theme
featured: true
draft: false
tags:
  - docs
description:
  Some rules & recommendations for creating or adding new posts using AstroPaper
  theme.
---

这里有一些关于在 AstroPaper 博客主题中创建新帖子的规则/建议、技巧和窍门。

<figure>
  <img
    src="https://images.pexels.com/photos/159618/still-life-school-retro-ink-159618.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1"
    alt="Free Classic wooden desk with writing materials, vintage clock, and a leather bag. Stock Photo"
  />
    <figcaption class="text-center">
    Photo by <a href="https://www.pexels.com/photo/brown-wooden-desk-159618/">Pixabay</a>
  </figcaption>
</figure>

## Table of contents

## 创建博客文章

要撰写一篇新的博客文章，请在 `src/data/blog/` 目录下创建一个 Markdown 文件。

> 在 AstroPaper v5.1.0 版本之前，所有的博客文章都必须存放在 `src/data/blog/` 根目录下，这意味着您无法将它们组织到子目录中。

从 AstroPaper v5.1.0 版本开始，您现在可以将博客文章整理到不同的子目录中，从而让您的内容管理起来更加便捷。

例如，如果您想将一些文章按年份 `2025` 分组，您可以将它们放置在 `src/data/blog/2025/` 目录下。这也会影响文章的URL，因此 `src/data/blog/2025/example-post.md` 这篇文章的访问链接将是 `/posts/2025/example-post`。

如果您不希望子目录影响文章的URL，只需在文件夹名称前加上下划线 `_` 即可。

```bash
# 示例：博客文章结构与对应的URL
src/data/blog/very-first-post.md          -> mysite.com/posts/very-first-post
src/data/blog/2025/example-post.md        -> mysite.com/posts/2025/example-post
src/data/blog/_2026/another-post.md       -> mysite.com/posts/another-post
src/data/blog/docs/_legacy/how-to.md      -> mysite.com/posts/docs/how-to
src/data/blog/Example Dir/Dummy Post.md   -> mysite.com/posts/example-dir/dummy-post
```

> 💡 **提示**：您也可以在 frontmatter 中覆盖文章的 `slug`。更多详情请参见下一节。

如果在构建输出中没有出现子目录的URL，请删除 `node_modules` 文件夹，重新安装依赖包，然后再次进行构建。

## Frontmatter

Frontmatter 是存储博客文章重要信息的关键区域。它位于文章顶部，并以 YAML 格式编写。您可以阅读 [Astro 官方文档](https://docs.astro.build/en/guides/markdown-content/)了解更多关于 frontmatter 的用法。

以下是每篇文章可用的 frontmatter 属性列表。

| 属性 (Property)    | 描述 (Description)                                                                                                                    | 备注 (Remark)                                  |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| **_title_**        | 文章的标题 (h1)。                                                                                                                     | 必需<sup>\*</sup>                              |
| **_description_**  | 文章的描述。用于文章摘要和页面的元描述（meta description）。                                                                          | 必需<sup>\*</sup>                              |
| **_pubDatetime_**  | 文章的发布日期和时间，采用 ISO 8601 格式。                                                                                            | 必需<sup>\*</sup>                              |
| **_modDatetime_**  | 文章的修改日期和时间，采用 ISO 8601 格式 (仅在文章被修改时添加此属性)。                                                               | 可选                                           |
| **_author_**       | 文章的作者。                                                                                                                          | 默认值：`SITE.author`                          |
| **_slug_**         | 文章的 slug (URL片段)。此字段为可选。                                                                                                 | 默认值：根据文件名自动生成                     |
| **_featured_**     | 是否在首页的“精选文章”区域显示此文章。                                                                                                | 默认值：`false`                                |
| **_draft_**        | 将此文章标记为“未发布”状态。                                                                                                          | 默认值：`false`                                |
| **_tags_**         | 与此文章相关的关键词。以 YAML 数组格式编写。                                                                                          | 默认值：`others`                               |
| **_ogImage_**      | 文章的 OG 图片。用于社交媒体分享和SEO。可以是远程URL，也可以是相对于当前文件夹的图片路径。                                              | 默认值：`SITE.ogImage` 或自动生成的 OG 图片      |
| **_canonicalURL_** | 规范链接 (Canonical URL)，用于指明文章的首选地址，以防文章已在别处发布。                                                              | 默认值：`Astro.site` + `Astro.url.pathname`    |
| **_hideEditPost_** | 在文章标题下方隐藏“编辑文章”按钮。此设置仅对当前文章生效。                                                                          | 默认值：`false`                                |
| **_timezone_**     | 为当前文章指定一个 IANA 格式的时区。这将覆盖 `SITE.timezone` 的全局配置。                                                             | 默认值：`SITE.timezone`                        |

> **提示**！您可以在浏览器的控制台中运行 `new Date().toISOString()` 来获取 ISO 8601 格式的日期时间。请注意，使用时需要移除双引号。

在 frontmatter 中，只有 `title`、`description` 和 `pubDatetime` 这三个字段是必须填写的。

标题和描述（摘要）对于搜索引擎优化（SEO）至关重要，因此 AstroPaper 主题鼓励您在博客文章中包含这些信息。

`slug` 是 URL 的唯一标识符，因此每篇文章的 `slug` 都必须是唯一的。其中的空格应使用 `-` 或 `_` 分隔，但推荐使用 `-`。Slug 会根据文章的文件名自动生成，但您也可以在 frontmatter 中明确定义 `slug` 来覆盖默认值。

例如，如果文章的文件名是 `adding-new-post.md`，而您没有在 frontmatter 中指定 `slug`，Astro 将根据文件名自动创建 slug，其值为 `adding-new-post`。但若您在 frontmatter 中指定了 `slug`，则会使用您指定的值。您可以阅读 [Astro 官方文档](https://docs.astro.build/en/guides/content-collections/#defining-custom-slugs) 了解更多细节。

如果您在文章中省略了 `tags` 字段（即没有指定任何标签），文章将被自动打上 `others` 这个默认标签。您可以在 `content.config.ts` 文件中修改这个默认值。

```ts file="src/content.config.ts"
export const blogSchema = z.object({
  // ...
  draft: z.boolean().optional(),
  // [!code highlight:1]
  tags: z.array(z.string()).default(["others"]), // 将 "others" 替换为您想要的任何默认值
  // ...
});
```

### Frontmatter 示例

这是一篇示例文章的 frontmatter。

```yaml file="src/data/blog/sample-post.md"
---
title: The title of the post
author: your name
pubDatetime: 2022-09-21T05:17:19Z
slug: the-title-of-the-post
featured: true
draft: false
tags:
  - some
  - example
  - tags
ogImage: ../../assets/images/example.png # src/assets/images/example.png
# ogImage: "https://example.org/remote-image.png" # 远程 URL
description: This is the example description of the example post.
canonicalURL: https://example.org/my-article-was-already-posted-here
---
```

## 添加文章目录

默认情况下，文章不包含目录（Table of Contents）。若要启用目录，您需要通过一种特定的方式来声明它。

在您希望显示目录的位置，用 h2 格式（即 `##`）写下 `Table of contents`。

例如，如果您希望将目录放置在引言段落的下方（就像我通常做的那样），您可以这样做：

<!-- prettier-ignore-start -->
```md
---
# 此处是 frontmatter
---

这里是一些关于在 AstroPaper 博客主题中创建新文章的建议和技巧。

<!-- [!code ++] -->
## Table of contents

<!-- 文章的其余部分 -->```
<!-- prettier-ignore-end -->

## 关于文章标题

关于标题，有一点需要注意。AstroPaper 主题将 frontmatter 中的 `title` 字段用作文章的主标题（即 `<h1>`）。因此，文章正文中的其他标题应从 h2 到 h6 级别开始使用。

这条规则并非强制，但为了更好的视觉效果、无障碍访问（Accessibility）和 SEO，我们强烈建议您遵守。

## 语法高亮

AstroPaper 使用 [Shiki](https://shiki.style/) 作为默认的语法高亮工具。从 AstroPaper v5.4 开始，我们引入了 [@shikijs/transformers](https://shiki.style/packages/transformers) 来增强代码块的展示效果。如果您不想使用它，可以通过以下命令移除：

```bash
pnpm remove @shikijs/transformers
```

```js file="astro.config.ts"
// ...
// [!code --:5]
import {
  transformerNotationDiff,
  transformerNotationHighlight,
  transformerNotationWordHighlight,
} from "@shikijs/transformers";

export default defineConfig({
  // ...
  markdown: {
    remarkPlugins: [remarkToc, [remarkCollapse, { test: "Table of contents" }]],
    shikiConfig: {
      // 更多主题请访问 https://shiki.style/themes
      themes: { light: "min-light", dark: "night-owl" },
      defaultColor: false,
      wrap: false,
      transformers: [
        transformerFileName(),
      // [!code --:3]
        transformerNotationHighlight(),
        transformerNotationWordHighlight(),
        transformerNotationDiff({ matchAlgorithm: "v3" }),
      ],
    },
  },
  // ...
}```

## 存储文章图片

以下是在 Markdown 文件中存储和展示图片的两种方法。

> **请注意！** 如果您需要在 Markdown 中对优化后的图片应用样式，您应该[使用 MDX](https://docs.astro.build/en/guides/images/#images-in-mdx-files)。

### 方案一：存放于 `src/assets/` 目录（推荐）

您可以将图片存放在 `src/assets/` 目录中。这些图片将通过 Astro 的 [图像服务API](https://docs.astro.build/en/reference/image-service-reference/) 被自动优化。

您可以使用相对路径或别名路径 (`@/assets/`) 来引用这些图片。

例如：假设您想显示 `example.jpg` 这张图片，它的路径是 `/src/assets/images/example.jpg`。

```md
![图片描述](@/assets/images/example.jpg)

<!-- 或者 -->

![图片描述](../../assets/images/example.jpg)

<!-- 使用 img 标签或 Image 组件将无法工作 ❌ -->
<img src="@/assets/images/example.jpg" alt="图片描述">
<!-- ^^ 这是错误的做法 -->
```

> 技术上讲，您可以将图片存储在 `src` 下的任何目录中。这里推荐使用 `src/assets` 只是一个建议。

### 方案二：存放于 `public` 目录

您也可以将图片存放在 `public` 目录中。请记住，存放在 `public` 目录中的图片不会被 Astro 处理，这意味着它们不会被优化，您需要自己负责图片的优化工作。

引用这些图片时，您应该使用绝对路径；并且可以通过 [Markdown 的图片语法](https://www.markdownguide.org/basic-syntax/#images-1)或 [HTML 的 `<img>` 标签](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img)来显示。

例如：假设 `example.jpg` 位于 `/public/assets/images/example.jpg`。

```md
![图片描述](/assets/images/example.jpg)

<!-- 或者 -->

<img src="/assets/images/example.jpg" alt="图片描述">
```

## 额外技巧

### 图片压缩

当您在文章中插入图片时（特别是存放在 `public` 目录下的图片），我们推荐您先对图片进行压缩。这将有助于提升网站的整体性能。

我推荐的图片压缩网站：

- [TinyPng](https://tinypng.com/)
- [TinyJPG](https://tinyjpg.com/)

### OG 图片

如果一篇文章没有在 frontmatter 中指定 OG 图片，系统将会使用默认的 OG 图片。虽然不是必需的，但我们建议为每篇文章指定与其内容相关的 OG 图片。OG 图片的推荐尺寸为 **_1200 X 640_** 像素。

> 从 AstroPaper v1.4.0 版本开始，如果未指定 OG 图片，系统将自动为其生成。详情请查看[这篇公告](https://astro-paper.pages.dev/posts/dynamic-og-image-generation-in-astropaper-blog-posts/)。
