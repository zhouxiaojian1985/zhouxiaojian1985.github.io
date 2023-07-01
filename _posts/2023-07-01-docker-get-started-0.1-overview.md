---
layout: post
title: Docker入门教程0.1——概述
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

# Docker概述
Docker是一个开源平台，通过容器化技术可以自动化部署、扩展和管理应用程序。它提供了一个环境，可以将应用程序及其依赖关系打包成一个标准化的单元，称为容器。容器是轻量且隔离的，使应用程序能够在不同的环境中一致运行。

以下是与Docker相关的关键概念：

- Images：Docker镜像是用于创建容器的只读模板。它们包含运行应用程序所需的文件、库和配置。

- Containers：容器是从Docker镜像创建的实例。它们是运行应用程序及其依赖关系的隔离环境。容器提供了在不同环境中一致且可重现的执行环境。

- Dockerfile：Dockerfile是一个文本文件，包含构建Docker镜像的指令。它指定基础镜像、添加依赖项、复制文件和配置容器等操作。

- Registry：Docker注册表是用于存储Docker镜像的集中式仓库。默认的公共注册表是Docker Hub，但您也可以设置私有注册表来存储和共享自己的镜像。

- Docker Compose：Docker Compose是一种定义和运行多容器Docker应用程序的工具。它允许您在单个YAML文件中指定多个容器、网络和依赖关系的配置。

- Docker Swarm：Docker Swarm是Docker的原生集群和编排解决方案。它可以创建和管理一组Docker节点，允许您在多台机器上部署和扩展应用程序。

要使用Docker，您需要在计算机上安装Docker引擎。Docker引擎负责构建和运行容器。安装完成后，您可以使用docker命令行界面（CLI）与Docker进行交互。

例如，您可以使用docker build命令构建镜像，使用docker run命令运行容器，并使用各种docker子命令管理容器、镜像和其他Docker资源。

Docker已成为软件开发和部署流程中的常用工具，因为它简化了应用程序的打包过程，并确保在不同环境中的一致性。它使开发人员能够将应用程序及其依赖项一起发布，从而更轻松地部署和管理软件在各种计算环境中运行。
