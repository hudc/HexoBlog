---
title: 在Hexo的next主题中，增加本地搜索search功能
tags: [Hexo]
categories: [技术]
date: 2019-04-19 14:37:28
updated: 2019-04-19 14:37:28
permalink: add-local-search-in-hexo-next

---

在Hexo中发布的文章可以通过分类和标签进行文章分组显示，但是如果只是想查询文章中的某些关键字或者文章数量较多的情况下，如果有搜索功能，将对读者查找文章有很大帮助，Hexo的hexo-generator-searchdb插件帮助Hexo实现了本地搜索功能，安装和配置步骤简单。
<!--more-->

## 1 配置步骤
1. 安装插件，在Hexo的工作目录执行命令`#npm install hexo-generator-searchdb --save` 。
2. 修改配置文件（./themes/next/_config.yml），查找`local_search:`标签，配置参数`enable: true` 。
3. 将以下参数增加到Hexo的主配置文件中（./_config.yml） 。
```
search:
  path: search.xml   #在public目录的根目录下生成search.xml 文件，用于存储网站文章的文字数据.
  field: post
  format: html
  limit: 10000
```

## 2 生成静态文件
重新生成静态文件，执行命令`#hexo g` ，打开浏览器查看页面即可。

## 3 问题解决
1. 在进行searchdb安装配置时，如果不配置第3步骤中的Hexo主配置文件，会出现搜索页面打不开的情况，有一个圆圈一直在旋转，这时只要增加Hexo主配置文件中的代码即可。

2. 另外，这里给出的searchdb的插件安装命令不是全局性的，是在Hexo工作目录中执行的命令，比如有的人在同一台服务器上有多个Hexo站点，则需要在每一个Hexo工作目录中执行命令。

## 4 参考资料
[hexo-generator-searchdb](https://github.com/theme-next/hexo-generator-searchdb)
