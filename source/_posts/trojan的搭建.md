---
title: Trojan的搭建
date: 2021-02-02 13:53
categories: fq
number: 1
---

### Trojan的搭建

系统版本: CentOS 7 x64 (**注意：不能使用CentOS 7 x64 bbr 版本的系统，会导致bbr plus内核无法正常安装**)

#### 1. 安装bbr plus加速

```sh
wget --no-check-certificate https://raw.githubusercontent.com/cx9208/Linux-NetSpeed/master/tcp.sh && chmod +x tcp.sh && ./tcp.sh
```

（Onedrive有本脚本的备份）

在脚本中按要求安装bbr plus加速内核和模块即可。

#### 2. 安装Trojan

```sh
curl -O https://raw.githubusercontent.com/atrandys/trojan/master/trojan_mult.sh && chmod +x trojan_mult.sh && ./trojan_mult.sh
```

运行脚本，按要求输入已经做好dns解析的域名。

#### 3. 配置Trojan

截至上一步，我们的Trojan其实已经开始工作了，但是通过配置Trojan,我们可以自定义Trojan监听的端口，密码等，以便不与其他服务冲突。

Trojan的配置文件位于`/usr/src/trojan/server.conf`

修改`server.conf`

```sh
{
    "run_type": "server",
    "local_addr": "0.0.0.0",
    "local_port": 50056, #端口号
    "remote_addr": "127.0.0.1",
    "remote_port": 80,
    "password": [
        "grh123456" #密码
    ],
    "log_level": 1,
    "ssl": {
        "cert": "/usr/src/trojan-cert/new.gurh16.top/fullchain.cer",
        "key": "/usr/src/trojan-cert/new.gurh16.top/private.key",
        "key_password": "",
        "cipher_tls13":"TLS_AES_128_GCM_SHA256:TLS_CHACHA20_POLY1305_SHA256:TLS_AES_256_GCM_SHA384",
        "prefer_server_cipher": true,
        "alpn": [
            "http/1.1"
        ],
        "reuse_session": true,
        "session_ticket": false,
        "session_timeout": 600,
        "plain_http_response": "",
        "curves": "",
        "dhparam": ""
    },
    "tcp": {
        "no_delay": true,
        "keep_alive": true,
        "fast_open": false,
        "fast_open_qlen": 20
    },
    "mysql": {
        "enabled": false,
        "server_addr": "127.0.0.1",
        "server_port": 3306,
        "database": "trojan",
        "username": "trojan",
        "password": ""
    }
}

```

一般只需要修改端口号和密码。端口号建议避开443，避免和nginx冲突。

#### 4. 启动Trojan

```sh
/usr/src/trojan/trojan -c /usr/src/trojan/server.conf
```

