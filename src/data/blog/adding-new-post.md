---
author: Sat Naing
pubDatetime: 2022-09-23T15:22:00Z
modDatetime: 2025-06-13T16:52:45.934Z
title: 在 AstroPaper 主题中添加新文章
slug: adding-new-posts-in-astropaper-theme
featured: true
draft: false
tags:
  - docs
description:
  关于使用 AstroPaper 主题创建或添加新文章的一些规则和建议。
---

以下是关于使用 AstroPaper 博客主题创建新文章的一些规则/建议、提示和技巧。

<figure>
  <img
    src="https://images.pexels.com/photos/159618/still-life-school-retro-ink-159618.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1"
    alt="一张免费的经典木质书桌图片，上面有书写材料、复古时钟和一个皮包。图库照片"
  />
    <figcaption class="text-center">
    照片由 <a href="https://www.pexels.com/photo/brown-wooden-desk-159618/">Pixabay</a> 提供
  </figcaption>
</figure>

## 目录

## 创建一篇博客文章

要撰写一篇新的博客文章，请在 `src/data/blog/` 目录下创建一个 Markdown 文件。

> 在 AstroPaper v5.1.0 之前，所有的博客文章都必须放在 `src/data/blog/` 目录下，这意味着您无法将它们组织到子目录中。

从 AstroPaper v5.1.0 开始，您现在可以将博客文章组织到子目录中，从而更轻松地管理您的内容。

例如，如果您想将文章分组到 `2025` 目录下，您可以将它们放置在 `src/data/blog/2025/`。这也会影响文章的 URL，因此 `src/data/blog/2025/example-post.md` 的访问地址将是 `/posts/2025/example-post`。

如果您不希望子目录影响文章的 URL，只需在文件夹名称前加上下划线 `_`。

```bash
# 示例：博客文章结构及其 URL
src/data/blog/very-first-post.md          -> mysite.com/posts/very-first-post
src/data/blog/2025/example-post.md        -> mysite.com/posts/2025/example-post
src/data/blog/_2026/another-post.md       -> mysite.com/posts/another-post
src/data/blog/docs/_legacy/how-to.md      -> mysite.com/posts/docs/how-to
src/data/blog/Example Dir/Dummy Post.md   -> mysite.com/posts/example-dir/dummy-post
```

> 💡 提示：您也可以在 frontmatter 中覆盖博客文章的 slug。更多详情请参见下一节。

如果子目录的 URL 没有出现在构建输出中，请删除 `node_modules`，重新安装依赖包，然后重新构建。

## Frontmatter

