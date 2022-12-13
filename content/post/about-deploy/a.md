---
title: 一次部署博客的记录
description: 健忘（
slug: blog-deploy
date: 2022-12-13T00:27:44Z
image: https://images.unsplash.com/photo-1670588761146-2425a98a9a5a?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDZ8aVVJc25WdGpCMFl8fGVufDB8fHx8&auto=format&fit=crop&w=500&q=60
categories:
    - 建站小寄巧
tags:
    - 建站小寄巧
---

在此记录建站过程，用作参考，也避免以后遗忘。

## 准备工作

本站采用全静态（穷死），方案是Github（仓库）+ Codespace（工作环境）+Vercel（托管）+Netlify（DNS）

（因为Netlify一直部署失败所才用的Vercel来托管）

主题用的[hugo-theme-stack](https://github.com/CaiJimmy/hugo-theme-stack)

## 部署Codespace

从[模板](https://github.com/CaiJimmy/hugo-theme-stack-starter)创建，然后切到fork后的仓库，单击Code绿色按钮，点击创建Codespace。

## 修改配置文件

参照[stack文档](https://stack.jimmycai.com)进行修改，不多赘述。

## 部署到Vercel

登录Vercel，从Github仓库创建，部署指令，输出目录和环境变量需要修改为：

```
Build Command:amazon-linux-extras install golang1.11 && hugo --gc --minify
Output Directory:public
环境变量：
HUGO_VERSION    0.108.0(为hugo_ext的最新版本)
```
![部署参考图](https://i.328888.xyz/2022/12/13/yRE8L.png)
![环境变量的配置参考图](https://i.328888.xyz/2022/12/13/yR7yk.png)

## 域名配置

DNS CNAME过去就行

~~希望不会懒死以后的我~~

## SEO

### Open Graph

修改`config/_default/params.toml`即可（可参考stack文档）

like this:

```
[opengraph.twitter]
site = "sout_Nantang"
card = "summary_large_image"
```

### 主动提交

将域名和[sitemap](https://sout.mikamika.ga/sitemap.xml)提交给各大搜索引擎

提交平台如下：
- https://www.bing.com/webmasters
- https://ziyuan.baidu.com/site/index
- https://search.google.com/search-console

## 常见问题

### Vercel 预览 部署失败

> 关了预览部署就行，git page编译容易报错
> ![关闭部署预览参考图](https://i.328888.xyz/2022/12/13/yRzqU.png)

### sitemap或搜索地址错误

> config没设置正确，看看`config/_default/config.toml`配置对了没有

--------

> Photo on [Unsplash](https://unsplash.com/)