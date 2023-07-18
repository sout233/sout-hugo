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

```yml
name: Auto Post From Issues

on:
  issues:
    types: ['labeled']

jobs:
  build:
    if: ${{ github.event.label.name == 'already' || github.event.label.name == 'pre-pub'}}
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      
      - name: 从issue创建文章
        run: |
          label="${{ github.event.label.name }}"
          case "$label" in
          "already")
          mkdir -p content/post/${{ github.event.issue.title }}
          cat > "content/post/${{ github.event.issue.title }}/${{ github.event.issue.title }}.md" << EOF
          ---
          ${{ github.event.issue.body }}
          EOF
          ;;
          "pre-pub")
          mkdir -p content/post/${{ github.event.issue.title }}
          cat > "content/post/${{ github.event.issue.title }}/${{ github.event.issue.title }}.md" << EOF
          ---
          ${{ github.event.issue.body }}
          > 该文章为自动预发布，可能存在些许误差，请以already版本为主。
          EOF
          ;;
          esac
      
      - name: 提交PR
        uses: peter-evans/create-pull-request@v3
        with:
          delete-branch: true
          title: "发布请求: ${{ github.event.issue.title}}"
          body: |
            文章将自动部署到: https://sout.eu.org
            将关闭以下issue: #${{ github.event.issue.number }}
```

发布的issue需要指定label才可触发build，该action完成后合并pr，即可触发gh-page的工作流，然后就会推送到vercel上。

该文章使用Github Issues发布。
