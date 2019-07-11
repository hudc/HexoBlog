---
title: 在阿里云ECS服务器上部署Hexo静态博客
date: 2019-04-03 18:11:17
updated: 2019-04-03 18:11:17
tags: 
- Hexo 
categories: 
- 技术 
permalink: install-hexo-on-aliyun-ecs
---

## 1 写在前面
之前在阿里云购买了ECS服务器，用来部署Wordpress博客环境，但采购的服务器配置低，安装全套的PHP、Nginx、Mysql后，运行和维护起来略显迟滞，遂想采用Hexo轻量级静态博客系统。以前也在GitHub上部署过Hexo，虽然轻量但也存在两个问题，1.是需要有本地环境，不利于多工作环境同步和备份；2.部署环境主要在GitHub（国内有coding），访问速度不占优势且不能在国内备案。所以计划在国内云服务器上部署Hexo，则这两个问题都将解决。
<!--more-->
## 2 达到效果
1. 使用国内云服务器和域名，并在通过备案。
2. 环境部署都在服务器端，不搭建本地环境。
3. 基础环境仅为CentOS，Nginx，NodeJS，Git，Hexo，需要资源少 。
4. 博客文章Markdown源文件保存在服务器端，易于备份和修改。 

## 3 安装部署
Hexo官网提供了非常详细的安装步骤和说明，在这里就不再详细描述，直接列出所需的关键步骤和命令，其他内容大家可参考[Hexo官网](https://hexo.io/zh-cn/)。

### 3.1 基础环境
阿里云ECS服务器，操作系统CentOS 7.6 64位。

### 3.2 安装Git
在这里Git主要用于Hexo的主程序和主题的安装，不是用于Hexo官网文档中“部署”的传输使用，如果熟悉Hexo环境也可以不安装，直接上传文件。
执行命令`#sudo yum install git-core`，安装结束后执行命令`#git --version`，如输出版本号则安装成功。

### 3.3 安装NodeJS
NodeJS是Hexo的基础环境，必须安装。
执行命令`#yum install -y nodejs`，安装结束后执行命令`#node -v`，如输出版本号则安装成功。

### 3.4 安装Hexo
按照官网命令安装，自动下载程序，需要一点时间。
执行命令`#npm install -g hexo-cli`，安装结束后执行命令`#hexo version`，如输出版本号则安装成功。

### 3.5 初始化 Hexo
在home目录下建了hexoblogdir目录，在hexoblog目录中执行命令`#hexo init aliyunbloger`（目录地址及名称可自定义），该命令自动创建以下文件` _config.yml  db.json  node_modules  package.json  scaffolds  source  themes`，文件说明可参考官网。

### 3.6 生成静态文件和启动服务
生成初始的Hexo页面，并启动服务。
执行命令`#hexo g`和`#hexo s`，如果在控制台提示Hexo is running，即表示服务已启动成功，但是这个时候还不能访问，因为阿里云ECS默认不开通4000端口。需要注意的是，以后Hexo服务是通过Nginx部署，所以不需要再执行`#hexo s`命令。

### 3.7 增加安全组规则4000端口
依次按照以下路径找到配置页，或者通过帮助找到配置页面，ECS云服务器控制台->实例->管理->本实例安全组->配置规则->入方向->添加安全组规则，端口范围4000/4000，授权对象0.0.0.0。

### 3.8 访问4000端口
在本地浏览器中，访问http://youripaddress:4000/ ，如果显示Hexo的Hello World页面，则表示部署成功。

### 3.9 安装 Nginx程序
虽然Hexo自带发布服务，但是功能比较弱，Nginx是比较方便的服务程序。
执行命令`#yum install nginx -y`，安装结束后执行命令`#nginx -v`，如输出版本号则安装成功。

### 3.10 启动Nginx服务
执行命令`#systemctl start nginx.service`，在浏览器中输入 http://youripaddress/ ，如果显示Welcome to nginx，则表示Nginx安装成功。配置Nginx服务默认开机启动服务，执行命令`#systemctl enable nginx` 。

###  3.11修改nginx.conf配置
修改配置文件 /etc/nginx/nginx.conf ，如果此时已经完成域名绑定，可直接配置域名，否则配置IP地址。找到以下内容：server_name处配置域名或IP，root处配置hexo的public目录，public目录在执行命令`#hexo g`时自动生成，如/home/hexoblogdir/aliyunbloger/public 。
```
server {
      listen       80;
      server_name  #配置域名 yourbloger.com
      root         #配置对应hexo的public目录
}
```

### 3.12 重启Nginx服务
修改 Nginx配置文件后，需要重新启动Nginx服务。
执行命令`#nginx -s reload` 。

### 3.13 访问Hexo服务
在浏览器中访问域名或者IP地址，在地址中不写4000端口，默认使用的是80端口，如果再次显示Hexo的Hello World页面，则通过Nginx部署Hexo的工作就完成了。

### 3.14 配置Hexo主题
现在比较流行的是Hexo主题是Next，进入到 /home/hexoblogdir/aliyunbloger/ 目录，执行命令`#git clone https://github.com/iissnan/hexo-theme-next themes/next`，下载完成后，修改_config.yml配置文件，找到 theme 行，将冒号后修改成next（注意冒号后面有空格，如 theme: next ）。 执行命令`#hexo clean`和`#hexo g` ，再次访问网站，则主题变为黑白的next主题。

## 4 写在最后
如果每一个步骤都按照本文档执行，并且没有报错，则基于阿里云ECS服务器部署Hexo的工作就完成了，该步骤也适用于其他VPS服务器，可能只是在网络端口规则配置上会有些差别，如有疑问可互相交流，联系方式见网站[关于页面](http://amdoing.com/about/)。

>参考资料：
Hexo官网文档：<https://hexo.io/zh-cn/docs/> 
在ECS上部署Hexo：<https://blog.csdn.net/tian330726/article/details/80791388> 
Hexo建站过程：<https://qiming.info/阿里云CentOS下Hexo+Nginx建站过程> 
主题Next配置：<http://theme-next.iissnan.com/>
主题Next个性优化：<https://www.jianshu.com/p/efbeddc5eb19>
GitHub官网Markdown的语法：<https://guides.github.com/features/mastering-markdown/#syntax> 
