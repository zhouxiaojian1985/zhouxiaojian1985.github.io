---
layout: post
title: Docker Hello World
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

要在 Docker 中运行 "Hello World"，您可以按照以下步骤进行操作：

安装 Docker: 首先，确保您已经安装了 Docker 引擎。您可以参考 Docker 官方文档中的安装指南，根据您的操作系统选择合适的安装方式。

拉取镜像: 打开终端或命令行界面，并运行以下命令来从 Docker Hub 上拉取 "Hello World" 镜像：

```
docker pull hello-world
```
这将从 Docker Hub 下载 "Hello World" 镜像到您的本地机器。

运行容器: 在终端或命令行界面中运行以下命令来创建并运行 "Hello World" 容器：

```
docker run hello-world
```
这将在 Docker 中创建一个新的容器，并运行 "Hello World" 镜像。容器将执行 "Hello World" 程序，并在终端或命令行界面中输出相应的信息。

如果一切顺利，您将看到类似以下的输出：

```
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (arm64v8)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```
这表示您已成功在 Docker 中运行了 "Hello World"。

通过上述步骤，您可以快速体验在 Docker 中运行简单的 "Hello World" 程序。这是一个入门级示例，帮助您熟悉 Docker 的基本使用方式。您可以进一步探索 Docker 的功能和用法，以构建和管理更复杂的容器化应用程序。
