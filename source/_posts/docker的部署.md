---
title: docker的部署
date: 2021-01-13 11:07
tags: [linux, docker]
number: 1
---

## Docker的部署

#### 1. 安装Docker

卸载旧版本docker

`sudo apt-get remove docker docker-engine docker.io`

安装所需依赖

`sudo apt-get install apt-transport-https ca-certificates curl gnupg2 software-properties-common`

信任docker的GPG公钥

`curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -`

添加软件仓库

```sh
sudo add-apt-repository \
   "deb [arch=amd64] https://mirrors.tuna.tsinghua.edu.cn/docker-ce/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```

安装docker

```shell
sudo apt-get update
sudo apt-get install docker-ce
```

#### 2. docker命令

```shell
#启动docker
sudo systemctl start docker

#停止docker
sudo systemctl stop docker

#重启docker
sudo systemctl restart docker

#登录dockerhub账号
sudo docker login
```

##### 镜像操作

符合命名规则的镜像由 用户名/库名:版本号 构成。(不写版本号默认为latest)

```sh
#列出镜像
sudo docker images

#从dockerhub拉取镜像
sudo docker pull <username>/<respo>:<tag>

#更改镜像tag
sudo docker tag iamge <username>/<respo>:<tag>

#上传镜像至dockerhub
sudo docker push <username>/<respo>:<tag>

#删除镜像
sudo docker rm image
```

##### 容器操作

**创建容器**

`sudo docker run [option] [镜像名] [向启动容器中传入的命令]`

常用可选参数：

```sh
-i # 表示以“交互模式”运行容器
-t # 表示容器启动后会进入其命令行。加入这两个参数后，容器创建就能登录进去。即 分配一个伪终端。
--name # 为创建的容器命名
-v # 表示目录映射关系(前者是宿主机目录，后者是映射到宿主机上的目录，即 宿主机目录:容器中目录)，可以使 用多个-v 做多个目录或文件映射。注意:最好做目录映射，在宿主机上做修改，然后 共享到容器上。
-d # 在run后面加上-d参数,则会创建一个守护式容器在后台运行(这样创建容器后不 会自动登录容器，如果只加-i -t 两个参数，创建后就会自动进去容器)。
-p # 表示端口映射，前者是宿主机端口，后者是容器内的映射端口。可以使用多个-p 做多个端口映射
-e # 为容器设置环境变量
--network=host # 表示将主机的网络环境映射到容器中，容器的网络与主机相同
```



**交互式容器**

创建一个交互式容器，并命名为 `myubuntu` ，使用如下命令:

`sudo docker run -it --name=myubuntu ubuntu /bin/bash`

在容器中可以随意执行linux命令，就是一个ubuntu的环境，当执行exit命令退出时，该容器也随之停止。

**守护式容器**

如果对于一个需要长期运行的容器来说，我们可以创建一个守护式容器。在容器内部exit退出时，容器也不会停止。

`sudo docker run -dit --name=myubuntu2 ubuntu`

**进入已运行的容器:**

```sh
sudo docker exec -it [容器名或容器id] [进入后执行的第一个命令]
```

停止与启动容器

```
# 停止一个已经在运行的容器
sudo docker container stop [容器名或容器id]

# 启动一个已经停止的容器
sudo docker container start [容器名或容器id]

# kill掉一个已经在运行的容器
sudo docker container kill [容器名或容器id]

# 删除容器
sudo docker container rm [容器名或容器id]
```

**将容器保存为镜像**

```sh
sudo docker commit [容器名] [镜像名]
```

**镜像备份与迁移**

```sh
# 打包
sudo docker save -o [保存的文件名] [镜像名]

# 如
sudo docker save -o ./ubuntu.tar ubuntu

# 加载
sudo docker load -i ./ubuntu.tar
```