---
title: v2ray/v2fly的搭建
date: 2021-01-17 19:28
tags: [fq,linux]
categories: fq
number: 1
---

## v2ray/v2fly的搭建

本md记录了如何在一个vps上搭建v2ray (v2fly是新版本的v2ray)

#### 1. 安装

1. 同步时间

```sh
date -R
timedatectl set-local-rtc 1
timedatectl set-timezone Asia/Shanghai
```

2. 安装源码

```sh
curl -O https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh
curl -O https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-dat-release.sh
```

3. 安装及更新V2ray

   `bash install-release.sh`

4. 安装geoip.dat和geosite.dat

   `bash install-dat-release.sh`

5. 安装依赖

   `yum update && yum install curl -y && yum install cron -y && yum install socat -y`

6. ##卸载v2ray

   `bash install-release.sh --remove`

#### 2. 配置

1. 配置文件位于/usr/local/etc/v2ray/config.json (需要自己创建)

配置文件：

```json
{
  "inbounds": [
    {
      "port": 50056, // 服务器端口
      "protocol": "vmess",    
      "settings": {
        "clients": [
          {
            "id": "UUID", // V2ray客户端UUID 
            "alterId": 64
          }
        ]
      },
      "streamSettings": {
        "network": "ws", // TCP或WS
        "security": "tls", // security 要设置为 tls 才会启用 TLS
        "tlsSettings": {
          "certificates": [
            {
              "certificateFile": "/etc/v2ray/v2ray.crt", // 证书文件路径
              "keyFile": "/etc/v2ray/v2ray.key" // 密钥文件路径
            }
          ]
        }
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "freedom",
      "settings": {}
    }
  ]
}
```

需要更改的配置项有：端口、uuid、证书及密钥地址（经测试：证书和密钥可直接使用nginx网站的证书）

2. 常用命令

   ```sh
   systemctl restart v2ray
   systemctl status v2ray
   systemctl enable v2ray #开机自启动
   ```

   也可直接使用 `/usr/local/bin v2ray -config /usr/local/etc/v2ray/config.json`命令直接启动 （v2ray的程序安装在/usr/local/bin/v2ray, 配置文件在/usr/local/etc/v2ray/config.json）

#### 3. 使用BBR plus 加速

安装四合一脚本

```sh
wget https://github.com/chiakge/Linux-NetSpeed/raw/master/tcp.sh #下载脚本

chmod +x tcp.sh #更改权限

./tcp.sh #运行脚本
```

在脚本中，先选择安装bbr plus内核，重启后再安装加速模块。