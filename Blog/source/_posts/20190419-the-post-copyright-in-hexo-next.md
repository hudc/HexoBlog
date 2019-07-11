---
title: 使用Hexo的next主题，配置POST文章文末的版权信息
tags: [Hexo]
categories: [技术]
date: 2019-04-19 14:23:14
updated: 2019-04-19 14:23:14
permalink: the-post-copyright-in-hexo-next

---

在每篇文章末尾默认增加文章作者、链接以及版权信息，是部分博主所需要的，而Hexo的next（v7.1.0）主题默认就集成了该功能，只需要在设置中启用即可。配置方式简要描述，实际效果与下面信息类似。
<!--more-->

```
本文作者： Hudc
本文链接： http://amdoing.com/static-site-generator-hexo-gitbook-vuepress-and-so-on/
版权声明： 本博客所有文章除特别声明外，均采用 BY-NC-SA 许可协议。转载请注明出处！
```

## 1 配置步骤
修改next主题的配置文件（./themes/next/_config.yml），搜索到`creative_commons:`标签， sidebar参数表示在侧边栏有一个版权的图片链接，post参数表示在每一篇文章末尾自动增加本文作者、本文链接、版权声明三个信息，language参数表示点击链接后显示的版权信息的语言。

```
creative_commons:
  license: by-nc-sa
  sidebar: true
  post: true
  language: deed.zh
```

如果想个性化配置版权信息，可修改配置文件(./themes/next/layout/_partials/post/post-copyright.swig)，如果想修改显示的样式可修改配置文件(./themes/next/source/css/_common/components/post/post-copyright.styl) 。

## 2 相关文章
[hexo next 主题修改底部版权信息](https://hoxis.github.io/hexo-next-copyright.html)
