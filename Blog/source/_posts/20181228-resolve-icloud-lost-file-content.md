---
title: 用iCloud同步Markdown文档丢失内容的问题及解决
date: 2018-12-28 18:11:17
updated: 2018-28-28 18:11:17
tags: 
- iCloud 
- Markdown
categories: 
- 技术 
permalink: resolve-icloud-lost-file-content

---

## 1.问题背景
问题背景是经常采用Win、iphone、ipad共同编写同一个Markdown文档，在Win上采用Typora，iphone和ipad上使用Mweb，文档数据采用iCloud进行同步。
## 2.问题现象
在Mweb上对A文件编辑了一部分内容，比如'12345'，然后再Typora中继续编写'abcde‘，并保存成功。可是偶尔会出现文档恢复到了'12345’的状态，'abcde'内容消失了，由此引发的数据丢失问题，让人非常痛苦。
<!--more-->
## 3.问题原因
经过分析和试验后，发现问题出在iphone上的Mweb端，当然这不是Mweb本身的问题。因为在iphone和ipad的软件设计中很少有关闭软件并退出的设计，比如Mweb软件在编写文件内容后，退出到iphone主界面或切换到其他应用就可以了，Mweb会自动保存。其实这时候iCloud也帮助我们把文件内容同步到了Win端，当我们通过Typora再次编辑文件后，iCloud再一次把文件进行了同步，截至目前都没有什么问题。可是当我们再次打开iphone上的Mweb时，因为Mweb一直没有关闭，Mweb所展现的内容还是停留在最后Mweb编辑的时候，没有包含在后面Typora中编辑的内容，这时候Mweb软件即时对文件内容进行了保存，则在此时刻iCloud上的内容就已经被过时的内容覆盖了，而且iCloud又把过时的内容给同步到了Win端，这时候我们就发现数据丢失了。
## 4.问题解决
有两种解决办法：
1. 采用具有版本管理功能的云盘，比如Dropbox，一旦发现版本有问题则及时进行版本回退找回。
2. 在iphone、ipad上使用Mweb编辑文件后，直接手工退出并关闭软件，下次再打开文件时，看一下iCloud有没有进行文件同步更新，如果有更新则再打开即可。

知一写于2018年12月29日凌晨