---
title: 使用Github Issues发布博客文章
description: 穷人必备小技能（
slug: gh-issues-post
date: 2023-07-18 00:00:00+0000
categories:
    - Tech
tags:
    - Web
---

之前发布文章需要先在本地修改，然后再push到仓库，非常麻烦，以至于很长时间都没更新。

前两天学rust的时候看到一个人用rust做的blog，竟然是使用GitHub issues来发布文章的。

由于我的blog仓库是自动触发的vercel build，故想到是否可以使用GitHub Action来自动创建文章。

事实证明是可以的，以下是action脚本：



发布的issue需要指定label才可触发build，该action完成后合并pr，即可触发gh-page的工作流，然后就会推送到vercel上。

该文章使用Github Issues发布。
> 该文章为自动预发布，可能存在些许误差，请以already版本为主。
