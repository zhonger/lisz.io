---
title: ubuntu-14.04-lts安装配置nodejs+bower
date: 2015-12-23 16:16:16
tags:
- ubuntu
- nodejs
- bower
categories: tech
---
> 强烈推荐方案二

# 一、方案一
安装准备：`pyhton，make，gcc，g++`均已安装
- 第一步 将`nodejs的ppa源`加入系统    ```$ sudo  add-apt-repository ppa:chris-lea/node.js```
- 第二步 更新系统软件源缓存并安装`nodejs`  ```$sudo apt-get update  $ sudo apt-get install nodejs```
- 第三步 使用`npm`命令全局安装bower命令 ```$ sudo npm install bower -g```
到此`nodejs`和`bower`工具安装完成，接下来请享受`bower`工具带来的舒适吧！
注：$ 为`bash`命令行前标识符

# 二、方案二
由于国内直接访问软件源的网速不是很好，而且`apt源`的`nodejs`版本也不是很好，所以建议采用方案二——使用`NPM淘宝镜像`来实现
- 第一步  在`https://npm.taobao.org/mirrors/node`中找到你想要的`nodejs`版本，建议采用`v4.4.3LTS版本`或者`the latest版本`
参考命令为：```wget –no-check-certifica https://npm.taobao.org/mirrors/node/v4.4.3/node-v4.4.3-linux-x64.tar.gz```
（因为实验时主机为`Ubuntu 14.04 LTS 64位`操作系统，所以选择`node-v4.4.3-linux-x64.tar.gz`）
- 第二步 在用户根目录创建node文件夹，将下载的压缩包内容解压到该文件夹
参考命令为：```tar zxf node-v4.4.3-linux-x64.tar.gz ~/node/```
- 第三步  将node和npm命令加入用户环境变量
参考命令为： `vim .bashrc`
在`.bashrc`文件的末尾加入`PATH=$PATH:~/node/bin`
```source .bashrc```
（使该配置文件立即生效，如果不生效可以重新开个窗口试试`node -v` 是否会返回`v4.4.3`）
（这样的命令就是只能单用户使用，如果需要多用户使用，请将`node文件夹`设置在系统公用目录，然后将`bin`目录赋给权限`755`）
- 第四步  安装cnpm
参考命令为：```npm install -g cnpm --registry=https://registry.npm.taobao.org```
到此为止，`cnpm`命令就可以完全替代`npm`进行使用，并且安装模块的速度杠杠的哦（毕竟是淘宝镜像源啊～）
- 第五步  安装bower
参考命令：`cnpm install -g bower`
