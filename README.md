# wengxiaozhou42 的个人博客

线上地址：<https://wengxiaozhou42-eng.github.io/>

用 [nice-template](https://github.com/yejianqin61-cell/nice-template) 搭的 Jekyll 静态博客，发布在 GitHub Pages 上。界面是液态玻璃（Liquid Glass / glassmorphism）风格：半透明磨砂面板、胶囊导航、彩色光斑背景，全部用纯 CSS 实现。没有 Node.js、npm、React、Vue，也没有外部 CDN 和构建工具；HTML/CSS/Markdown 之外什么都不需要。

## 写一篇新文章

在 `_posts/` 新建 `YYYY-MM-DD-title.md`，开头保留 Front Matter：

```yaml
---
layout: post
title: 文章标题
date: 2026-10-24
excerpt: 一句话摘要
tags:
  - 标签
---

正文用 Markdown 写：标题、段落、列表、表格、链接、代码块都可以。
```

文件名里的日期决定排序，`title`（文件名去掉日期和扩展名）决定网址：`/posts/<title>/`。注意 `date` 不要写成未来日期，Jekyll 默认不发布未来文章。

## 文件说明

| 文件 | 作用 |
| --- | --- |
| `_config.yml` | 站点标题、描述、语言、时区、permalink |
| `index.html` | 首页：自我介绍、文章列表、项目卡片 |
| `about.md` | 关于页 |
| `_posts/*.md` | 文章 |
| `_layouts/default.html` | 公共布局：导航、页头、页脚 |
| `_layouts/post.html` | 文章页布局 |
| `assets/style.css` | 配色（顶部 CSS 变量）和排版 |
| `.github/workflows/pages.yml` | GitHub Actions：构建并部署到 Pages |

## 改配色（液态玻璃）

`assets/style.css` 顶部是一组 CSS 变量，改这里就能换整站风格，不用动其他样式：

```css
:root {
  --ink: #0e1a33;          /* 正文颜色 */
  --muted: #46557a;        /* 次要文字 */
  --accent: #6d4df6;       /* 主色（紫） */
  --accent-2: #00a6c0;     /* 辅助色（青） */
  --accent-3: #e35d9b;     /* 点缀色（粉） */
  --accent-ink: #4a34c9;   /* 链接和强调文字 */
  --glass: rgba(255,255,255,.42);        /* 玻璃底色 */
  --glass-strong: rgba(255,255,255,.64); /* 导航等更实的玻璃 */
  --glass-line: rgba(255,255,255,.75);   /* 玻璃高光边 */
}
```

彩色光斑背景在 `body` 的 `background-image` 里，磨砂效果来自各面板的 `backdrop-filter`。改完用浏览器打开即可预览，不需要安装任何依赖。

## 发布

1. `git status` 和 `git diff` 检查改动
2. `git add -A`
3. `git commit -m "写清楚这次改了什么"`
4. `git push`
5. 推送后 GitHub Actions 自动构建，打开 <https://wengxiaozhou42-eng.github.io/> 确认

本地不需要安装 Ruby 或 Jekyll，页面由 Action 生成。第一次使用时，仓库的 Settings → Pages → Source 要设为 **GitHub Actions**（已配置）。

## 仓库结构

```text
├── _config.yml
├── index.html
├── about.md
├── _posts/
├── _layouts/
├── assets/style.css
└── .github/workflows/pages.yml
```
