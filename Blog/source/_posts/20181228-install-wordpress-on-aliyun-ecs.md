---
title: 在阿里云ECS服务器上安装WordPress步骤
date: 2018-12-28 18:11:17
updated: 2018-12-28 18:11:17
tags: 
- WordPress
- blog搭建
categories: 
- 技术 
permalink: install-wordpress-on-aliyun-ecs

---

本文档记录了在阿里云ECS服务器上安装WordPress的操作步骤和命令，阿里云ECS服务器采用CentOS系统，运行环境安装LNMP，软件包从仓库或者官网下载。但本文没有对各步骤进行介绍说明，如想了解各步骤详细说明，可参考文档后面的参考文献，或Google、Baidu查询。
<!--more-->

## 1.安装前准备
更新系统软件命令 `\# yum update`
## 2.安装新仓库
为了可以使用 CentOS 系统的包管理工具去安装更多的东西，需要单独安装额外的软件仓库。EPEL和IUS，IUS 仓库里面有需要的一些新的软件包，比如 PHP 7。
`\# sudo yum install epel-release -y`
`\# sudo yum install https://centos7.iuscommunity.org/ius-release.rpm -y`
## 3.安装nginx
NGINX 软件包在 EPEL 仓库里。安装结束并启动服务以后，可以在浏览器上使用服务器的 IP 地址，或者指向这个地址的域名访问服务器指定的目录了。
安装命令 ` \# sudo yum install nginx -y`
启动命令  `\# sudo systemctl start nginx`
开启自启动命令 `\# sudo systemctl enable nginx`
配置 nginx 
重启 nginx 或者重新加载 nginx配置文件命令`\# sudo systemctl reload nginx`
## 4.安装PHP
要让 nginx 能够执行 php 文件，需要去安装一下 php-fpm，软件在 IUS 仓库里。
安装命令 `\# sudo yum install php70u-fpm -y`
启动命令 `\# sudo systemctl start php-fpm`
开机自启动命令`\# sudo systemctl enable php-fpm`
安装 PHP 扩展，为了可以正常运行WordPress，Drupal等 PHP 应用，你需要再安装一些其它的 PHP 扩展。下面是一些常用的 PHP 扩展：
安装扩展包命令 `\# sudo yum install php70u-gd  php70u-mysqlnd php70u-pdo php70u-mcrypt php70u-mbstring php70u-json php70u-opcache php70u-xml -y`
重新加载 PHP-FPM命令 `\# sudo systemctl reload php-fpm`
测试php是否安装成功，使用 php 的 phpinfo(); 函数，方法是在你的虚拟主机根目录下面，创建一个 php 文件，命名为 phpinfo.php，然后在这个文件里输入：`<?php phpinfo(); ?>`
保存文件并退出。在浏览器里打开刚才创建的这个 php 文件。

## 5.安装Mysql
下载MySql安装包命令 `\# rpm -ivh http://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm`
安装MySql命令 `\# yum install -y mysql-server`
设置开机启动Mysql命令 `\#  systemctl enable mysqld.service`
检查是否已经安装了开机自动启动命令 `\# systemctl list-unit-files | grep mysqld`
设置开启服务命令 `\# systemctl start mysqld.service`
查看MySql默认密码命令 `\#  grep 'temporary password' /var/log/mysqld.log`
登陆MySql，输入用户名和密码命令 `\# mysql -uroot -p`
设置数据库密码   `set password=password(xxx_db');`
Mysql安全配置向导 `\# mysql_secure_installation`
创建数据库
`\# mysql -uroot -p`
`create database wdpress_db`
## 6.安装WordPress
下载Wordpress，`\# wget  https://cn.wordpress.org/wordpress-5.0.2-zh_CN.tar.gz`
解压缩 `\# tar xzvf wordpress-5.0.2-zh_CN.tar.gz`
把解压缩的Wordpress中的所有内容放在wpblog文件夹中。
在浏览器中输入   http://x.x.x.x/wp-admin
## 7.问题处理
### 7.1安装nginx后无法访问欢迎页面
原因是没有在阿里云控制台的安全组记录中，添加入方向规则的HTTP（80）协议。
### 7.2wordpress无法安装主题和插件
在安装Wordpress主题和插件时，提示无法建立目录wp-content/uploads/年/月份。没有上级目录的写权限，出现这个问题时当前启动Wordpress服务的用户没有在wpblog目录中的写权限，执行命令 `\# chown -R php-fpm:php-fpm wpblog` 。（如果不确定用户及用户组，可备份uploads目录，并付权限777，执行命令 `\# chmod 777 uploads`，安装主题后，查看文件所属用户即可）。
### 7.3出现 413 Request Entity Too Large 的问题
出现该问题，主要检查 /etc/php5/fpm/php.ini 文件中的参数，在做相应调整后，重启服务。
upload_max_filesize = 20M
post_max_size = 20M
重启fpm服务 `\# service php5-fpm restart`
### 7.4不能写入wp-config.php文件
在wordpress的根目录创建wp-config.php，并把页面中的内容粘贴到文件中，并增加 ?> 结尾。
## 8.参考资料
>安装nginx、php、mysql，请参考  https://ninghao.net/blog/1368
>安装Mysql，请骤参考  https://yq.aliyun.com/articles/285398
>无法访问nginx欢迎界面，请参考  http://www.cnblogs.com/themeth/p/10074593.html
>解决413 Request Entity Too Large错误，请参考https://blog.csdn.net/urbanvice/article/details/79111827
>安装wordpress主题时，提示需要FTP用户名密码的问题，请参考 https://www.cnblogs.com/ryanzheng/p/8372426.html
>不能写入wp-config.php文件问题解决，请参考https://blog.csdn.net/lindexi_gd/article/details/79773168
>安装FTP，请参考 https://www.cnblogs.com/tonyibm/p/7497978.html

知一写于2018年12月28日