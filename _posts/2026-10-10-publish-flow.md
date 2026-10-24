---
layout: post
title: 第一次自己发布文章
date: 2026-10-10
excerpt: 从新建 Markdown 文件到线上能打开，我把每一步都记了下来。
tags:
  - 建站
  - 发布
---

这是我第一次自己加文章。前面几篇是搭博客的时候一起写的，这一篇是从头写、提交、推送，然后等它自己变成网页。

## 我做了这几步

1. 在 `_posts` 里新建 `2026-10-10-publish-flow.md`
2. 开头写 front matter：`layout: post`、标题、日期、摘要、标签
3. 正文用 Markdown 写
4. `git add`、`git commit`、`git push`
5. 打开仓库的 Actions 页面，等 workflow 跑完
6. 刷新网址，看到这一篇

## 第一次写错的地方

front matter 里少写了一个冒号，标题和标签就没生效，页面上直接显示了原文。改回来重新推送就正常了。

所以现在发布前我会检查三样：

- front matter 的 `---` 有没有配对
- `layout: post` 有没有写
- `date` 是不是未来的日期（Jekyll 默认不发布未来文章）

## 发布以后的感觉

前面几篇是“模板自带的”，这一篇是我自己写完、自己推上去的。看到网址里真的多了一页，才觉得这个博客是我的。
