---
layout: post
title: Docker入门教程1.1——镜像加速
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

# Docker Desktop镜像加速
使用 Docker Desktop 时可以配置国内镜像加速器来加快 Docker 镜像的下载速度。以下是在 Docker Desktop 中配置国内镜像加速器的步骤：

打开 Docker Desktop 设置: 打开 Docker Desktop 应用程序，并从任务栏或系统托盘中找到 Docker 图标。右键单击图标，然后选择 "Settings"（设置）。

选择 Docker 镜像加速器选项: 在 Docker Desktop 设置中，导航到 "Resources"（资源）选项卡，然后选择 "Docker Engine"（Docker 引擎）部分。

配置国内镜像加速器: 在 "Docker Engine" 部分的配置文件框中，添加以下内容：

```
"registry-mirrors": [
  "https://dockerhub.azk8s.cn",
  "https://hub-mirror.c.163.com",
  "https://mirror.baidubce.com"
]
```
上述示例中，我们添加了三个常用的国内镜像加速器地址：Azure China（中国 Azure）、网易云、百度云。您也可以根据自己的需求选择其他可用的镜像加速器地址。

保存并应用配置: 单击 "Apply & Restart"（应用并重启）按钮，以保存并应用配置更改。

Docker Desktop 将重新启动 Docker 引擎，并使用配置的国内镜像加速器来加速 Docker 镜像的下载。

通过配置国内镜像加速器，您可以在中国境内更快地下载 Docker 镜像，并提高 Docker Desktop 的使用效率。请注意，镜像加速器的地址可能因时间而有所变化，建议根据最新的信息进行配置。

# Docker Engine镜像加速

编辑 Docker 配置文件: 打开 Docker 的配置文件，通常位于 /etc/docker/daemon.json（Linux）或 %USERPROFILE%/.docker/daemon.json（Windows）。

如果文件不存在，可以创建一个新的配置文件。

配置镜像加速器地址: 在配置文件中，添加以下内容：

```
"registry-mirrors": [
  "https://dockerhub.azk8s.cn",
  "https://hub-mirror.c.163.com",
  "https://mirror.baidubce.com"
]
```

保存并退出配置文件: 保存对配置文件的修改，并关闭文件编辑器。

重启 Docker 服务: 在终端或命令行界面中，执行以下命令以重启 Docker 服务：

Linux：

```
sudo systemctl restart docker
```

Windows（使用管理员权限的 PowerShell）：
```
Restart-Service docker
```

验证镜像加速器: 运行以下命令来验证 Docker 是否正在使用配置的镜像加速器：
```
docker info
```

```
...
Registry Mirrors:
  https://dockerhub.azk8s.cn/
  https://hub-mirror.c.163.com/
  https://mirror.baidubce.com/
```
在输出信息中，查找 "Registry Mirrors" 部分，并确认镜像加速器地址是否正确显示。

通过配置镜像加速器，Docker 将使用指定的镜像加速器来加速拉取镜像的过程。这将显著提高 Docker 镜像的下载速度，尤其对于那些网络限制或延迟较高的情况下。
