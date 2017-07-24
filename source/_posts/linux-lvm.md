---
title: 在linux系统上没有磁盘阵列实现合并磁盘
date: 2017-07-01 14:27:06
tags:
    - linux
    - lvm
    - 合并磁盘
---

# 基本概念

- `物理存储`:指的是物理的硬盘，在`/dev`目录下的`sda`、`sdb`等
- `物理卷`:指的是物理硬盘上的分区或逻辑上与磁盘分区具有相同功能的设备，是LVM的基本存储块，但和分区相比，却包含了与LVM管理相关的参数
- `卷组`:LVM的卷组类似于物理硬盘，卷组上边可以建立多个虚拟的分区，LVM卷组由一个或多个物理卷组成
- `逻辑卷`:LVM的逻辑卷类似于非LVM系统中的硬盘分区，在逻辑卷上边可以建立文件系统，用于mount到不同的挂载点，提升分区空间——`真正跟用户打交道的部分`
- `Physcial Extent`:每一个物理卷被划分为一个个的基本存储单元，每一个PE都具有唯一的编址（类似于物理磁盘上的磁盘地址），PE的大小默认为4MB
- `Logical Extent`:每一个逻辑卷也被划分为一个个的基本存储单元，每一个LE也具有唯一的编址，在同一个卷组中，LE和PE的大小是相等的

# 实验环境
- Ubuntu Server 16.04 LTS 
- 已安装好系统的1T硬盘
- 2块2T空硬盘

# 实验步骤(在root用户下操作)

## 第一步 分区
- 格式化`fdisk /dev/sda`
```
Command(m for help): n  (创建新分区)
```
- 接下来选择创建主分区、默认分区号为1，把所有空间全部分配给这个分区(默认即可)
- 使用`p`查看分区情况，使用`t`命令(`30`为`Linux LVM`)
```
Hex code (type L to list codes): 30
```
- 最后再用`w`命令保存分区表
- 另外一块也按照以上的步骤格式化为`LVM`格式

## 第二步 建立LVM分区和VG逻辑卷组
```
pvcreate /dev/sda1 /dev/sdb1
pvdisplay
vgextend asc-vg /dev/sda1 /dev/sdb1 (或者vgcreate extspace /dev/sda1 /dev/sdb1)
vgdisplay
```

## 第三步 创建逻辑卷
```
lvcreate --name data --size 3.6T asc-vg
lvdisplay
```

## 第四步 挂载逻辑卷
```
mkfs.ext4 /dev/asc-vg/data 
mount /dev/asc-vg/data /home/data
```

## 第五步 配置自动挂载
- 修改`/etc/fstab`，增加以下几行：
```
/dev/asc-vg/data /home/data ext4 rw,noatime 0 0
```
