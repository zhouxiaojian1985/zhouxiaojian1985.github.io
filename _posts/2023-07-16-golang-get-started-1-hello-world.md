---
layout: post
title: Go入门教程1——hello world
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

# Hello World

初始化目录
```
cd ~
mkdir hello
cd hello
```

使用[go mod](https://go.dev/doc/modules/managing-dependencies#naming_module)初始化
```
go mod init example/hello
```
自Go 1.11版本开始引入。Go Mod用于管理Go项目的依赖关系和版本控制。
它简化了Go项目的依赖管理过程，提供了更好的版本控制和构建可重复性。
它是Go语言推荐的官方模块管理方式，取代了以前使用的GOPATH和dep等工具。


创建文件并复制代码
```
vim hello.go
```

```
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

运行
```
go run .
Hello, World!
```

# 调用外部包[quote](https://pkg.go.dev/rsc.io/quote)

```
vim hello.go
```

修改代码
```
package main

import "fmt"

import "rsc.io/quote"

func main() {
    fmt.Println(quote.Go())
}
```

使用go mod根据代码中的导入语句，自动添加、删除或更新go.mod文件中的依赖项
```
go mod tidy
go: finding module for package rsc.io/quote
go: found rsc.io/quote in rsc.io/quote v1.5.2
```

运行
```
go run .
Don't communicate by sharing memory, share memory by communicating.
```
