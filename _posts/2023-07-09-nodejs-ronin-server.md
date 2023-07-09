---
layout: post
title: nodejs入门 - ronin server
categories: [nodejs, node, javascript, js]
description:
keywords: nodejs, node, javascript, js
mermaid: false
sequence: false
flow: false
mathjax: false
mindmap: false
mindmap2: false
---

# 初始化应用程序

## 创建目录
```
mkdir node-docker
cd node-docker
```

## 安装
```
npm init -y
Wrote to node-docker/package.json:

{
  "name": "docker",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

```
npm install ronin-server ronin-mocks

added 120 packages, and audited 121 packages in 37s

8 packages are looking for funding
  run `npm fund` for details

4 moderate severity vulnerabilities

Some issues need review, and may require choosing
a different dependency.

Run `npm audit` for details.
npm notice
npm notice New minor version of npm available! 9.5.1 -> 9.8.0
npm notice Changelog: https://github.com/npm/cli/releases/tag/v9.8.0
npm notice Run npm install -g npm@9.8.0 to update!
npm notice
```

## 程序代码
```
cat server.js
```

```
const ronin = require('ronin-server')
const mocks = require('ronin-mocks')

const server = ronin.server()

server.use('/', mocks.server(server.Router(), false, true))
server.start()
```

## 运行和测试

### 运行
```
node server.js
```

### 测试

打开新的终端

post

```
curl --request POST   --url http://localhost:8000/test   --header 'content-type: application/json'   --data '{"msg": "testing"}'
```

```
{"code":"success","payload":[{"msg":"testing","id":"e7821259-f510-4d56-825e-d9fb8d6cb840","createDate":"2023-07-09T06:33:38.209Z"}]}
```

get
```
curl http://localhost:8000/test
```

```
"code":"success","meta":{"total":1,"count":1},"payload":[{"msg":"testing","id":"e7821259-f510-4d56-825e-d9fb8d6cb840","createDate":"2023-07-09T06:33:38.209Z"}]}
```

回到运行终端窗口

```
2023-07-09T14:24:37:4290  INFO: POST /test
2023-07-09T14:25:05:4610  INFO: GET /test
```

# 使用docker方式

## Dockerfile

```
# syntax=docker/dockerfile:1

FROM node:18-alpine
ENV NODE_ENV=production

WORKDIR /app

COPY ["package.json", "package-lock.json*", "./"]

RUN npm install --production

COPY . .

CMD ["node", "server.js"]

```

## .dockerignore
```
node_modules
```

## 编译镜像

```
docker build --tag node-docker .
```

## 查看

```
docker images | head
REPOSITORY                       TAG               IMAGE ID       CREATED          SIZE
node-docker                      latest            76f1b84d50a3   46 seconds ago   188MB
```

打标签
```
docker tag node-docker:latest node-docker:v1.0.0
```

再次查看
```
docker images | head
REPOSITORY                       TAG               IMAGE ID       CREATED          SIZE
node-docker                      latest            76f1b84d50a3   46 seconds ago   188MB
node-docker                      v1.0.0            76f1b84d50a3   46 seconds ago   188MB
```

## 运行

```
docker run --publish 8000:8000 node-docker
```

验证
```
curl --request POST   --url http://localhost:8000/test   --header 'content-type: application/json'   --data '{"msg": "testing"}'
```

```
{"code":"success","payload":[{"msg":"testing","id":"a9dee620-f1c9-4a3f-ae8b-79dd859eb09c","createDate":"2023-07-09T06:32:50.914Z"}]}
```
