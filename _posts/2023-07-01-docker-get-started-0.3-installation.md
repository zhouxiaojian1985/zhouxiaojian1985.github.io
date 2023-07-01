---
layout: post
title: Docker入门教程0.2——安装
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

# 安装 Docker

在开始使用 Docker 之前，您需要安装 Docker 引擎（Docker Engine）。Docker 引擎是运行 Docker 的核心组件，它负责构建、运行和管理容器。

Docker 在多个平台上都提供了安装程序和安装脚本。您可以根据您的操作系统选择相应的安装方法。下面是一些常见的操作系统和安装方式：

## [macOS](https://docs.docker.com/desktop/install/mac-install/):
在 macOS 上，您可以使用 Docker Desktop 进行安装。Docker Desktop 提供了一个集成的环境，包括 Docker 引擎、Docker CLI 和其他相关工具。您可以从 Docker 官方网站下载 Docker Desktop 安装程序，并按照说明进行安装。

## [Windows](https://docs.docker.com/desktop/install/windows-install/):
在 Windows 上，您可以使用 Docker Desktop 进行安装。Docker Desktop 提供了一个集成的环境，包括 Docker 引擎、Docker CLI 和其他相关工具。您可以从 Docker 官方网站下载 Docker Desktop 安装程序，并按照说明进行安装。请注意，Docker Desktop 需要在 Windows 10 专业版、企业版或教育版上安装。

## [Linux](https://docs.docker.com/desktop/install/linux-install/):
在 Linux 上，您可以使用 Docker 安装脚本进行安装。Docker 安装脚本会自动检测您的 Linux 发行版，并为您下载和安装适合的 Docker 版本。您可以在 Docker 官方网站上找到安装脚本和相应的说明。

安装 Docker 后，您可以使用 `docker version` 命令来验证 Docker 是否成功安装，并查看安装的版本信息。

```
Client:
 Cloud integration: v1.0.35
 Version:           24.0.2
 API version:       1.43
 Go version:        go1.20.4
 Git commit:        cb74dfc
 Built:             Thu May 25 21:51:16 2023
 OS/Arch:           darwin/arm64
 Context:           desktop-linux

Server: Docker Desktop 4.21.0 (113844)
 Engine:
  Version:          24.0.2
  API version:      1.43 (minimum version 1.12)
  Go version:       go1.20.4
  Git commit:       659604f
  Built:            Thu May 25 21:50:59 2023
  OS/Arch:          linux/arm64
  Experimental:     false
 containerd:
  Version:          1.6.21
  GitCommit:        3dce8eb055cbb6872793272b4f20ed16117344f8
 runc:
  Version:          1.1.7
  GitCommit:        v1.1.7-0-g860f061
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
```


# 开始使用Docker

安装 Docker 完成后，您可以开始使用 Docker 来构建、运行和管理容器了。以下是一些常见的 Docker 命令：

- `docker run`: 用于基于镜像启动一个容器。
- `docker build`: 用于根据 Dockerfile 构建一个镜像。
- `docker pull`: 用于从 Docker 仓库拉取一个镜像。
- `docker push`: 用于将一个镜像推送到 Docker 仓库。
- `docker images`: 用于列出本地已经下载的镜像。
- `docker ps`: 用于列出正在运行的容器。
- `docker stop`: 用于停止一个运行中的容器。
- `docker rm`: 用于删除一个停止的容器。

这只是 Docker 命令的一小部分，您可以通过 docker --help 命令或查阅 Docker 官方文档来了解更多命令和选项。

开始使用 Docker 后，您可以使用 Docker 镜像来构建和运行应用程序，通过容器实现应用程序的隔离和可移植性。您还可以通过 Docker Hub 或私有仓库来共享和获取
