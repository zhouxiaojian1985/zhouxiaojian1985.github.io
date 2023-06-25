---
layout: post
title: M1 芯片 Mac 上 Homebrew 安装
categories: [Mac]
description: 转载
keywords: mac, arm, homebrew, brew
mermaid: false
sequence: false
flow: false
mathjax: false
mindmap: false
mindmap2: false
---

# M1 芯片 Mac 上 Homebrew 安装

转载自: https://brew.idayer.com/

原因：
 - 这个版本来自[阿里云Homebrew镜像](https://developer.aliyun.com/mirror/homebrew)的评论，用起来很流畅
 - [清华Homebrew镜像](https://mirrors.tuna.tsinghua.edu.cn/help/homebrew/)说了一大堆，用起来还是不流畅，各种卡住

## 安装 ARM 版 Homebrew

`ARM`版`Homebrew`最终被安装在`/opt/homebrew`路径下。

直接执行：

```shell
/bin/bash -c "$(curl -fsSL https://gitee.com/ineo6/homebrew-install/raw/master/install.sh)"
```

然后还需设置环境变量，具体操作步骤如下，一定要仔细阅读。

1. 在终端执行命令`echo $SHELL`获得终端类型：

   - `/bin/zsh` => `zsh` => `.zprofile`
   - `/bin/bash` => `bash` => `.bash_profile`

2. 如果看到的是`/bin/zsh`

   ```shell
   echo 'eval "$(/opt/homebrew/bin/brew shellenv)" #brew.idayer.com' >> ~/.zprofile
   eval "$(/opt/homebrew/bin/brew shellenv)"
   ```

   如果看到的是`/bin/bash`

   ```shell
   echo 'eval "$(/opt/homebrew/bin/brew shellenv)" #brew.idayer.com' >> ~/.bash_profile
   eval "$(/opt/homebrew/bin/brew shellenv)"
   ```

> 从`macOS Catalina`(10.15.x) 版开始，`Mac`使用`zsh`作为默认`Shell`。

扩展阅读：[在 Mac 上将 zsh 用作默认 Shell](https://support.apple.com/zh-cn/HT208050)

## 安装 X86 版 Homebrew

因为目前很多软件包没有支持`ARM`架构，我们也可以考虑使用`x86`版的`Homebrew`。

在命令前面添加`arch -x86_64`，就可以按 X86 模式执行该命令，比如：

```shell
arch -x86_64 /bin/bash -c "$(curl -fsSL https://gitee.com/ineo6/homebrew-install/raw/master/install.sh)"
```

## 多版本共存

如果你同时安装了 ARM 和 X86 两个版本，那你需要设置别名，把命令区分开。

同样是`.zprofile`或者`.bash_profile`里面添加：

至于操作哪个文件，请参考前文关于终端类型的描述，下文如有类似文字，保持一样的操作。

```shell
alias abrew='arch -arm64 /opt/homebrew/bin/brew'
alias ibrew='arch -x86_64 /usr/local/bin/brew'
```

`abrew`、`ibrew`可以根据你的喜好自定义。

然后再执行`source ~/.zprofile`或`source ~/.bash_profile`命令更新文件。

## 设置镜像

**注意：本文中的安装脚本会设置中科大源镜像，如果你也想设置`cask`和`bottles`的镜像，请按下面注释部分选择执行代码。**

更详细的教程可以参考前面的文章：[设置镜像](/guide/start/#part3) 。

执行时根据实际情况修改`"$(brew --repo)"`代码中的`brew`。

意思是如果你只是使用一个版本`Homebrew`，直接执行命令即可，如果你想多个版本共存或者使用了别名，就把`brew`关键字替换为别名名称，如前面的`abrew`、`ibrew`。

```shell
# brew
git -C "$(brew --repo)" remote set-url origin https://mirrors.ustc.edu.cn/brew.git

# core
git -C "$(brew --repo homebrew/core)" remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git

# cask
git -C "$(brew --repo homebrew/cask)" remote set-url origin https://mirrors.ustc.edu.cn/homebrew-cask.git

# bottles for zsh 和下面2选1
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles/bottles' >> ~/.zprofile
source ~/.zprofile

# bottles for bash 和上面2选1
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles/bottles' >> ~/.bash_profile
source ~/.bash_profile
```

**如果觉得教程有用，欢迎多多分享宣传~**

[mac]:[https://zhuanlan.zhihu.com/p/90508170][github]:[https://github.com/ineo6/homebrew-install]
