---
layout: post
title: 用 GitHub Pages 搭起这个博客
date: 2026-10-09
excerpt: 从模板仓库到能访问的网址，整个过程只有 Markdown、Jekyll 和 GitHub Actions。
tags:
  - 建站
  - GitHub Pages
---

这个博客没有服务器，也没有数据库。它由三个很朴素的部分组成：

```text
Markdown 文章  →  Jekyll（在 GitHub Actions 上运行）  →  HTML 页面  →  GitHub Pages 网址
```

## 用到的模板

起点是 [nice-template](https://github.com/yejianqin61-cell/nice-template)：一个 Markdown + Jekyll 的个人博客模板，本身不依赖 Node.js、npm 或任何前端框架。

我没有把模板重写一遍，只改了自己的信息：

| 文件 | 作用 |
| --- | --- |
| `_config.yml` | 站点标题、描述、语言和时区 |
| `index.html` | 首页：自我介绍、文章列表、项目卡片 |
| `about.md` | 关于页 |
| `_posts/*.md` | 每一篇文章，文件名是 `YYYY-MM-DD-标题.md` |
| `_layouts/*.html` | 公共布局：导航、页头、页脚和文章页 |
| `assets/style.css` | 配色和排版，颜色都写在顶部的 CSS 变量里 |

文章写到 `_posts` 文件夹里，首页会自动按时间列出最近的几篇。

## 发布流程

仓库里已经带了一个 GitHub Actions workflow：`.github/workflows/pages.yml`。它的工作很直接：

1. 检出代码
2. 用 Jekyll 编译 Markdown
3. 把生成的 `_site` 目录上传成 Pages 产物
4. 部署到 GitHub Pages

```yaml
- name: Build with Jekyll
  uses: actions/jekyll-build-pages@v1
  with:
    source: ./
    destination: ./_site
```

因此我本地不需要装 Ruby 或 Jekyll：编译发生在 GitHub 的服务器上。我每次只做三件事——写 Markdown、`git commit`、`git push`。推送到 `main` 分支后，workflow 跑完，网址就更新了。

## 踩过的一个小坑

Jekyll 默认**不发布日期在未来的文章**。如果我把文章的 `date` 写成明天，它就会安静地不出现在列表里。所以写完一篇要先看一眼日期，或者等那一天到来。

另一个坑在 front matter：开头的两行 `---` 必须写成 YAML 语法，少一个冒号，标题和标签就会失效。

## 下一步

- 把首页的项目卡片都换成真正做过的东西
- 继续写 C 语言和 Git 的笔记
- 学会看 Actions 的构建日志，出问题能自己定位
