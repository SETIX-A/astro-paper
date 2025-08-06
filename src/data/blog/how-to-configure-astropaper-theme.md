---
author: SETIX
pubDatetime: 2022-09-23T04:58:53Z
modDatetime: 2025-08-04T03:15:57.792Z
title: 如何配置 AstroPaper 主题
slug: how-to-configure-astropaper-theme
featured: true
draft: false
tags:
  - configuration
  - docs
description: 如何将 AstroPaper 主题完全打造成您的专属风格。
---

AstroPaper 是一个高度可定制的 Astro 博客主题。使用 AstroPaper，您可以根据个人品味自定义一切。本文将讲解如何通过配置文件轻松地进行一些自定义设置。

## Table of contents

好的，没问题！为您提供专业的翻译服务并保持原有排版是我的荣幸。

以下是为您精心翻译并排版好的内容：

---

## 配置 SITE

重要的配置项位于 `src/config.ts` 文件中。在该文件中，您会看到一个 `SITE` 对象，您可以在此指定网站的主要配置。

在开发环境中，`SITE.website` 的值可以留空。但在生产环境中，您应该在 `SITE.website` 选项中指定您部署好的网站 URL，因为这个 URL 将被用于生成规范链接（canonical URL）、社交媒体卡片链接等，这些对于 SEO 至关重要。

```js file=src/config.ts
export const SITE = {
  website: "https://astro-paper.pages.dev/", // 将此替换为您部署的域名
  author: "Sat Naing",
  profile: "https://satnaing.dev/",
  desc: "一个极简、响应式且对 SEO 友好的 Astro 博客主题。",
  title: "AstroPaper",
  ogImage: "astropaper-og.jpg",
  lightAndDarkMode: true,
  postPerIndex: 4,
  postPerPage: 4,
  scheduledPostMargin: 15 * 60 * 1000, // 15 分钟
  showArchives: true,
  showBackButton: true, // 在文章详情页显示返回按钮
  editPost: {
    enabled: true,
    text: "建议更改",
    url: "https://github.com/satnaing/astro-paper/edit/main/",
  },
  dynamicOgImage: true, // 启用自动动态生成 OG 图片
  dir: "ltr", // "rtl" | "auto"
  lang: "en", // html 语言代码。留空则默认为 "en"
  timezone: "Asia/Bangkok", // 默认全局时区 (IANA 格式) https://en.wikipedia.org/wiki/List_of_tz_database_time_zones
} as const;
```

以下是 SITE 的配置选项说明：

