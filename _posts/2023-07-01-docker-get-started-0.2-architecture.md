---
layout: post
title: Docker入门教程0.2——架构
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

# Docker架构

Docker采用了客户端-服务器架构。Docker客户端与Docker守护进程进行通信，而守护进程负责构建、运行和分发Docker容器。Docker客户端和守护进程可以运行在同一系统上，也可以将Docker客户端连接到远程的Docker守护进程。Docker客户端和守护进程之间通过REST API进行通信，可以通过UNIX套接字或网络接口进行通信。另一个Docker客户端是Docker Compose，它允许您处理由一组容器组成的应用程序

![docker arch](/images/posts/docker/architecture.svg)

在典型的Docker架构中，包括以下组件：

- Docker客户端（Docker Client）：Docker客户端是与用户交互的命令行界面或图形界面工具。它允许用户通过发送命令与Docker进行交互，例如构建镜像、运行容器、管理容器等。

- Docker守护进程（Docker Daemon）：Docker守护进程是Docker的核心组件，负责管理Docker容器和镜像。守护进程监听来自客户端的命令，并执行相应的操作，如构建镜像、创建容器、分发镜像等。守护进程还负责管理容器的生命周期、网络和存储等方面。

- Docker镜像（Docker Images）：Docker镜像是应用程序及其依赖关系的静态表示。镜像可以视为只读模板，其中包含了运行应用程序所需的一切，包括操作系统、库、代码和配置文件。镜像是容器的基础，可以通过构建、拉取或导出创建。

- Docker容器（Docker Containers）：Docker容器是基于Docker镜像创建的运行实例。容器提供了一个独立的运行环境，其中包含了运行应用程序所需的所有文件和设置。容器可以被启动、停止、暂停和删除，使应用程序能够在隔离的环境中运行。

- Docker注册表（Docker Registry）：Docker注册表用于存储和共享Docker镜像。Docker Hub是官方的公共注册表，其中包含了大量的官方和社区贡献的镜像。您还可以搭建私有的注册表，用于存储和分享自己的镜像。

- Docker网络（Docker Networking）：Docker提供了网络功能，使容器之间可以相互通信和访问外部网络。它支持多种网络驱动程序，包括桥接网络、主机网络、覆盖网络等。网络功能可以通过创建网络、连接容器到网络、指定网络别名等来配置。

- Docker存储（Docker Storage）：Docker提供了存储功能，用于持久化容器的数据和配置。它支持多种存储驱动程序，包括本地卷、共享卷、网络存储等。存储功能可以通过挂载卷、创建数据卷容器等方式进行配置。

总体而言，Docker的架构允许用户通过客户端与守护进程进行交互，构建、运行和管理容器。镜像和注册表用于存储和共享容器的静态表示。网络和存储功能使容器能够与其他容器和外部环境进行通信和数据交换。这种架构的灵活性和可扩展性使得Docker成为一个强大而流行的容器化平台。
