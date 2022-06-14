---
title: 在Windows10下利用wsl2运行Ubuntu的解决方案
date: 2021-05-10 22:40
tags: [win10,linux]
categories: linux
number: 1
---

### 在Windows10下利用WSL2运行Ubuntu的解决方案

------

WSL2是微软自带的一款超优秀的linux虚拟机，借助WSL2，可以在Win10中创建一个linux发行版子系统

#### 前置需求：

Win10最新版本

管理员模式下的PowerShell或命令提示符

#### 安装步骤：

1. 在PowerShell中运行以下命令以安装WSL2：

   ```powershell
   dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
   ```

   

2. 启用虚拟机平台

   ```powershell
   dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
   ```

   重启计算机以完成安装

3. 安装Linux内核更新包(备份在OneDrive中)

[适用于x64的WSL2 Linux内核更新包](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

4. 将WSL2设置为默认版本

```powershell
wsl --set-default-version 2
```



5. 安装Linux发行版

   在Microsoft Store中搜索Ubuntu并安装

   ![企业微信截图_16206569018073.png](https://i.loli.net/2021/05/10/Njp53iK1tCfRqXM.png)

6. 启动软件，Ubuntu将自动安装

#### 使用：

在PowerShell或命令提示符中输入`wsl`以启动Ubuntu.