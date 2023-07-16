---
layout: post
title: Go入门教程2——创建和使用自己的mod模块
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

## 初始化目录
```
cd ~
mkdir greetings
cd greetings
```

## 初始化mod模块

```
go mod init example.com/greetings
```

## 增加代码

```
vim greetings.go
```

```
package greetings

import "fmt"

// Hello returns a greeting for the named person.
func Hello(name string) string {
    // Return a greeting that embeds the name in a message.
    message := fmt.Sprintf("Hi, %v. Welcome!", name)
    return message
}
```

## 调用greetings模块

初始化调用目录
```
cd ..
mkdir hello
cd hello
```

初始化调用模块
```
go mod init example.com/hello
```

```
vim hello.go
```

```
package main

import (
    "fmt"

    "example.com/greetings"
)

func main() {
    // Get a greeting message and print it.
    message := greetings.Hello("Gladys")
    fmt.Println(message)
}
```


### 调用错误
```
go run hello.go
hello.go:6:5: no required module provides package example.com/greetings; to add it:
	go get example.com/greetings
```

### 使用go mod edit修复错误

```
go mod edit -replace example.com/greetings=../greetings
```

```
cat go.mod
module example.com/hello

go 1.20

replace example.com/greetings => ../greetings
```

使用go mod tidy解决go.mod文件中的依赖项
```
go mod tidy
go: found example.com/greetings in example.com/greetings v0.0.0-00010101000000-000000000000
```

```
cat go.mod
module example.com/hello

go 1.20

replace example.com/greetings => ../greetings

require example.com/greetings v0.0.0-00010101000000-000000000000
```

运行
```
go run .
Hi, Gladys. Welcome!
```
