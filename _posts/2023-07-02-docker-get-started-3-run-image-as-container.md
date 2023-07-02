---
layout: post
title: Docker入门教程3——将映像作为容器运行
categories: [docker, devops, python]
description:
keywords:
mermaid: false
sequence: false
flow: false
mathjax: false
mindmap: false
mindmap2: false
---

# 运行容器

因为5000端口可能再主机上已经被占用了，所以我们将主机的端口8000映射到容器的端口5000，
这样就可以通过访问主机的端口8000来访问运行在容器中的应用程序。
```
docker run --publish 8000:5000 python-docker
* Debug mode: off
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on all addresses (0.0.0.0)
 * Running on http://127.0.0.1:5000
 * Running on http://172.17.0.2:5000
Press CTRL+C to quit
```

使用`curl`验证输出
```
curl localhost:8000

Hello, Docker!
```

容器界面的输出
```
172.17.0.1 - - [02/Jul/2023 07:20:57] "GET / HTTP/1.1" 200 -
```


# 后台模式下运行

```
docker run -d -p 8000:5000 python-docker
69b8bc4f3da702c3af98209cb6db5488804caab0770c586748915ecb9ff590f8
```

使用`curl`验证输出
```
curl localhost:8000

Hello, Docker!
```

## 查看容器


要查看正在运行的容器列表，可以运行`docker ps`命令。
类似于在Linux机器上使用ps命令来查看进程列表。

```
docker ps
CONTAINER ID   IMAGE           COMMAND                   CREATED         STATUS         PORTS                    NAMES
69b8bc4f3da7   python-docker   "python3 -m flask ru…"   4 minutes ago   Up 4 minutes   0.0.0.0:8000->5000/tcp   competent_tu
```

`docker ps`命令提供了关于正在运行的容器的一些信息:
- 容器ID
- 镜像
- 启动命令
- 创建时间
- 状态
- 暴露的端口
- 名称

启动容器时如果没有提供容器的名称，Docker会生成一个随机的名称（这里是competent_tu）。
运行`docker stop`命令可以停止容器

```
docker stop competent_tu
competent_tu
```

再次运行`docker ps`命令，现在容器已经不在运行了
```
docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

## 为容器命名

在`docker run`命令中传递`--name`选项
```
docker run -d -p 8000:5000 --name rest-server python-docker

docker ps
CONTAINER ID   IMAGE           COMMAND                   CREATED        STATUS        PORTS                    NAMES
583b52000b1a   python-docker   "python3 -m flask ru…"   1 second ago   Up 1 second   0.0.0.0:8000->5000/tcp   rest-server
```

现在可以使用`docker stop/start/restart`等命令操作容器`rest-server`了

```
docker stop rest-server
rest-server

docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

docker start rest-server
rest-server

docker ps
CONTAINER ID   IMAGE           COMMAND                   CREATED              STATUS         PORTS                    NAMES
583b52000b1a   python-docker   "python3 -m flask ru…"   About a minute ago   Up 2 seconds   0.0.0.0:8000->5000/tcp   rest-server

docker restart rest-server
rest-server

docker ps
CONTAINER ID   IMAGE           COMMAND                   CREATED         STATUS        PORTS                    NAMES
583b52000b1a   python-docker   "python3 -m flask ru…"   2 minutes ago   Up 1 second   0.0.0.0:8000->5000/tcp   rest-server
```

还可以使用`docker rm`删除容器`rest-server`

```
docker stop rest-server
rest-server
docker rm rest-server
rest-server
```


## 列出所有容器

```
docker ps --all
CONTAINER ID   IMAGE           COMMAND                   CREATED          STATUS                        PORTS     NAMES
69b8bc4f3da7   python-docker   "python3 -m flask ru…"   16 minutes ago   Exited (137) 11 minutes ago             competent_tu
ef0d3a3fe979   python-docker   "python3 -m flask ru…"   20 minutes ago   Exited (0) 16 minutes ago               hardcore_jennings
57a7933c664f   python-docker   "python3 -m flask ru…"   24 minutes ago   Created                                 clever_brown
e0e002696653   python-docker   "python3 -m flask ru…"   25 minutes ago   Exited (0) 25 minutes ago               tender_austin
c6e148d1e00d   hello-world     "/hello"                  24 hours ago     Exited (0) 24 hours ago                 epic_grothendieck
```
可以看到所有容器，包括状态是`Exited`，表示已经被stop的容器

`Tip`: 快速删除所有容器

```
docker rm -f `docker ps -aq`

docker ps --all
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```
