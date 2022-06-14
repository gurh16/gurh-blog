---
title: 用Hexo搭建个人博客
date: 2020-12-29 19:43
tags: [linux,Hexo]
categories: hexo
number: 1
---



### 用Hexo搭建个人博客

------

[TOC]

系统版本：CentOS 7 （CentOS Linux release 7.8.2003 (Core)）

#### 安装Hexo

##### 一、必备环境搭建及Hexo安装

1. 安装node.js和git

   ```sh
   yum -y install git
   yum -y install nodejs
   ```

   

2. 查看node和npm版本

   `node -v`

   `npm -v`

   如果npm不是最新版本，请更新，否则hexo安装时会报错。

   ![img](https://img2020.cnblogs.com/blog/1065623/202007/1065623-20200708165344800-931380504.png)

3. 更新npm

   ```sh
   npm uninstall npm -g #卸载旧版本npm
   mkdir npm #创建存放npm的目录
   cd npm
   wget https://npm.taobao.org/mirrors/node/v10.14.1/node-v10.14.1-linux-x64.tar.gz #下载最新版npm
   tar -xvf  node-v10.14.1-linux-x64.tar.gz #解压
   mv node-v10.14.1-linux-x64 node
   ```

   添加环境变量：

   ```sh
   vim /etc/profile
   -----------加入以下内容
   export NODE_HOME=/usr/local/node  
   export PATH=$NODE_HOME/bin:$PATH
   ```

   刷新 `source /etc/profile`

4. 安装hexo

   本文使用npm进行安装：

   `npm install -g hexo-cli`

   安装完成后，要配置相关环境变量：

   `echo 'PATH="$PATH:./node_modules/.bin"' >> ~/.profile`

   **至此，hexo就安装完成啦！XD**

##### 二、Hexo基本配置

我们需要对Hexo进行最基本的配置以方便以后的使用

1. 创建Hexo项目

   ```sh
   $ hexo init <folder>
   $ cd <folder>
   $ npm install
   ```

   创建完成后，我们可以看一下Hexo项目的文件目录结构：

   ```
   .
   ├── _config.yml
   ├── package.json
   ├── scaffolds
   ├── source
   |   ├── _drafts
   |   └── _posts
   └── themes
   ```

   各文件功能：

   ```
   _config.yml	hexo配置文件（基本上所有配置都围绕这个文件）
   scaffold 存放模板
   source 推文的源文件
   	_drafts 草稿源
   	_posts	post源
   themes	主题文件夹
   ```

2. 配置 _config.yml

   ![keys](https://i.loli.net/2020/12/30/5dG8EgB13ShsQNC.png)

   主要更改author、subtitle等项。

##### 三、Hexo的基本操作

1. 创建post

   `hexo new a`  (a为推文的名称)

   本操作会让hexo在source/_posts下创建a.md文件。（post将直接发布在网站上）

2. 创建draft

   `hexo new draft b `  (b为draft的内容)

   本操作会创建一个draft，即在source/_drafts下创建b.md（draft不会显示在网站上） 

3. 发布

   `hexo publish`

   本操作会发布所有的draft，即将source/_drafts下的.md文件转移至source/_posts。

4. 生成静态网页

   `hexo generate` | `hexo generate --watch`

   本操作会将所有posts生成为html文件，保存在./public中。

5. 清除缓存

   有时（更换主题后）需要清空所有public中的内容，此时需要使用`hexo clean`

   **清空后要重新generate以生成最新的静态页面。**





##### 四、将public目录部署nginx

具体参考：[如何部署nginx](https://blog.gurh16.top/2020/12/29/%E9%83%A8%E7%BD%B2nginx%E5%8F%8A%E9%85%8D%E7%BD%AEssl%E8%AF%81%E4%B9%A6/)  

至此，我们的博客就搭建完成啦！XD

------

参考链接：

[Documentation | Hexo](https://hexo.io/docs/)

[centos安装pm2出现问题 哈利路亚啊啊啊 - 博客园 (cnblogs.com)](https://www.cnblogs.com/hallejuayahaha/p/13267892.html)

