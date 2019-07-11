---
title: 静态网站生成器Hexo、Gitbook、Vuepress、Docsify、Docute、Nuxt
tags: [blog搭建,Hexo,Gitbook,Vuepress,Docsify,Docute,Nuxt]
categories: [技术]
date: 2019-04-13 11:29:55
updated: 2019-04-13 11:29:55
permalink: static-site-generator-hexo-gitbook-vuepress-and-so-on
---

GitBook在不久前改版了，新版本向着商业化、平台化运作了，而作为开源工具的CLI也不在提供了（[Gitbook V2 Important differences](https://docs.gitbook.com/v2-changes/important-differences)），查找静态网站生成器代替方案记录如下。

<!--more-->

## 1 Hexo
Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
Hexo 配合他的主题模块，比如Next主题，可以作为非常简洁方便的静态博客系统。
[Hexo官网](https://hexo.io/zh-cn/docs/) 。

## 2 Nuxt
Nuxt.js 是一个基于 Vue.js 的通用应用框架。通过对客户端/服务端基础架构的抽象组织，Nuxt.js 主要关注的是应用的 UI渲染。Nuxt.js 的目标是创建一个灵活的应用框架，你可以基于它初始化新项目的基础结构代码，或者在已有 Node.js 项目中使用 Nuxt.js。
Nuxt 更像是为构建应用程序而生的，而不是独立的内容静态网站。
[Nuxt.js官网](https://zh.nuxtjs.org/guide) 。

## 3 Docsify
Docsify 是一个动态生成文档网站的工具。不同于 GitBook、Hexo 的地方是它不会生成将 .md 转成 .html 文件，所有转换工作都是在运行时进行。
Docsify是基于 Vue，完全的运行时驱动，不需要渲染html，所以对 SEO 不够友好。如果不关注 SEO，安装简单化不想有大量依赖，他是比较好的选择，比如公司或这团队内部的文档系统。
[docsify 官网](https://docsify.js.org/#/zh-cn/) 。

## 4 Docute
Docute 本质上就是一个 JavaScript 文件，它可以获取 Markdown 文件并将它们呈现为单页面应用。它完全由运行时驱动，因此并不涉及服务端组件，这就意味着没有构建过程。你只需创建一个 HTML 文件和一堆 Markdown 文档，你的网站就差不多完成了！
Docute 与Docsify 基本一样，只是在文件大小和UI 及不同的使用方式，Docute网站有其差异介绍。
[Docute 官网](https://docute.org/zh/) 。

## 5 GitBook
GitBook 是一个现代的文档平台，团队或个人可以在其上编写产品、API接口文档以及团队内部知识库。
GitBook 改版之后，感觉的团队更专注于商业产品而不是开源工具，同时CLI工具不再提供了，所以无法实现个性化部署，所以不做介绍，有兴趣的可以看其官网。
[GitBook 官网](https://docs.gitbook.com/) 。

## 6 VuePress
VuePress 是基于Vue开发的平台，功能上实现了GitBook功能。
VuePress 展示页面与Docsify类似，但是与Docsify不同的是，预先渲染html。
[VuePress官网](https://vuepress.vuejs.org/zh/) 。
