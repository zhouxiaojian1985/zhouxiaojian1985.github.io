---
layout: post
title: Go入门教程0——安装golang
categories: [golang, go]
description:
keywords: golang, go
mermaid: false
sequence: false
flow: false
mathjax: false
mindmap: false
mindmap2: false
---

# [官方安装地址](https://go.dev/dl/)

镜像地址 [https://golang.google.cn/dl/](https://golang.google.cn/dl/)


# Ubuntu安装方式

## amd64
```
wget https://golang.google.cn/dl/go1.20.6.linux-amd64.tar.gz
sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf go1.20.6.linux-amd64.tar.gz
```

## arm64

下载，删除旧版本，并安装
```
wget https://golang.google.cn/dl/go1.20.6.linux-arm64.tar.gz
sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf go1.20.6.linux-arm64.tar.gz
```

验证
```
export PATH=$PATH:/usr/local/go/bin
go version
go version go1.20.6 linux/arm64
```



# mac m1 推荐安装方式

## 下载官方ARM64版本的pkg文件，双击后安装

![go install](/images/posts/go/go_install.png)

## 验证
```
go version
go version go1.20.5 darwin/arm64
```

## 安装路径

```
cd /usr/local/go
ls
CONTRIBUTING.md	PATENTS		SECURITY.md	api		codereview.cfg	lib		pkg		test
LICENSE		README.md	VERSION		bin		doc		misc		src

which go
/usr/local/go/bin/go
```

## 环境变量配置$GOROOT和$GOPATH(可选)

```
export GOPATH=/Users/xiaojianzhou/go
export GOROOT=/usr/local/go
```

## 卸载旧版本(可选)

```
go version
go version go1.18.3 darwin/arm64
```

```
cd /usr/local
sudo mv go go1.18.3
```

## 加速代理配置

### [goproxy](https://goproxy.cn/)
```
cat ~/.zshrc
export GO111MODULE=on
export GOPROXY=https://goproxy.cn
```

常用加速配置
- [七牛Goproxy 中国](https://goproxy.cn)
- [阿里](mirrors.aliyun.com/goproxy/)
- [官方： 全球 CDN 加速 ](https://goproxy.io/)
- [其他：jfrog 维护](https://gocenter.io)


### Dockerfile中加速

```
# goproxy
ENV GO111MODULE=on \
    GOPROXY=https://goproxy.cn,direct
```
