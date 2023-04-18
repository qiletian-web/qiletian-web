---
title: Have a Try
date: 2023-04-18 16:36:47
tags:
---

# 开始使用

## 概述

### 什么是Hexo

Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 [Markdown](http://daringfireball.net/projects/markdown/)（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

### 安装

#### 安装前提

安装 Hexo 相当简单，只需要先安装下列应用程序即可：

- [Node.js](http://nodejs.org/) (Node.js 版本需不低于 10.13，建议使用 Node.js 12.0 及以上版本)
- [Git](http://git-scm.com/)

如果您的电脑中已经安装上述必备程序，那么恭喜您！你可以直接前往 [安装 Hexo](https://hexo.io/zh-cn/docs/#安装-Hexo) 步骤。

如果您的电脑中尚未安装所需要的程序，请根据以下安装指示完成安装。

#### 安装GIT

- Windows：下载并安装 [git](https://git-scm.com/download/win).
- Mac：使用 [Homebrew](http://mxcl.github.com/homebrew/), [MacPorts](http://www.macports.org/) 或者下载 [安装程序](http://sourceforge.net/projects/git-osx-installer/)。
- Linux (Ubuntu, Debian)：`sudo apt-get install git-core`
- Linux (Fedora, Red Hat, CentOS)：`sudo yum install git-core`

#### 安装Node.js

Node.js 为大多数平台提供了官方的 [安装程序](https://nodejs.org/zh-cn/download/)。对于中国大陆地区用户，可以前往 [淘宝 Node.js 镜像](https://npmmirror.com/mirrors/node/) 下载。

其它的安装方法：

- Windows：通过 [nvs](https://github.com/jasongin/nvs/)（推荐）或者 [nvm](https://github.com/nvm-sh/nvm) 安装。
- Mac：使用 [Homebrew](https://brew.sh/) 或 [MacPorts](http://www.macports.org/) 安装。
- Linux（DEB/RPM-based）：从 [NodeSource](https://github.com/nodesource/distributions) 安装。
- 其它：使用相应的软件包管理器进行安装，可以参考由 Node.js 提供的 [指导](https://nodejs.org/zh-cn/download/package-manager/)。

对于 Mac 和 Linux 同样建议使用 nvs 或者 nvm，以避免可能会出现的权限问题。

#### 安装Hexo

所有必备的应用程序安装完成后，即可使用 npm 安装 Hexo。

```
$ npm install -g hexo-cli
```

#### 进阶安装和使用

对于熟悉 npm 的进阶用户，可以仅局部安装 `hexo` 包。

```
$ npm install hexo
```

安装以后，可以使用以下两种方式执行 Hexo：

1. `npx hexo <command>`
2. 将 Hexo 所在的目录下的 `node_modules` 添加到环境变量之中即可直接使用 `hexo <command>`：

```
echo 'PATH="$PATH:./node_modules/.bin"' >> ~/.profile
```

## 建站

安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。

```
$ hexo init <folder>
$ cd <folder>
$ npm install
```

新建完成后，指定文件夹的目录如下：

```
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

本地操作实例

```
hexo init myBlog
cd myBlog
npm install
hexo new "Have a Try"
hexo g
hexo server
```

上述命令行含义是

1. 创建一个新的文件夹myBlog作为Hexo的工作目录
2. 进入文件夹myBlog
3. 局部安装hexo
4. 创建新的文章 md文档
5. 将md文档生成静态html文件
6. 将页面渲染到本地服务器上

# 部署

## 将Hexo部署到GitLab Pages

在本教程中，我们将会使用 GitLab CI 将 Hexo 博客部署到 GitLab Pages 上。

新建一个 repository。如果你希望你的站点能通过 <你的 GitLab 用户名>.gitlab.io 域名访问，你的 repository 应该直接命名为 <你的 GitLab 用户名>.gitlab.io。

将你的 Hexo 站点文件夹推送到 repository 中。默认情况下 public 目录将不会（并且不应该）被推送到 repository 中，建议你检查 .gitignore 文件中是否包含 public 一行，如果没有请加上。
在你的站点文件夹中新建 .gitlab-ci.yml 文件：

```
image: node:10-alpine # use nodejs v10 LTS
cache:
  paths:
    - node_modules/

before_script:
  - npm install hexo-cli -g
  - npm install

pages:
  script:
    - hexo generate
  artifacts:
    paths:
      - public
  only:
    - master
```
GitLab CI 应该会自动开始运行，构建成功以后你应该可以在 https://<你的 GitLab 用户名>.gitlab.io 查看你的网站。
(可选) 如果你需要查看生成的文件，可以在 job artifact 中找到。
在 GitLab.com 上，GitLab CI 是默认启用的。如果你使用的是自托管的 GitLab，你可能需要在 Settings -> CI / CD -> Shared Runners 启用 GitLab CI。