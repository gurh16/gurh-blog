---
title: 本md记录了一次从零配置nginx服务并配置ssl证书的经历
date: 2020-12-29 12:18:42
tags: [linux,nginx]
number: 1
---



### **本md记录了一次从零配置nginx服务并配置ssl证书的经历**

------

[TOC]

系统版本：CentOS 7 （CentOS Linux release 7.8.2003 (Core)）

##### 一、安装nginx

```sh
yum -y install nginx
```

安装成功后别忘了开启服务：

```shell
sudo systemctl start nginx.service
sudo systemctl enable nginx.service
```

##### 二、配置nginx

首先，我们需要确定我们网站的根目录，如：/home/wwwroot/www.gurh16.top 。

之后，找到并修改/etc/nginx/nginx.conf 。

可能用到的文件搜索命令：

```shell
sudo find -name nginx
```

在nginx.conf中，"#"代表注释，最重要的是server{}块这部分。每个server{}就代表每一个web站点；listen后为监听端口，一般http为80，https为443；server_name为域名；location后为网站根目录的绝对路径。

![img](https://images2015.cnblogs.com/blog/172889/201704/172889-20170418173628696-1685332558.png)

```shell
listen 80;代表监听80端口
server_name xxx.com;代表外网访问的域名
location / {};代表一个过滤器，/匹配所有请求，我们还可以根据自己的情况定义不同的过滤，比如对静态文件js、css、image制定专属过滤
root html;代表站点根目录
index index.html;代表默认主页
```

保存，至此我们就完成了最基本的nginx配置！

记得刷新！！！

 `nginx -s reload`

Now, 不妨试试用域名访问一下自己的网站吧！XD



##### 三、获取并配置SSL证书

证书可通过腾讯云获取，第一年免费使用。

获取证书后，我们会得到以下两个文件，一个为证书文件，另一个为key。![企业微信截图_16091720908073.png](https://i.loli.net/2020/12/30/wDvfgx6nH7haYod.png)

将两个证书上传至服务器(推荐目录：/etc/ssl  本文中使用的目录：/home/wwwroot/www.gurh16.top/ssl)

修改nginx.conf文件：（监听443端口）

```sh
http{
    #http节点中可以添加多个server节点
    server{
        #监听443端口
        listen 443 ssl;
        #对应的域名，把baofeidyz.com改成你们自己的域名就可以了
        server_name baofeidyz.com;
        #从腾讯云获取到的第一个文件的全路径
        ssl_certificate /etc/ssl/1_baofeidyz.com_bundle.crt;
        #从腾讯云获取到的第二个文件的全路径
        ssl_certificate_key /etc/ssl/2_baofeidyz.com.key;
        ssl_session_timeout 5m;
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
        ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:HIGH:!aNULL:!MD5:!RC4:!DHE;
        ssl_prefer_server_ciphers on;
        #这是我的主页访问地址，因为使用的是静态的html网页，所以直接使用location就可以完成了。
        location / {
                #文件夹
                root /home/wwwroot/www.gurh16.top;
                #主页文件
                index index.html;
        }
    }
    server{
        listen 80;
        server_name www.gurh16.top;
        rewrite ^/(.*)$ https://www.gurh16.top:443/$1 permanent;
    } #重定向链接
}
```

刷新！！！

`nginx -s reload`



大功告成！现在你的网站可以用https访问啦！

------

参考链接：

[Nginx Linux详细安装部署教程 - taiyonghai - 博客园 (cnblogs.com)](https://www.cnblogs.com/taiyonghai/p/6728707.html)

[Nginx配置SSL证书 - 别动我的猫 - 博客园 (cnblogs.com)](https://www.cnblogs.com/zeussbook/p/11231820.html)