---
title: 选择和配置hexo的第一个主题
date: 2018-12-24 18:11:17
updated: 2018-12-24 18:11:17
tags: 
- Hexo 
categories: 
- 技术 
permalink: hexo-select-and-config-the-first-theme

---


## 1.选择主题
Hexo官网上提供了[主题清单](https://hexo.io/themes/)，截至到2018-12-16，清单中有232个主题，在Hexo运行起来后，可以在里面选一个自己能接受的主题，不要在选择上花费太多的时间，以后会有很多时间用来美化博客，毕竟写博客是长期的事情。我当时选的是Maupassant。
<!--more-->
作者介绍文章：[大道至简——Hexo简洁主题推荐](https://www.haomwei.com/technology/maupassant-hexo.html)
github网址：[maupassant-hexo](https://github.com/tufu9441/maupassant-hexo)
## 2.安装主题
从github上下载，并安装。
```
$ git clone https://github.com/tufu9441/maupassant-hexo.git themes/maupassant
$ npm install hexo-renderer-pug --save
$ npm install hexo-renderer-sass --save
```
## 3.配置主题
修改本地blog根目录下的_config.yml文件，将theme后面的参数修改为maupassant。
```
theme: maupassant
```
maupassant主题支持多语言，到themes/maupassant主题的languages目录下，留下对应语言的yml文件，删除其它即可。maupassant详细的配置参数可以参考github项目的[README.md](https://github.com/tufu9441/maupassant-hexo)文件。
## 4.部署主题
执行以下命令。
```
hexo clean
hexo g
hexo s
hexo d
```
到目前为止，新主题就部署成功了。其它主题的安装和部署方式与此类似，主要是配置参数的不同，可详细看一下对应的README说明文件。
