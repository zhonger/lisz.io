---
title: 解决VPS升级/安装WordPress主题及插件需要输入FTP账户和密码的问题
date: 2015-08-08 14:24:10
tags: 
- vps 
- ftp 
- wordpress主题安装
categories: tech
---

今天正式将原来博客网站转移至VPS中，原博客域名 `www.wl27.cn` 正式改为 `blog.wl27.cn` 。在VPS中搭建Wordpress博客，和使用主机空间搭建稍微有些不同。我使用的这台VPS是`Ubuntu 14.04 LTS`版本系统，采用LNMP一键架设整个服务坏境。在和使用主机空间搭建一样完成之后，由于Linux安全权限原因，我在网站后台升级、安全主题或者插件的时候，会出现提示需要我提供FTP信息的界面。有这样的字样提示”要执行请求的操作，WordPress需要访问您网页服务器的权限。请输入您的FTP登陆凭据以继续。如果您忘记了您的登陆凭据(如用户名、密码)，请联系您的网站托管商”。
解决这样一个问题，其实只需要我们可以给自己的WP网站授权就可以了。
```bash
chown -R www /home/wwwroot/blog.wl27.cn(修改成网站域名目录)
```
