---
layout: post
title: Docker入门教程5——使用docker-compose进行简化
categories: [docker, devops, python, mysql]
description:
keywords:
mermaid: false
sequence: false
flow: false
mathjax: false
mindmap: false
mindmap2: false
---

# docker-compose介绍
Docker Compose是一个工具，用于定义和共享多容器应用程序。使用Compose，我们可以创建一个YAML文件来定义服务，并通过单个命令来启动或停止所有服务。


# 安装docker compose
如果您已经在Windows、Mac或Linux上安装了Docker Desktop，那么Docker Compose已经包含在其中。 [独立安装参考](https://docs.docker.com/compose/install/)

安装完成后，运行以下命令查看版本信息：
```
docker compose version
Docker Compose version v2.19.0
```

# 使用docker-compose进行简化

### 构建
在VS Code中打开python-docker目录，并创建一个名为docker-compose.dev.yml的新文件，复制以下内容。
```
version: '3.8'

services:
 web:
  build:
   context: .
  ports:
  - 8000:5000
  volumes:
  - ./:/app

 mysqldb:
  image: mysql
  ports:
  - 3306:3306
  environment:
  - MYSQL_ROOT_PASSWORD=p@ssw0rd1
  volumes:
  - mysql:/var/lib/mysql
  - mysql_config:/etc/mysql

volumes:
  mysql:
  mysql_config:

```

### 启动
```
docker-compose -f docker-compose.dev.yml up --build
```

### 验证

```
curl http://localhost:8000/initdb
init database
```

```
curl http://localhost:8000/widgets
[{"name": "test_widget1", "description": "test widget1"}]
```