Frontmatter 是存储博客文章（article）一些重要信息的主要位置。Frontmatter 位于文章的顶部，以 YAML 格式编写。在 [Astro 文档](https://docs.astro.build/en/guides/markdown-content/)中阅读更多关于 frontmatter 及其用法的信息。

以下是每篇文章的 frontmatter 属性列表。

| 属性               | 描述                                                                                                                                  | 备注                                           |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| **_title_**        | 文章的标题。(h1)                                                                                                                      | 必需<sup>\*</sup>                              |
| **_description_**  | 文章的描述。用于文章摘要和网站的文章描述。                                                                                            | 必需<sup>\*</sup>                              |
| **_pubDatetime_**  | 文章的发布日期时间，采用 ISO 8601 格式。                                                                                              | 必需<sup>\*</sup>                              |
| **_modDatetime_**  | 文章的修改日期时间，采用 ISO 8601 格式。(仅当博客文章被修改时才添加此属性)                                                              | 可选                                           |
| **_author_**       | 文章的作者。                                                                                                                          | 默认 = SITE.author                             |
| **_slug_**         | 文章的 slug (URL片段)。此字段为可选。                                                                                                 | 默认 = 根据文件名生成的 slug                   |
| **_featured_**     | 是否在主页的精选部分显示此文章。                                                                                                      | 默认 = false                                   |
| **_draft_**        | 将此文章标记为‘未发布’。                                                                                                              | 默认 = false                                   |
| **_tags_**         | 与此文章相关的关键词。以数组 YAML 格式编写。                                                                                          | 默认 = others                                  |
| **_ogImage_**      | 文章的 OG 图片。对社交媒体分享和 SEO 有用。这可以是一个远程 URL 或相对于当前文件夹的图片路径。                                        | 默认 = `SITE.ogImage` 或自动生成的 OG 图片     |
| **_canonicalURL_** | 规范 URL (绝对路径)，用于文章已存在于其他来源的情况。                                                                                  | 默认 = `Astro.site` + `Astro.url.pathname`     |
| **_hideEditPost_** | 在博客标题下隐藏“编辑文章”按钮。此设置仅对当前博客文章生效。                                                                          | 默认 = false                                   |
| **_timezone_**     | 为当前博客文章指定一个 IANA 格式的时区。这将覆盖当前文章的 `SITE.timezone` 配置。                                                      | 默认 = `SITE.timezone`                         |

> 提示！您可以在浏览器控制台中运行 `new Date().toISOString()` 来获取 ISO 8601 格式的日期时间。不过请确保移除引号。

在 frontmatter 中，只有 `title`、`description` 和 `pubDatetime` 字段是必须指定的。

标题和描述（摘要）对于搜索引擎优化（SEO）非常重要，因此 AstroPaper 鼓励在博客文章中包含这些内容。

`slug` 是 URL 的唯一标识符。因此，`slug` 必须是唯一的，且与其他文章不同。`slug` 中的空格应使用 `-` 或 `_` 分隔，但推荐使用 `-`。Slug 是根据博客文章的文件名自动生成的。但是，您可以在博客文章的 frontmatter 中自定义 `slug`。

例如，如果博客文件名为 `adding-new-post.md`，并且您没有在 frontmatter 中指定 slug，Astro 将使用文件名自动为该文章创建一个 slug。因此，slug 将是 `adding-new-post`。但如果您在 frontmatter 中指定了 `slug`，这将覆盖默认的 slug。您可以在 [Astro 文档](https://docs.astro.build/en/guides/content-collections/#defining-custom-slugs)中了解更多相关信息。

如果您在某篇博客文章中省略了 `tags`（换句话说，没有指定任何标签），那么默认的 `others` 标签将被用作该文章的标签。您可以在 `content.config.ts` 文件中设置默认标签。

```ts file="src/content.config.ts"
export const blogSchema = z.object({
  // ...
  draft: z.boolean().optional(),
  // [!code highlight:1]
  tags: z.array(z.string()).default(["others"]), // 将 "others" 替换为您想要的任何值
  // ...
});
```

### Frontmatter 示例

以下是一篇文章的 frontmatter 示例。

```yaml file="src/data/blog/sample-post.md"
---
title: 文章的标题
author: 你的名字
pubDatetime: 2022-09-21T05:17:19Z
slug: the-title-of-the-post
featured: true
draft: false
tags:
  - 一些
  - 示例
  - 标签
ogImage: ../../assets/images/example.png # src/assets/images/example.png
# ogImage: "https://example.org/remote-image.png" # 远程 URL
description: 这是示例文章的示例描述。
canonicalURL: https://example.org/my-article-was-already-posted-here
---
```

## 添加目录

默认情况下，一篇文章（article）不包含任何目录（toc）。要包含目录，您必须以一种特定的方式来指定它。

以 h2 格式（在 markdown 中是 `##`）编写 `Table of contents`，并将其放置在您希望它在文章中出现的位置。

例如，如果您想将目录放置在引言段落的正下方（就像我通常做的那样），您可以按以下方式操作。

<!-- prettier-ignore-start -->
```md
---
# frontmatter
---

这里是关于使用 AstroPaper 博客主题创建新文章的一些建议、提示和技巧。

<!-- [!code ++] -->
## Table of contents

<!-- 文章的其余部分 -->
```
<!-- prettier-ignore-end -->

## 标题

关于标题，有一点需要注意。AstroPaper 的博客文章使用 frontmatter 中的 title 作为文章的主标题。因此，文章中其余的标题应该使用 h2 ~ h6。

这条规则不是强制性的，但为了视觉效果、无障碍性和 SEO 目的，强烈推荐遵守。

## 语法高亮

AstroPaper 使用 [Shiki](https://shiki.style/) 作为默认的语法高亮工具。从 AstroPaper v5.4 开始，使用 [@shikijs/transformers](https://shiki.style/packages/transformers) 来增强代码块的显示效果。如果您不想使用它，可以像这样简单地移除它：

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
      // 更多主题，请访问 https://shiki.style/themes
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
}
```

## 为博客内容存储图片

这里有两种在 Markdown 文件中存储和显示图片的方法。

> 注意！如果需要在 markdown 中为优化后的图片设置样式，您应该[使用 MDX](https://docs.astro.build/en/guides/images/#images-in-mdx-files)。

### 在 `src/assets/` 目录中 (推荐)

您可以将图片存储在 `src/assets/` 目录中。这些图片将通过 [Image Service API](https://docs.astro.build/en/reference/image-service-reference/) 由 Astro 自动优化。

您可以使用相对路径或别名路径 (`@/assets/`) 来引用这些图片。

示例：假设您想显示 `example.jpg`，其路径为 `/src/assets/images/example.jpg`。

```md
![一些描述](@/assets/images/example.jpg)

<!-- 或者 -->

![一些描述](../../assets/images/example.jpg)

<!-- 使用 img 标签或 Image 组件将不起作用 ❌ -->
<img src="@/assets/images/example.jpg" alt="一些描述">
<!-- ^^ 这是错误的 -->
```

> 从技术上讲，您可以将图片存储在 `src` 下的任何目录中。在这里，`src/assets` 只是一个建议。

### 在 `public` 目录中

您可以将图片存储在 `public` 目录中。请记住，存储在 `public` 目录中的图片不会被 Astro 处理，这意味着它们不会被优化，您需要自己处理图片优化。

对于这些图片，您应该使用绝对路径；并且这些图片可以使用 [Markdown 标注](https://www.markdownguide.org/basic-syntax/#images-1) 或 [HTML img 标签](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img)来显示。

示例：假设 `example.jpg`位于 `/public/assets/images/example.jpg`。

```md
![一些描述](/assets/images/example.jpg)

<!-- 或者 -->

<img src="/assets/images/example.jpg" alt="一些描述">
```

## 额外加分项

### 图片压缩

当您在博客文章中放置图片时（特别是对于 `public` 目录下的图片），建议对图片进行压缩。这将影响网站的整体性能。

我推荐的图片压缩网站：

- [TinyPng](https://tinypng.com/)
- [TinyJPG](https://tinyjpg.com/)

### OG 图片

如果一篇文章没有指定 OG 图片，将会使用默认的 OG 图片。虽然不是必需的，但建议在 frontmatter 中指定与文章内容相关的 OG 图片。OG 图片的推荐尺寸是 **_1200 X 640_** 像素。

> 从 AstroPaper v1.4.0 开始，如果未指定 OG 图片，将会自动生成。请查看[相关公告](https://astro-paper.pages.dev/posts/dynamic-og-image-generation-in-astropaper-blog-posts/)。
