---
layout: post
title: Docker入门教程6——Docker Engine
categories: [docker, devops]
description:
keywords:
mermaid: false
sequence: false
flow: false
mathjax: false
mindmap: false
mindmap2: false
---

# Docker desktop和Docker Engine的区别
Docker Desktop：Docker Desktop是一个全面的桌面应用程序，为开发人员提供了在本地计算机上使用Docker的一体化解决方案。它包含了Docker引擎、Docker CLI、Docker Compose、Docker Swarm等工具和组件，并提供了图形用户界面（GUI）以及与操作系统集成的功能。Docker Desktop适用于Windows和Mac操作系统，可以在本地轻松地构建、运行和管理Docker容器，并提供了一些附加功能，如文件共享、资源配置、网络设置等。

Docker Engine：Docker Engine是Docker的核心组件，它是一个开源的容器运行时环境，负责管理和运行容器。Docker Engine包括了Docker守护程序（Docker daemon）和Docker客户端（Docker client）。Docker守护程序负责管理镜像、容器、网络和存储等资源，而Docker客户端则是与守护程序进行交互的命令行工具或API。

总结来说，Docker Desktop是一个面向开发人员的桌面应用程序，提供了一个集成的Docker环境，包括Docker Engine和其他相关工具，用于在本地开发和管理容器。而Docker Engine是Docker的核心组件，是一个容器运行时环境，负责管理和运行容器。


# Docker Engine
Docker Engine是一个客户端-服务器应用程序，包括以下组件：

1. 一个长时间运行的守护进程（daemon）dockerd，充当服务器端。
1. API定义了程序可以使用的接口，用于与Docker守护进程进行通信和指令。
1. 命令行界面（CLI）客户端docker，用于通过脚本或直接的命令行指令控制或与Docker守护进程交互。


CLI客户端使用Docker API通过脚本或直接的命令行指令来控制或与Docker守护进程交互。许多其他Docker应用程序使用底层的API和CLI。守护进程创建和管理Docker对象，如镜像、容器、网络和卷等。

简而言之，Docker Engine是一个客户端-服务器应用程序，包括守护进程、API和CLI。守护进程创建和管理Docker对象，API定义了与守护进程通信的接口，而CLI则用于控制和与守护进程交互。


# 安装Docker Engine ([Ubuntu](https://docs.docker.com/engine/install/ubuntu/))

## APT方式

### 卸载非官方的APT包
- docker.io
- docker-compose
- docker-doc
-podman-docker

```
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

### 设置APT仓库

允许HTTPS
```
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
```

添加官方GPG key
```
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

添加docker仓库源
```
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

确认
```
cat /etc/apt/sources.list.d/docker.list
deb [arch=arm64 signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu   focal stable
```

推荐切换到aliyun源，安装速度较快
```
cat /etc/apt/sources.list.d/docker.list
#deb [arch=arm64 signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu   focal stable
deb [arch=arm64 signed-by=/etc/apt/keyrings/docker.gpg] http://mirrors.aliyun.com/docker-ce/linux/ubuntu    focal stable
```


### 安装

更新源
```
sudo apt-get update
```

安装Docker Engine, containerd和docker compose等
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

验证
```
sudo docker run hello-world
```

### 卸载

```
sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-ce-rootless-extras
```

```
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```


## 或者[从deb package安装](https://docs.docker.com/engine/install/ubuntu/)

[建议从aliyun下载deb包](https://mirrors.aliyun.com/docker-ce/linux/ubuntu/dists/focal/pool/stable/arm64/)


## 安装后配置

### 不使用`sudo`操作docker

```
sudo groupadd docker

sudo usermod -aG docker $USER

newgrp docker

docker run hello-world
```
