---
title: Docsify是最简单的博客系统
date: 2019-01-06 18:11:17
updated: 2019-01-06 18:11:17
tags: 
- Docsify
- blog搭建
- Markdown 
categories: 
- 技术 
permalink: docsify-is-the-simplest-blog

---

## 1.什么是Docsify
官方定义：一个神奇的文档网站生成工具。通俗点说：是由一个html文件和几个js文件构成的CMS（内容管理系统），无需安装复杂的运行环境，无需安装数据库，无需进行繁琐的配置，Markdown文件就是它的内容。
<!--more-->
## 2.用它能做什么
标准的回答应该是，用它来做能做的事情。如果必须举例子，则可以用来搭建blog、当个人笔记系统、当个人知识库、用来写本书、整理读书笔记、团队协作写文档等等，只要与文字相关都可以用它来承载，只要用Markdown书写的文字，都可以用它来渲染和展现。
## 3.同类工具对比
### 3.1与Wordpress比较
Wordpress是一个老牌的、成熟的CMS系统。
优势：有很成熟的主题、插件系统，网上资料丰富，相关人才很多，在成功案例方面涵盖大公司网站和个人blog。后期使用方面优势明显，只需浏览器就可以编辑和发布文章。
缺点：需要占用较高的硬件资源，需要安装数据库、PHP、nginx（Apache）等基础环境。内容源文件需要单独备份保存，比如.md源文件。
### 3.2与Hexo比较
Hexo是比Wordpress更加轻量级的blog系统。
优势：把.md文件直接渲染成静态.html文件，通过静态环境（如Github）部署。
缺点：因为将.md文件渲染成html文件的过程需要在电脑上完成，而且电脑端环境需要做一定的配置，使得不能随时、随地、任意设备编辑和发布文章。
### 3.3Docsify
非常轻量，主文件只有几十kb。远端环境如果使用GitHub Pages，无需安装，只要简单配置即可。本地环境在熟悉后重新搭建只需要几分钟，在对Docsify原理熟悉后，无需在本地搭建环境，直接编写Markdown文章内容，然后直接发布即可，所见即所得。
## 4.本地部署
为什么说是**本地**部署呢，这就是神奇之处，如果最终是部署到Github等远端，实际上在本地只需要写.md文件就可以，根本就不需要任何环境。但是为了让大家熟悉Docsify和实现在本地预览，通过以下步骤可以在本地装一个环境。默认本地已经安装node.js环境，如果没有安装，可直接到node官网下载安装包即可。
### 4.1下载安装包
在shell下（或任何命令提示符）执行`npm i docsify-cli -g`。
### 4.2初始化目录
在本地创建一个工作目录文件夹，在shell下进入该文件夹执行`docsify init ./docs`。然后查看docs文件夹，有三个文件。
  * index.html       //可以理解为是主程序
  * README.md  //可以理解为就是网站内容
  * .nojekyll          //不是太重要的文件（用于阻止 GitHub Pages 忽略掉下划线开头的文件）

### 4.3启动服务
在shell中执行`docsify serve docs`，终端屏幕提示http://localhost:3000 ，表示服务已启动。服务支持实时加载，在更改参数和文档内容后，不需要重新启动服务。
在本机浏览器中输入http://localhost:3000 ，打开网站，页面显示的内容就是README.md文件中的内容，使用记事本修改一下内容，网页内容也同步修改。
### 4.4本地部署完成
截至到本步骤，大家对docsify已经有了一定的了解，并且本地环境也具备了。这个时候我推荐大家把docsify官网的帮助文档看一遍，内容不是很多，30分钟应该可以看完，这样可以对docsify有一个比较全面的了解。
## 5.多页面实现
服务启动以后，默认只显示一个单页面，也就是README.md文件内容，左边侧边栏是README.md文档中的标题大纲。Docsify可以通过配置在左边实现侧边栏，类似blog菜单的树形结构。
### 5.1md文件与URL的对应关系
本部分基于官方数据例子做说明。其中README.md文件是默认文件，在输入URL时可以选择不输入，其他.md文件需要在URL中输入文件名称，不需要.md结尾。
假设docs的目录结构如下：
```
-| docs/
  -| README.md
  -| guide.md
  -| zh-cn/
    -| README.md
    -| guide.md
```
则实际访问的URL地址如下：
```
docs/README.md        => http://domain.com
docs/guide.md         => http://domain.com/guide
docs/zh-cn/README.md  => http://domain.com/zh-cn/
docs/zh-cn/guide.md   => http://domain.com/zh-cn/guide
```
### 5.2侧边栏配置方法：
1. 在index.html页面中，找到`window.$docsify`，然后在其中加入`loadSidebar: true,`（语句以逗号结尾）。

```javascript
<script>
  window.$docsify = {
    loadSidebar: true,
  }
/script>
```
2. 在docs目录中创建'_sidebar.md'文件，文件内容如下。其中[方括号]内容的层级显示，按照实际需要调整即可，（圆括号）内容是实际的文档结构。默认README.md文件名可以不写。

```
* [1.Home](/)
* [2.Guide](/guide.md)
    * [1.Guide-Home](/zh-cn/)
    * [2.Guide-Info](/zh-cn/guide.md)
```

## 6.参考资料
[官网英文](https://docsify.js.org/)
[官网中文](https://docsify.js.org/#/zh-cn/)
