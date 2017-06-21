---
title: windows安装配置python 3.5.1+pip 8.1.0 +django 1.9.4
date: 2016-03-08 22:12:49
tags:
- windows
- pip
categories: tech
---
# 下载并安装python3.5.1
> python官网：https://www.python.org/downloads/

- 下载完毕后，点击`.exe`文件直接安装，安装选项可以选择配置`python`到系统变量、安装`pip`工具
- 在`cmd窗口`使用`python`命令检查`python`是否安装成功（成功的话会进入`python shell`，失败会返回没有这个命令）

# 更新pip至最新版本
- 在`cmd窗口`使用`pip list`命令检查pip是否安装成功（成功的话会显示当前`pip`的版本和`setuptool`的版本）
- 输入`python -m pip install -U pip`命令升级`pip`至最新版本
- 再输入`pip list`检查当前`pip`版本（当前`pip`的最新版本为`8.1.0`版本）

# 更换pip的镜像源为上海大学开源社区镜像源
- 由于pip的默认服务器在美国，日常使用`pip install`命令会出现超时，所以我们要把镜像源更换为`上海大学开源社区pip镜像源`
- 更换方法是，在当前windows用户的主目录，添加一个`pip`文件夹，在`pip`文件夹中新建一个`pip.ini`文件，并把以下内容写入文件：
```
[global]
index-url=https://pypi.shuosc.org/simple
[list]
format=columns
```

# 安装django1.9.4（当前最新版本）
新开一个cmd窗口，在窗口中输入`pip install django`命令来安装`django`最新版本