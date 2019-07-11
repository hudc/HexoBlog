---
title: 在Hexo中添加Html属性功能
tags: [Hexo,html,Markdown]
categories: [技术]
date: 2019-04-09 09:56:44
updated: 2019-04-09 09:56:44
permalink: add-html-function-in-hexo
---

## 1 写在前面
众所周知，Hexo网站的整体样式、风格由主题Theme预先确定，Markdown文件中主要专注于文章内容的编写，经过Hexo渲染后形成静态html页面。但是，Hexo并没有限制博主通过在MD文件中增加Html、JavaScript等代码来实现除Markdown语法以外的功能，比如实现Button、Tabs、Menu、Navigation等静态Html常用的功能，本文将通过在Markdown中增加Tabs页为例子介绍实现方法，使得非技术人员也可以在Blog中实现很多出彩的功能。
<!--more-->
## 2 达到效果
如：在某篇文章中作三个不同的城市简单介绍，通常使用无序列表或者表格的方式，这次我们采用Tabs方式（效果如下）。

{% raw %}
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
body {font-family: Arial;}

/* Style the tab */
.tab {
  overflow: hidden;
  border: 1px solid #ccc;
  background-color: #f1f1f1;
}

/* Style the buttons inside the tab */
.tab button {
  background-color: inherit;
  float: left;
  border: none;
  outline: none;
  cursor: pointer;
  padding: 14px 16px;
  transition: 0.3s;
  font-size: 17px;
}

/* Change background color of buttons on hover */
.tab button:hover {
  background-color: #ddd;
}

/* Create an active/current tablink class */
.tab button.active {
  background-color: #ccc;
}

/* Style the tab content */
.tabcontent {
  display: none;
  padding: 6px 12px;
  border: 1px solid #ccc;
  border-top: none;
}
</style>

<p>Tabs</p>
<p>Click on the buttons inside the tabbed menu:</p>

<div class="tab">
  <button class="tablinks" onclick="openCity(event, 'London')">London</button>
  <button class="tablinks" onclick="openCity(event, 'Paris')">Paris</button>
  <button class="tablinks" onclick="openCity(event, 'Tokyo')">Tokyo</button>
</div>

<div id="London" class="tabcontent">
  <h3>London</h3>
  <p>London is the capital city of England.</p>
</div>

<div id="Paris" class="tabcontent">
  <h3>Paris</h3>
  <p>Paris is the capital of France.</p> 
</div>

<div id="Tokyo" class="tabcontent">
  <h3>Tokyo</h3>
  <p>Tokyo is the capital of Japan.</p>
</div>

<script>
function openCity(evt, cityName) {
  var i, tabcontent, tablinks;
  tabcontent = document.getElementsByClassName("tabcontent");
  for (i = 0; i < tabcontent.length; i++) {
    tabcontent[i].style.display = "none";
  }
  tablinks = document.getElementsByClassName("tablinks");
  for (i = 0; i < tablinks.length; i++) {
    tablinks[i].className = tablinks[i].className.replace(" active", "");
  }
  document.getElementById(cityName).style.display = "block";
  evt.currentTarget.className += " active";
}
</script>
{% endraw %}

## 3 实现方式
技术实现主要是使用Hexo的Raw标签和html语法，只需要在Markdown文件中编辑即可。

### 3.1 使用Raw标签
Hexo提供Raw标签，用于实现在MD文件中添加不需要Hexo渲染的代码，Hexo会将Raw标签中的内容直接复制到html文件中。Hexo官网[Tag Plugins](https://hexo.io/docs/tag-plugins)介绍。使用时将我们编辑的html代码替换标签中的content即可。
```
{% raw %}
content
{% endraw %}
```

### 3.2 实现Tabs的html代码
为了体现html的规范性，我从[w3schools.com](https://www.w3schools.com/howto/howto_js_tabs.asp)获取的Tabs代码，大家可以拷贝w3schools中的例子代码，按照自己的内容修改即可，下面是本次例子的代码，大家直接拷贝粘贴到MD文件中可以直接使用。
```
{% raw %}
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
body {font-family: Arial;}

/* Style the tab */
.tab {
  overflow: hidden;
  border: 1px solid #ccc;
  background-color: #f1f1f1;
}

/* Style the buttons inside the tab */
.tab button {
  background-color: inherit;
  float: left;
  border: none;
  outline: none;
  cursor: pointer;
  padding: 14px 16px;
  transition: 0.3s;
  font-size: 17px;
}

/* Change background color of buttons on hover */
.tab button:hover {
  background-color: #ddd;
}

/* Create an active/current tablink class */
.tab button.active {
  background-color: #ccc;
}

/* Style the tab content */
.tabcontent {
  display: none;
  padding: 6px 12px;
  border: 1px solid #ccc;
  border-top: none;
}
</style>

<p>Tabs</p>
<p>Click on the buttons inside the tabbed menu:</p>

<div class="tab">
  <button class="tablinks" onclick="openCity(event, 'London')">London</button>
  <button class="tablinks" onclick="openCity(event, 'Paris')">Paris</button>
  <button class="tablinks" onclick="openCity(event, 'Tokyo')">Tokyo</button>
</div>

<div id="London" class="tabcontent">
  <h3>London</h3>
  <p>London is the capital city of England.</p>
</div>

<div id="Paris" class="tabcontent">
  <h3>Paris</h3>
  <p>Paris is the capital of France.</p> 
</div>

<div id="Tokyo" class="tabcontent">
  <h3>Tokyo</h3>
  <p>Tokyo is the capital of Japan.</p>
</div>

<script>
function openCity(evt, cityName) {
  var i, tabcontent, tablinks;
  tabcontent = document.getElementsByClassName("tabcontent");
  for (i = 0; i < tabcontent.length; i++) {
    tabcontent[i].style.display = "none";
  }
  tablinks = document.getElementsByClassName("tablinks");
  for (i = 0; i < tablinks.length; i++) {
    tablinks[i].className = tablinks[i].className.replace(" active", "");
  }
  document.getElementById(cityName).style.display = "block";
  evt.currentTarget.className += " active";
}
</script>
{% endraw %}
```

## 4 写在最后
以上通过Tabs例子实现在MD中增加html功能，大家也可以拓展实现JavaScript等脚本语言功能。
>参考资料：
>Hexo官网Tag Plugins标签[Tag Plugins](https://hexo.io/docs/tag-plugins)
>W3schools官网html代码[w3schools.com](https://www.w3schools.com/howto/howto_js_tabs.asp)
