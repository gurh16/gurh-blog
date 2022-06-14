---
title: 在Linux下搭建FTP服务
date: 2021-02-02 13:18
categories: linux
number: 1
---



### 在Linux下搭建FTP服务

FTP服务让文件从本地到服务器的传输变得方便，但几乎每次搭建ftp都会遇到一些问题。本md记录了如何在linux下搭建ftp服务。

系统环境： CentOS 7 x64

#### 1. 安装vsftpd

```sh
yum -y vsftpd
```

#### 2. 配置vsftpd

vsftpd相关配置文件的默认位置为 `/etc/vsftpd`

编辑 `vsftpd.conf`

只有两行必须要改动，**改为**如下所示（即保留listen=yes，注释掉ipv6）

```markdown
Listen=YES
#listen_ipv6=YES
```

在文件末尾插入

```
pasv_min_port=10060
pasv_max_port=10090
```

#### 3. 添加FTP账户

首先需要创建一个ftp文件夹，这里我们使用`/home/wwwroot`。

建议将文件夹权限设为www

```sh
chown -R www /home/wwwroot
chgrp -R www /home/wwwroot
```

执行如下语句添加用户并修改密码（username为用户名）:

```sh
sudo useradd -d /home/wwwroot -s /bin/bash username
sudo passwd username
```

最后 启动vsftpd服务

```sh
sudo service vsftpd start #启动vsftpd
sudo service vsftpd stop #停止vsftpd
sudo service vsftpd restart #重启vsftpd
```

记得查看端口状态:

```sh
netstat -nlpt #ftp服务对应的默认端口是21端口且进程名为vsftpd
```

