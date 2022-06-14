---
title: 备份整个Linux系统的方法
date: 2021-01-09 14:26
tags: [linux,backups]
number: 1
---

本md记录了如何备份一个Linux系统并将其还原至新机器。

即：将/ 目录下所有内容全部打包为tar,并在新机器中解包。

#### 1.备份

本a)可以直接通过tar对整个文件系统（'/‘）进行备份，但是有几点需要注意：

i. 不能备份以下几个文件（目录）

\1. 当前压缩文件

\2. /proc文件夹

\3. /lost+found文件夹

\4. /mnt文件夹

\5. /sys文件夹

\6. /media文件夹

b)所以，命令为：

```shell
tar cvpzf backup.tar.gz --exclude=/proc --exclude=/lost+found --exclude=/backup.tar.gz --exclude=/mnt --exclude=/sys --exclude=/media /

```

#### 2.还原

a) Linux可以再正在远行的系统中还原系统，如果当前启动无法启动，可以通过live cd来启动并执行恢复操作

b) 操作如下

```shell
tar xcpfz backup.tar.gz -C /
```

c) 需要额外创建目录

```shell
mkdir proc

mkdir lost+found

mkdir mnt

mkdir sys


```

