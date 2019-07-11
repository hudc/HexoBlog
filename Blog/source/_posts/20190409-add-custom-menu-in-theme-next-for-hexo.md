---
title: 为Hexo的Next主题增加自定义menu菜单
tags: [Hexo]
categories: [技术]
date: 2019-04-09 15:18:51
updated: 2019-04-09 15:18:51
permalink: add-custom-menu-in-theme-next-for-hexo
---

## 1 写在前面
现在Hexo使用的主题当中，Next主题是比较流行的，查看Next主题的_config.yml，其中有8个默认定义的menu菜单，分别是home、about、tags、categories、archives、schedule、sitemap、commonweal 。通过参考tags、categories两个菜单，可以实现菜单的定制化。
<!--more-->
## 2 达到效果
在Next主题的首页显示自定义的菜单，如读书、技术等。

## 3 实现方式
参考categories配置，增加新行`读书: /categories/read || book`，其中read是我们在写文章post的时候添加的分类（可根据实际情况配置），book是新增菜单的图标，可以在[fontawesome.com](https://fontawesome.com/v4.7.0/icons/)挑选一个喜欢的图标配置即可。
同样，我们也可以使用`技术: /tags/tech || wrench`，实现按照标签进行自定义菜单。
配置完成后，显示的效果与归档archieves类似，右边是符合过滤条件的文章列表。
