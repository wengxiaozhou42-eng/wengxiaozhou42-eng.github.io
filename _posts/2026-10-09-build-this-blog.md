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

需要改的地方只有四处：

| 文件 | 作用 |
| --- | --- |
| `_config.yml` | 站点标题、描述、语言和时区 |
| `index.html` | 首页：自我介绍、文章列表、项目卡片 |
| `_posts/*.md` | 每一篇文章，文件名是 `YYYY-MM-DD-标题.md` |
| `assets/style.css` | 配色和排版，颜色都写在顶部的 CSS 变量里 |

## 发布流程

仓库里已经带了一个 GitHub Actions workflow：`.github/workflows/pages.yml`。它的工作很直接——检出代码、用 Jekyll 编译、把生成的 `_site` 目录上传为 Pages 产物、然后部署。

```yaml
- name: Build with Jekyll
  uses: actions/jekyll-build-pages@v1
  with:
    source: ./
    destination: ./_site
```

因此我本地不需要装 Ruby 或 Jekyll：编译发生在 GitHub 的服务器上。我只做三件事——写 Markdown、`git commit`、`git push`。推送到 `main` 分支后，workflow 跑完，网址就更新了。

## 踩过的一个小坑

Jekyll 默认**不发布日期在未来的文章**。如果我把文章的 `date` 写成明天，它就会安静地不出现在列表里。所以写完一篇要先看一眼日期，或者等那一天到来。

## 下一步

- 给首页换一张真实的头像
- 把项目卡片换成自己真正做过的东西
- 学会用 `git log` 和 `git diff` 检查每次改动
