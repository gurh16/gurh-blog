---
title: 使用PlatformIO配置开发ESP8266
date: 2021-10-24 0:22
tags: [ESP8266,PlatformIO]
categories: ESP8266
number: 1
---



### 使用PlatformIO配置开发ESP8266

------

[TOC]

系统版本：Windows11 家庭中文版

VS Code 主题： Monokai Pro/Classic

Prerequisite：Arduino IDE， Python3.8

​	眼球无法忍受Arduino IDE 的丑陋主题，遂使用VS Code + PlatformIO 插件进行开发。PlatformIO是一个专门用于开发嵌入式系统的VS Code插件，笔者只用了一次就深深的爱上了这个优秀便利的开发环境。但是在配置PlatformIO过程中却遇到了很多问题，耗费了大量时间才得以解决。下面记录本次完整的安装过程。

#### PlatformIO相关网址

​	官网：[A professional collaborative platform for embedded development · PlatformIO](https://platformio.org/)

​	PlatformIO core 安装脚本： [Installation — PlatformIO latest documentation](https://docs.platformio.org/en/latest/core/installation.html#installation-methods)

#### 1. 下载PlatformIO IDE 插件

​	在VS Code 插件市场中搜索PlatformIO IDE 安装，在右下角提示安装内核时最小化VS Code， 使用PlatformIO core 安装脚本 get-platformio-core.py 进行安装， 语法为：`python.exe get-platformio.py`. 安装完成后重启VS Code。

#### 2. 配置PlatformIO

​	在首选项中搜索PlatformIO， 禁用`builtin python3`。在首选项中搜索Ardunio 并输入Ardunio Path。（填写文件夹路径即可）

#### 3. 创建PlatformIO项目

​	点击左侧按钮栏新出现的外星人图标，点击`New Project`。输入项目名称并选择开发板NodeMCU1.0 (12E). 第一次加载会联网下载所需库文件，时间会非常之长，**但请务必不要挂代理！！！** （开发者已经创建了中国CDN，挂代理反而会下载不了）。

#### 4. platformio.ini

​	这个文件是项目的配置文件，具体配置可以查阅 [官方doc](https://docs.platformio.org/en/latest/projectconf/index.html)。

#### 5. 基本操作和主要文件

​	程序源代码位于`/src/main.cpp`中， 可以在与`/src`同级目录下创建`/data`文件夹，用于存放准备上传到闪存中的文件。

​	左下角的`->`为编译上传按钮，`插头`按钮为串口监视器，默认波特率9600。

​	上传文件请使用`Upload Filesystem Image`功能， 位于`外星人图标 ->PROJECT TASKS ->``Upload Filesystem Image`