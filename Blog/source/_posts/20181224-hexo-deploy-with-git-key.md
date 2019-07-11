---
title: Hexo采用git类型deploy部署时密钥key配置
date: 2018-12-24 18:11:17
updated: 2018-12-24 18:11:17
tags: 
- Hexo 
categories: 
- 技术 
permalink: hexo-deploy-with-git-key

---

## 1.生成SSH Key
生成SSH Key：注意C是大写。
```
$ ssh-keygen -t rsa -C "yourname@youremail.com"  
```
连续输入回车即可，也可以输入密码。
<!--more-->
当看到以下界面时，表示Key生成成功。
```
The key's randomart image is:
+---[RSA 2048]----+
|*=*+o.           |
|.=O==o    5      |
| +++Bo  5        |
|.o+...  .        |
|+.=.   ES.       |
|++o8o . .+=  5   |
|o.=.. ..o..  5   |
|.+.o.8 .  .  5   |
|  o+o. 5         |
+----[SHA256]-----+
```
## 2.配置Key
仔细看刚才输出的字符信息，找到id_rsa.pub文件的对应目录，用记事本等工具打开，拷贝文件中内容。
登陆github，选择yourname.github.io这个Repository，选择左边Deploy Key，选择右边Add deploy key，将刚才复制的id_rsa.pub中的内容粘贴到Key中，勾选Allow write access，然后点击Add Key。
## 3.测试连接
输入命令
```
$ ssh -T git@GitHub.com
```
如果显示的界面中有以下字符，表示连接成功。
```
You've successfully authenticated
```