---
title: VuePress安装和初始化配置
tags: [VuePress,blog搭建]
categories: [技术]
date: 2019-04-14 22:00:40
updated: 2019-04-14 22:00:40
permalink: vuepress-install-and-init-config

---

## 1 写在前面
前期已经介绍了Hexo和Docsify两个系统的功能和安装，其中Hexo功能上更偏向于blog，Docsify功能上更偏向于文档和书籍的整理，Hexo会预先渲染成html，Docsify不预先渲染。VuePress则综合了他们的功能和特点。VuePress目前的功能更适合用于文档和书籍整理，同时因为预先渲染html，有利于静态部署。
<!--more-->

## 2 达到效果
在本地运行VuePress，并对其有简单了解，更详细的内容可参见[VuePress官网](https://vuepress.vuejs.org/zh/guide/) 。

## 3 安装运行
* 安装程序。执行命令 `npm install -g vuepress` ，Node.js 版本需要 >= 8 。
* 创建工作目录。创建工作目录 `mkdir vuepressdir` ， 在vuepressdir工作目录中创建文档目录 `mkdir docs` 。并在docs中创建README.md文件，并输入一段文字（在启动VuePress服务后，作为首页内容显示），可通过在docs目录中执行命令实现 `echo '# Hello VuePress!' > README.md` 。
* 启动服务。在vuepressdir目录中执行命令 `vuepress dev docs` 。
* 访问服务。在浏览器中访问 http://localhost:8080/ 。 在浏览器中显示 Hello VuePress! ，即安装成功。
* 生成静态的 HTML 。执行命令 `vuepress build docs` ，可生成静态的 HTML ，注意目录docs中的文件数量变化。
* 也可以在目录vuepressdir中创建 `package.json` 文件，并在其中增加如下代码，然后可以使用`npm run docs:dev` 和 `npm run docs:build` 两个命令启动服务和生成静态文件。
```
{
  "scripts": {
    "docs:dev": "vuepress dev docs",
    "docs:build": "vuepress build docs"
  }
}
```

## 4 目录结构
.vuepressdir
├─ docs
│  ├─ README.md
│  └─ .vuepress
│     └─ config.js  //VuePress 网站必要的配置文件，需自行创建。
│     └─ dist          //生成的静态HTML文件夹。
└─ package.json

## 5 config配置文件
需自行在docs/.vuepress目录中创建config.js配置文件，配置文件中内容格式如下，具体详细配置参数可参考VuePress网站：[配置文件](https://vuepress.vuejs.org/zh/guide/basic-config.html#%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6) ， [基本配置](https://vuepress.vuejs.org/zh/config/#%E5%9F%BA%E6%9C%AC%E9%85%8D%E7%BD%AE) ，[主题配置](https://vuepress.vuejs.org/zh/default-theme-config/) 。
以下是一个简单的配置文件样例。
```
// .vuepress/config.js
module.exports = {
  title: 'Hello VuePress',
  description: 'Just playing around',
  themeConfig: {
    nav: [
      { text: 'Home', link: '/' },
      { text: 'Guide', link: '/guide/' },
      { text: 'External', link: 'https://baidu.com' },
    ],
	sidebar: [
      '/',
      '/page-a',
      ['/page-b', 'Explicit link text']
    ],
	sidebarDepth: 2
	
  }
}
```

## 6 写在后面
现在你已经可以在浏览器中看到VuePress的效果了，但是仅仅是个简单空无一物的网站，建议在开始正式用VuePress之前，认真浏览VuePress官网的指南文档，花不了多长时间，但对你后期的使用将有很大益处。

