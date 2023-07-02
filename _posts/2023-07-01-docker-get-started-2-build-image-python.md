---
layout: post
title: Docker入门教程2——构建python镜像
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

## 示例应用程序

示例应用程序使用Python流行的Flask框架。
创建一个名为python-docker的目录，并按照以下步骤激活Python虚拟环境、安装Flask作为依赖项，并创建一个Python代码文件。

```
mkdir -p $HOME/learn/python/python-docker
cd $HOME/learn/python/python-docker

python3 -m venv .venv
source .venv/bin/activate

python3 -m pip install Flask
python3 -m pip freeze > requirements.txt
touch app.py
```

添加用于处理简单Web请求的代码。在Visual Studio Code或您喜欢的其它IDE中打开python-docker目录，并将以下代码输入app.py文件中。

```
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, Docker!'
```


## 测试应用程序

启动应用程序并确保它正在运行。打开终端并导航到您创建的工作目录。

```
cd $HOME/learn/python/python-docker
. .venv/bin/activate
python3 -m flask run
 * Debug mode: off
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on http://127.0.0.1:5000
```

使用curl验证
```
curl http://127.0.0.1:5000
Hello, Docker!
```

切换回运行服务器的终端的结果
```
127.0.0.1 - - [02/Jul/2023 11:12:08] "GET / HTTP/1.1" 200 -
```


# 创建一个Dockerfile

```

#syntax=docker/dockerfile:1

FROM python:3.8-slim-buster

WORKDIR /app

COPY requirements.txt requirements.txt
RUN pip3 install -r requirements.txt

COPY . .

CMD ["python3", "-m" , "flask", "run", "--host=0.0.0.0"]
```

现在的目录结构

```
tree
.
├── Dockerfile
├── app.py
└── requirements.txt

1 directory, 3 files
```

# 编译镜像

先使用`docker pull`获取python基础镜像以加快编译镜像
```
docker pull python:3.8-slim-buster
```

使用`docker build`编译镜像
```
docker build --tag python-docker .
```

查看本地镜像
```
docker images
REPOSITORY        TAG               IMAGE ID       CREATED         SIZE
python-docker     latest            3796f1745aca   3 minutes ago   133MB
python            3.8-slim-buster   ebe69edfe405   3 weeks ago     111MB
```


# 给镜像打标签

```
docker tag python-docker:latest python-docker:v1.0.0
```

再次查看本地镜像
```
docker images
REPOSITORY        TAG               IMAGE ID       CREATED         SIZE
python-docker     latest            3796f1745aca   6 minutes ago   133MB
python-docker     v1.0.0            3796f1745aca   6 minutes ago   133MB
python            3.8-slim-buster   ebe69edfe405   3 weeks ago     111MB
```

如果删除tag，不会影响原来的镜像

```
docker rmi python-docker:v1.0.0
Untagged: python-docker:v1.0.0
```

再次查看本地镜像，`python-docker:lastest`仍旧存在
```
docker images
REPOSITORY        TAG               IMAGE ID       CREATED         SIZE
python-docker     latest            3796f1745aca   7 minutes ago   133MB
python            3.8-slim-buster   ebe69edfe405   3 weeks ago     111MB
```
