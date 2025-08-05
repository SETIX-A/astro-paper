# AstroPaper 📄

![AstroPaper](public/astropaper-og.jpg)
[![Figma](https://img.shields.io/badge/Figma-F24E1E?style=for-the-badge&logo=figma&logoColor=white)](https://www.figma.com/community/file/1356898632249991861)
![Typescript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)![GitHub](https://img.shields.io/github/license/satnaing/astro-paper?color=%232F3741&style=for-the-badge)
[![Conventional Commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-%23FE5196?logo=conventionalcommits&logoColor=white&style=for-the-badge)](https://conventionalcommits.org)
[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg?style=for-the-badge)](http://commitizen.github.io/cz-cli/)

AstroPaper 是一个极简、响应式、无障碍且SEO友好的Astro博客主题。此主题的设计与构建灵感来源于[我的个人博客](https://satnaing.dev/blog)。

阅读[这篇博客文章](https://astro-paper.pages.dev/posts/)或查看 [README 文档部分](#-文档)以获取更多信息。

## 🔥 功能特性

- [x] 类型安全的 Markdown
- [x] 极致的性能
- [x] 无障碍访问 (键盘/VoiceOver)
- [x] 响应式设计 (移动端 ~ 桌面端)
- [x] SEO 友好
- [x] 浅色 & 深色模式
- [x] 模糊搜索
- [x] 文章草稿 & 分页
- [x] 站点地图 & RSS Feed
- [x] 遵循最佳实践
- [x] 高度可定制
- [x] 为博客文章动态生成 OG 图片 [#15](https://github.com/satnaing/astro-paper/pull/15) ([相关博文](https://astro-paper.pages.dev/posts/dynamic-og-image-generation-in-astropaper-blog-posts/))

_请注意：我已在 Mac 上使用 **VoiceOver** 并在 Android 上使用 **TalkBack** 测试了 AstroPaper 的屏幕阅读器无障碍性。我无法测试市面上的所有其他屏幕阅读器。然而，AstroPaper 在无障碍性方面的增强应该也能在其他设备上良好运行。_

## ✅ Lighthouse 评分

<p align="center">
  <a href="https://pagespeed.web.dev/report?url=https%3A%2F%2Fastro-paper.pages.dev%2F&form_factor=desktop">
    <img width="710" alt="AstroPaper Lighthouse Score" src="AstroPaper-lighthouse-score.svg">
  <a>
</p>

## 🚀 项目结构

在 AstroPaper 项目内部，您会看到以下文件夹和文件：

```bash
/
├── public/
│   ├── assets/
|   ├── pagefind/ # 构建时自动生成
│   └── favicon.svg
│   └── astropaper-og.jpg
│   └── favicon.svg
│   └── toggle-theme.js
├── src/
│   ├── assets/
│   │   └── icons/
│   │   └── images/
│   ├── components/
│   ├── data/
│   │   └── blog/
│   │       └── some-blog-posts.md
│   ├── layouts/
│   └── pages/
│   └── styles/
│   └── utils/
│   └── config.ts
│   └── constants.ts
│   └── content.config.ts
└── astro.config.ts
```

Astro 会在 `src/pages/` 目录中寻找 `.astro` 或 `.md` 文件。每个页面都会根据其文件名作为一个路由暴露出来。

任何静态资源，如图片，都可以放置在 `public/` 目录中。

所有的博客文章都存储在 `src/data/blog` 目录中。

## 📖 文档

文档可以通过两种格式阅读：_markdown_ 和 _博客文章_。

-   配置 - [markdown](src/data/blog/how-to-configure-astropaper-theme.md) | [博客文章](https://astro-paper.pages.dev/posts/how-to-configure-astropaper-theme/)
-   添加文章 - [markdown](src/data/blog/adding-new-post.md) | [博客文章](https://astro-paper.pages.dev/posts/adding-new-posts-in-astropaper-theme/)
-   自定义配色方案 - [markdown](src/data/blog/customizing-astropaper-theme-color-schemes.md) | [博客文章](https://astro-paper.pages.dev/posts/customizing-astropaper-theme-color-schemes/)
-   预定义配色方案 - [markdown](src/data/blog/predefined-color-schemes.md) | [博客文章](https://astro-paper.pages.dev/posts/predefined-color-schemes/)

## 💻 技术栈

**主要框架** - [Astro](https://astro.build/)  
**类型检查** - [TypeScript](https://www.typescriptlang.org/)  
**样式** - [TailwindCSS](https://tailwindcss.com/)  
**UI/UX 设计** - [Figma 设计文件](https://www.figma.com/community/file/1356898632249991861)  
**静态搜索** - [FuseJS](https://pagefind.app/)  
**图标** - [Tablers](https://tabler-icons.io/)  
**代码格式化** - [Prettier](https://prettier.io/)  
**部署** - [Cloudflare Pages](https://pages.cloudflare.com/)  
**关于页面的插图** - [https://freesvgillustration.com](https://freesvgillustration.com/)  
**代码检查** - [ESLint](https://eslint.org)

## 👨🏻‍💻 本地运行

您可以通过在您期望的目录中运行以下命令，来在本地开始使用此项目：

```bash
# pnpm
pnpm create astro@latest --template satnaing/astro-paper

# npm
npm create astro@latest -- --template satnaing/astro-paper

# yarn
yarn create astro --template satnaing/astro-paper

# bun
bun create astro@latest -- --template satnaing/astro-paper
```

然后通过运行以下命令来启动项目：

```bash
# 如果上一步没有安装依赖，请先安装
pnpm install

# 启动项目
pnpm run dev
```

作为一种替代方法，如果您安装了 Docker，您可以使用 Docker 在本地运行此项目。操作如下：

```bash
# 构建 Docker 镜像
docker build -t astropaper .

# 运行 Docker 容器
docker run -p 4321:80 astropaper
```

## Google 网站验证 (可选)

您可以使用一个环境变量，在 AstroPaper 中轻松添加您的 [Google 网站验证 HTML 标签](https://support.google.com/webmasters/answer/9008080#meta_tag_verification&zippy=%2Chtml-tag)。此步骤是可选的。如果您不添加以下环境变量，`google-site-verification` 标签将不会出现在 HTML 的 `<head>` 部分。

```bash
# 在您的环境变量文件 (.env) 中
PUBLIC_GOOGLE_SITE_VERIFICATION=your-google-site-verification-value
```

> 关于将 AstroPaper 添加到 Google Search Console，请参阅[此讨论](https://github.com/satnaing/astro-paper/discussions/334#discussioncomment-10139247)。

## 🧞 命令

所有命令都从项目的根目录，在终端中运行：

> **_请注意!_** 对于 `Docker` 命令，我们必须在您的机器上[安装它](https://docs.docker.com/engine/install/)。

| Command | Action |
| :--- | :--- |
| `pnpm install` | 安装依赖 |
| `pnpm run dev` | 在 `localhost:4321` 启动本地开发服务器 |
| `pnpm run build` | 构建您的生产站点到 `./dist/` |
| `pnpm run preview` | 在部署前，本地预览您的构建成果 |
| `pnpm run format:check`| 使用 Prettier 检查代码格式 |
| `pnpm run format` | 使用 Prettier 格式化代码 |
| `pnpm run sync` | 为所有 Astro 模块生成 TypeScript 类型。[了解更多](https://docs.astro.build/en/reference/cli-reference/#astro-sync)。|
| `pnpm run lint` | 使用 ESLint 进行代码检查 |
| `docker compose up -d` | 在 docker 中运行 AstroPaper，您可以通过与 `dev` 命令相同的域名和端口访问。|
| `docker compose run app npm install` | 您可以在 docker 容器内运行上述任何命令。 |
| `docker build -t astropaper .` | 为 AstroPaper 构建 Docker 镜像。 |
| `docker run -p 4321:80 astropaper` | 在 Docker 中运行 AstroPaper。网站将可以通过 `http://localhost:4321` 访问。|

> **_警告!_** Windows PowerShell 用户如果想在开发过程中[运行诊断](https://docs.astro.build/en/reference/cli-reference/#astro-check) (`astro check --watch & astro dev`)，可能需要安装 [concurrently 包](https://www.npmjs.com/package/concurrently)。更多信息，请参阅[这个 issue](https://github.com/satnaing/astro-paper/issues/113)。

## ✨ 反馈 & 建议

如果您有任何建议/反馈，您可以通过[我的电子邮件](mailto:contact@satnaing.dev)与我联系。另外，如果您发现 bug 或希望请求新功能，欢迎随时提交 issue。

## 📜 许可证

根据 MIT 许可证授权，版权所有 © 2025

---

由 [Sat Naing](https://satnaing.dev) 👨🏻‍💻 和 [贡献者们](https://github.com/satnaing/astro-paper/graphs/contributors) 🤍 制作。
