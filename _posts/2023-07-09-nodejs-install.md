---
layout: post
title: 安装nodejs
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

# [官方安装地址](https://nodejs.org/en)

# mac m1 推荐安装方式

## 下载官方的pkg文件，双击后安装

![docker arch](/images/posts/node/nodejs_install.png)

最后
```
This package has installed:
	•	Node.js v18.16.1 to /usr/local/bin/node
	•	npm v9.5.1 to /usr/local/bin/npm
Make sure that /usr/local/bin is in your $PATH.
```

验证
```
which node
/usr/local/bin/node

node -v
v18.16.1

which npm
/usr/local/bin/npm

npm -v
9.5.1
```

## 使用brew

```
brew search nodejs
==> Formulae
node                               nodenv                             node@16                            node@14                            node@10                            node@18

==> Casks
nodeclipse
```

选择[LTS](https://github.com/nodejs/release#release-schedule)进行安装，这里是18

```
brew install node@18
==> Auto-updated Homebrew!
Updated 2 taps (homebrew/core and homebrew/cask).
==> New Formulae
adb-enhanced       blades             cbonsai            cycode             fuc                hex                libversion         ntbtls             runme              trufflehog         xe
bilix              cargo-binstall     crabz              driftwood          fw                 libdivsufsort      lr                 proxygen           sh4d0wup           trzsz-ssh
==> New Casks
chatall                                   elektron-overbridge                       flexoptix                                 screen-studio                             whisky

You have 1 outdated formula installed.

==> Fetching dependencies for node@18: brotli, c-ares, icu4c, libnghttp2, libuv and openssl@3
==> Fetching brotli
==> Downloading https://mirrors.ustc.edu.cn/homebrew-bottles/bottles/brotli-1.0.9.arm64_ventura.bottle.tar.gz
############################################################################################################################################################################################################# 100.0%
==> Fetching c-ares
==> Downloading https://mirrors.ustc.edu.cn/homebrew-bottles/bottles/c-ares-1.19.1.arm64_ventura.bottle.tar.gz
############################################################################################################################################################################################################# 100.0%
==> Fetching icu4c
==> Downloading https://mirrors.ustc.edu.cn/homebrew-bottles/bottles/icu4c-73.2.arm64_ventura.bottle.tar.gz
############################################################################################################################################################################################################# 100.0%
==> Fetching libnghttp2
==> Downloading https://mirrors.ustc.edu.cn/homebrew-bottles/bottles/libnghttp2-1.54.0.arm64_ventura.bottle.tar.gz
############################################################################################################################################################################################################# 100.0%
==> Fetching libuv
==> Downloading https://mirrors.ustc.edu.cn/homebrew-bottles/bottles/libuv-1.46.0.arm64_ventura.bottle.tar.gz
############################################################################################################################################################################################################# 100.0%
==> Fetching openssl@3
==> Downloading https://mirrors.ustc.edu.cn/homebrew-bottles/bottles/openssl%403-3.1.1_1.arm64_ventura.bottle.tar.gz
############################################################################################################################################################################################################# 100.0%
==> Fetching node@18
==> Downloading https://mirrors.ustc.edu.cn/homebrew-bottles/bottles/node%4018-18.16.1_1.arm64_ventura.bottle.tar.gz
############################################################################################################################################################################################################# 100.0%
==> Installing dependencies for node@18: brotli, c-ares, icu4c, libnghttp2, libuv and openssl@3
==> Installing node@18 dependency: brotli
==> Pouring brotli-1.0.9.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/brotli/1.0.9: 25 files, 2.3MB
==> Installing node@18 dependency: c-ares
==> Pouring c-ares-1.19.1.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/c-ares/1.19.1: 87 files, 681KB
==> Installing node@18 dependency: icu4c
==> Pouring icu4c-73.2.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/icu4c/73.2: 268 files, 80.1MB
==> Installing node@18 dependency: libnghttp2
==> Pouring libnghttp2-1.54.0.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libnghttp2/1.54.0: 13 files, 731.2KB
==> Installing node@18 dependency: libuv
==> Pouring libuv-1.46.0.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libuv/1.46.0: 47 files, 3MB
==> Installing node@18 dependency: openssl@3
==> Pouring openssl@3-3.1.1_1.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/openssl@3/3.1.1_1: 6,495 files, 28.4MB
==> Installing node@18
==> Pouring node@18-18.16.1_1.arm64_ventura.bottle.tar.gz
==> Caveats
node@18 is keg-only, which means it was not symlinked into /opt/homebrew,
because this is an alternate version of another formula.

If you need to have node@18 first in your PATH, run:
  echo 'export PATH="/opt/homebrew/opt/node@18/bin:$PATH"' >> ~/.zshrc

For compilers to find node@18 you may need to set:
  export LDFLAGS="-L/opt/homebrew/opt/node@18/lib"
  export CPPFLAGS="-I/opt/homebrew/opt/node@18/include"
==> Summary
🍺  /opt/homebrew/Cellar/node@18/18.16.1_1: 2,341 files, 54.8MB
==> Running `brew cleanup node@18`...
Disable this behaviour by setting HOMEBREW_NO_INSTALL_CLEANUP.
Hide these hints with HOMEBREW_NO_ENV_HINTS (see `man brew`).
==> Caveats
==> node@18
node@18 is keg-only, which means it was not symlinked into /opt/homebrew,
because this is an alternate version of another formula.

If you need to have node@18 first in your PATH, run:
  echo 'export PATH="/opt/homebrew/opt/node@18/bin:$PATH"' >> ~/.zshrc

For compilers to find node@18 you may need to set:
  export LDFLAGS="-L/opt/homebrew/opt/node@18/lib"
  export CPPFLAGS="-I/opt/homebrew/opt/node@18/include"
```

验证版本
```
echo 'export PATH="/opt/homebrew/opt/node@18/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

```
node -v
v18.16.1

npm -v
9.5.1

```

# Ubuntu LTS [推荐安装方式](https://github.com/nodesource/distributions#installation-instructions)

例如，安装Node.js v18.x:
```
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - &&\
sudo apt-get install -y nodejs
```