| 选项                  | 描述                                                                                                                                                                                                                                                                      |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `website`             | 您部署的网站 URL                                                                                                                                                                                                                                                          |
| `author`              | 您的姓名                                                                                                                                                                                                                                                                  |
| `profile`             | 您的个人/作品集网站 URL，用于更好的 SEO。如果您没有，请设置为 `null` 或空字符串 `""`。                                                                                                                                                                                      |
| `desc`                | 您的网站描述。对 SEO 和社交媒体分享很有用。                                                                                                                                                                                                                               |
| `title`               | 您的网站名称                                                                                                                                                                                                                                                              |
| `ogImage`             | 网站的默认 OG 图片。对社交媒体分享很有用。OG 图片可以是一个外部图片 URL，也可以是放在 `/public` 目录下的图片。                                                                                                                                                           |
| `lightAndDarkMode`    | 启用或禁用网站的“浅色 & 深色模式”。如果禁用，将使用主配色方案。此选项默认启用。                                                                                                                                                                                        |
| `postPerIndex`        | 显示在主页“近期文章”板块下的文章数量。                                                                                                                                                                                                                                    |
| `postPerPage`         | 您可以指定每个文章分页将显示多少篇文章。（例如：如果您将 `SITE.postPerPage` 设为 3，每个分页将只显示 3 篇文章）                                                                                                                                                         |
| `scheduledPostMargin` | 在生产环境中，发布时间（`pubDatetime`）在未来的文章将不会显示。但是，如果一篇文章的发布时间在未来 15 分钟之内，它将会被显示。如果您不喜欢默认的 15 分钟缓冲时间，可以设置 `scheduledPostMargin`。                                                                            |
| `showArchives`        | 决定是否在网站上显示“归档”菜单（位于“关于”和“搜索”菜单之间）及其对应的页面。此选项默认设置为 `true`。                                                                                                                                                                 |
| `showBackButton`      | 决定是否在每篇博客文章中显示“返回”按钮。                                                                                                                                                                                                                                  |
| `editPost`            | 此选项允许用户通过在博客文章标题下方提供一个编辑链接来建议对文章进行修改。通过将 `SITE.editPost.enabled` 设置为 `false` 可以禁用此功能。                                                                                                                                   |
| `dynamicOgImage`      | 此选项控制是否在博客文章的 frontmatter 中未指定 `ogImage` 时，[动态生成 OG 图片](https://astro-paper.pages.dev/posts/dynamic-og-image-generation-in-astropaper-blog-posts/)。如果您的博客文章很多，您可能想要禁用此功能。更多细节请参阅[权衡利弊](https://astro-paper.pages.dev/posts/dynamic-og-image-generation-in-astropaper-blog-posts/#trade-off)。 |
| `dir`                 | 指定整个博客的文本方向。用作 `<html dir="ltr">` 中的 [HTML dir 属性](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/dir)。支持的值：`ltr` \| `rtl` \| `auto`。                                                                                |
| `lang`                | 用作 `<html lang"en">` 中的 HTML ISO 语言代码。默认为 `en`。                                                                                                                                                                                                             |
| `timezone`            | 此选项允许您使用 [IANA 格式](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)指定您的时区。设置此项可确保您本地主机和部署站点之间的时间戳一致，消除时间差异。                                                                                              |

## 更新布局宽度

整个博客默认的 `max-width`（最大宽度）是 `768px` (`max-w-3xl`)。如果您想更改它，可以很轻松地在 `global.css` 文件中更新 `max-w-app` 这个功能类。例如：

```css file=src/styles/global.css
@utility max-w-app {
  /* [!code --:1] */
  @apply max-w-3xl;
  /* [!code ++:1] */
  @apply max-w-4xl xl:max-w-5xl;
}
```

您可以在 [Tailwind CSS 文档](https://tailwindcss.com/docs/max-width)中探索更多 `max-width` 的值。

## 配置 Logo 或标题

在 AstroPaper v5 之前，您可以在 `src/config.ts` 文件中的 `LOGO_IMAGE` 对象里更新您的网站名称/logo。然而，在 AstroPaper v5 中，为了更好地利用 Astro 内置的 SVG 和 Image 组件，这个选项已被移除。

![一个指向网站 logo 的箭头](https://res.cloudinary.com/noezectz/v1663911318/astro-paper/AstroPaper-logo-config_goff5l.png)

您有 3 种选择：

### 选项一：使用 SITE 的标题文本

这是最简单的选项。您只需要更新 `src/config.ts` 文件中的 `SITE.title` 即可。

### 选项二：使用 Astro 的 SVG 组件

如果您想使用 SVG 格式的 logo，您可能会选择这个方案。

-   首先，在 `src/assets` 目录下添加一个 SVG 文件。（例如：`src/assets/dummy-logo.svg`）
-   然后，在 `Header.astro` 文件中导入该 SVG。
    ```astro file=src/components/Header.astro
    ---
    // ...
    import DummyLogo from "@/assets/dummy-logo.svg";
    ---
    ```
-   最后，用导入的 logo 替换掉 `{SITE.title}`。
    ```html
    <a
      href="/"
      class="absolute py-1 text-left text-2xl leading-7 font-semibold whitespace-nowrap sm:static"
    >
      <DummyLogo class="scale-75 dark:invert" />
      <!-- {SITE.title} -->
    </a>
    ```

这个方法最大的好处是您可以根据需要自定义 SVG 的样式。在上面的例子中，您可以看到 SVG logo 的颜色是如何在深色模式下被反转的。

### 选项三：使用 Astro 的 Image 组件

如果您的 logo 是图片格式而非 SVG，您可以使用 Astro 的 Image 组件。

-   将您的 logo 添加到 `src/assets` 目录下。（例如：`src/assets/dummy-logo.png`）
-   在 `Header.astro` 中导入 `Image` 组件和您的 logo。
    ```astro file=src/components/Header.astro
    ---
    // ...
    import { Image } from "astro:assets";
    import dummyLogo from "@/assets/dummy-logo.png";
    ---
    ```
-   然后，用导入的 logo 替换掉 `{SITE.title}`。
    ```html
    <a
      href="/"
      class="absolute py-1 text-left text-2xl leading-7 font-semibold whitespace-nowrap sm:static"
    >
      <Image src={dummyLogo} alt="Dummy Blog" class="dark:invert" />
      <!-- {SITE.title} -->
    </a>
    ```

通过这种方法，您依然可以使用 CSS 类来调整图片的外观。然而，这可能不总能满足您的需求。如果您需要根据浅色或深色模式显示不同的 logo 图片，请参考 `Header.astro` 组件中处理浅色/深色模式图标的方式。

## 配置社交链接

![一个指向社交链接图标的箭头](https://github.com/user-attachments/assets/8b895400-d088-442f-881b-02d2443e00cf)

您可以在 `constants.ts` 文件中的 `SOCIALS` 对象里配置社交链接。

```ts file=src/constants.ts
export const SOCIALS = [
  {
    name: "GitHub",
    href: "https://github.com/satnaing/astro-paper",
    linkTitle: ` ${SITE.title} 在 GitHub`,
    icon: IconGitHub,
  },
  {
    name: "X",
    href: "https://x.com/username",
    linkTitle: `${SITE.title} 在 X`,
    icon: IconBrandX,
  },
  {
    name: "LinkedIn",
    href: "https://www.linkedin.com/in/username/",
    linkTitle: `${SITE.title} 在 LinkedIn`,
    icon: IconLinkedin,
  },
  {
    name: "Mail",
    href: "mailto:yourmail@gmail.com",
    linkTitle: `向 ${SITE.title} 发送邮件`,
    icon: IconMail,
  },
] as const;
```

## 配置分享链接

您可以在 `src/constants.ts` 文件中的 `SHARE_LINKS` 对象里配置分享链接。

![一个指向分享链接图标的箭头](https://github.com/user-attachments/assets/4f930b68-b625-45df-8c41-e076dd2b838e)

## 结论

以上是关于如何自定义此主题的简要说明。如果您懂一些编程，您可以进行更多的自定义。关于自定义样式，请阅读[这篇文章](https://astro-paper.pages.dev/posts/customizing-astropaper-theme-color-schemes/)。感谢您的阅读。✌🏻
