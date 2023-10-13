---
title: 快速使用Hexo搭建个人博客
date: 2023-04-18 16:36:47
updated: 2023-10-13 14:22:29
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

- _config.yml
网站的配置信息，可以在此配置大部分的参数
-  package.json
应用程序的信息。
- scaffolds
模版 文件夹。当您新建文章时，Hexo 会根据 scaffold 来创建文件。
Hexo 的模板是指在新建的文章文件中默认填充的内容。例如，如果您修改 scaffold/post.md 中的 Front-matter 内容，那么每次新建一篇文章时都会包含这个修改。
- source
资源文件夹是存放用户资源的地方。除 _posts 文件夹之外，开头命名为 _ (下划线)的文件 / 文件夹和隐藏的文件将会被忽略。Markdown 和 HTML 文件会被解析并放到 public 文件夹，而其他文件会被拷贝过去。
- themes
主题 文件夹。Hexo 会根据主题来生成静态页面。

## 配置

可以在 _config.yml 或 代替配置文件 中修改大部分的配置。

### 网站

| 参数        | 描述                         |
| ---------- | ---------------------------- |
| title       | 网站标题                     |
| subtitle    | 网站副标题                   |
| description | 网站描述                     |
| keywords    | 网站的关键词。支持多个关键词 |
| author      | 您的名字                     |
| language    | 网站使用的语言。             |
| timezone    | 网站时区                     |



# 写作

## 概述命令

```
hexo init myBlog
cd myBlog
npm install
hexo new "Have a Try"
hexo g
hexo server
```

上述命令行含义是

1. hexo init myBlog创建一个新的文件夹myBlog作为Hexo的工作目录
2. cd myBlog进入文件夹myBlog
3. npm install局部安装hexo
4. hexo new "Have a Try"在source文件夹下的_POST文件夹下创建新的文章 md文档
5. hexo g将md文档生成静态html文件
6. hexo server将页面渲染到本地服务器上

你可以执行下列命令来创建一篇新文章或者新的页面。

```
$ hexo new [layout] <title>
```

您可以在命令中指定文章的布局（layout），默认为 post，可以通过修改 _config.yml 中的 default_layout 参数来指定默认布局。

## 布局

Hexo 有三种默认布局：post、page 和 draft。在创建这三种不同类型的文件时，它们将会被保存到不同的路径；而您自定义的其他布局和 post 相同，都将储存到 source/_posts 文件夹。

### 草稿
刚刚提到了 Hexo 的一种特殊布局：draft，这种布局在建立时会被保存到 source/_drafts 文件夹，您可通过 publish 命令将草稿移动到 source/_posts 文件夹，该命令的使用方式与 new 十分类似，您也可在命令中指定 layout 来指定布局。
```
$ hexo publish [layout] <title>
```
草稿默认不会显示在页面中，您可在执行时加上 --draft 参数，或是在 _config.yml 中把 render_drafts 参数设为 true 来预览草稿。
## 模版（Scaffold）
在新建文章时，Hexo 会根据 scaffolds 文件夹内相对应的文件来建立文件，例如：
``` 
$ hexo new photo "My Gallery"
```
在执行这行指令时，Hexo 会尝试在 scaffolds 文件夹中寻找 photo.md，并根据其内容建立文章，以下是您可以在模版中使用的变量：

|变量|	描述|
|----|---|
|layout|	布局|
|title	|标题|
|date	|文件建立日期|

# 资源文件夹


对于那些想要更有规律地提供图片和其他资源以及想要将他们的资源分布在各个文章上的人来说，Hexo也提供了更组织化的方式来管理资源。这个稍微有些复杂但是管理资源非常方便的功能可以通过将 config.yml 文件中的 `post_asset_folder `选项设为` true` 来打开。

```
_config.yml
post_asset_folder: true
```

当资源文件管理功能打开后，Hexo将会在你每一次通过` hexo new [layout] <title>` 命令创建新文章时自动创建一个文件夹。这个资源文件夹将会有与这个文章文件一样的名字。将所有与你的文章有关的资源放在这个关联文件夹中之后，你可以通过相对路径来引用它们，这样你就得到了一个更简单而且方便得多的工作流。

# 服务器 

## hexo-server

Hexo 3.0 把服务器独立成了个别模块，您必须先安装 hexo-server 才能使用。
```
$ npm install hexo-server --save
```
安装完成后，输入以下命令以启动服务器，您的网站会在 http://localhost:4000 下启动。在服务器启动期间，Hexo 会监视文件变动并自动更新，您无须重启服务器。
```
$ hexo server
```
如果您想要更改端口，或是在执行时遇到了` EADDRINUSE` 错误，可以在执行时使用` -p` 选项指定其他端口，如下：
```
$ hexo server -p 5000
```

## 静态模式

在静态模式下，服务器只处理 public 文件夹内的文件，而不会处理文件变动，在执行时，您应该先自行执行 `hexo generate`，此模式通常用于生产环境（production mode）下。
```
$ hexo server -s
```

## 自定义 IP
服务器默认运行在 `0.0.0.0`，您可以覆盖默认的 IP 设置，如下：
```
$ hexo server -i 192.168.1.1
```
指定这个参数后，您就只能通过该IP才能访问站点。例如，对于一台使用无线网络的笔记本电脑，除了指向本机的`127.0.0.1`外，通常还有一个`192.168.*.*`的局域网IP，如果像上面那样使用`-i`参数，就不能用`127.0.0.1`来访问站点了。对于有公网IP的主机，如果您指定一个局域网IP作为`-i`参数的值，那么就无法通过公网来访问站点。

# 生成器

## 生成文件
使用 Hexo 生成静态文件快速而且简单。
```
$ hexo generate
```
### 监视文件变动
Hexo 能够监视文件变动并立即重新生成静态文件，在生成时会比对文件的 SHA1 checksum，只有变动的文件才会写入。
```
$ hexo generate --watch
```
### 完成后部署
您可执行下列的其中一个命令，让 Hexo 在生成完毕后自动部署网站，两个命令的作用是相同的。
```
$ hexo generate --deploy
$ hexo deploy --generate
```
简写

上面两个命令可以简写为
```
$ hexo g -d
$ hexo d -g
```

# 部署

## 将Hexo部署到GitHub Pages

本文将使用 GitHub Actions 部署至 GitHub Pages，此方法适用于公开或私人储存库。若你不希望将源文件夹上传到 GitHub，请参阅 一键部署。

1. 建立名为`<你的 GitHub 用户名>.github.io` 的储存库，若之前已将 Hexo 上传至其他储存库，将该储存库重命名即可。
2. 将 Hexo 文件夹中的文件 push 到储存库的默认分支，默认分支通常名为 main，旧一点的储存库可能名为 master。
- 将 `main` 分支 push 到 GitHub：
```
$ git push -u origin main
```

-  默认情况下 public/ 不会被上传(也不该被上传)，确保`.gitignore` 文件中包含一行 `public/`。整体文件夹结构应该与 范例储存库 大致相似。

3. 使用` node --version` 指令检查你电脑上的 Node.js 版本，并记下该版本 (例如：`v16.y.z`)
4. 在储存库中建立` .github/workflows/pages.yml`，并填入以下内容 (将 16 替换为上个步骤中记下的版本)：
```
name: Pages

on:
  push:
    branches:
      - main # default branch

jobs:
  pages:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: actions/checkout@v2
      - name: Use Node.js 16.x
        uses: actions/setup-node@v2
        with:
          node-version: "16"
      - name: Cache NPM dependencies
        uses: actions/cache@v2
        with:
          path: node_modules
          key: ${{ runner.OS }}-npm-cache
          restore-keys: |
            ${{ runner.OS }}-npm-cache
      - name: Install Dependencies
        run: npm install
      - name: Build
        run: npm run build
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```
5. 当部署作业完成后，产生的页面会放在储存库中的 gh-pages 分支。
6. 在储存库中前往 Settings > Pages > Source，并将 branch 改为 gh-pages。
7. 前往 https://<你的 GitHub 用户名>.github.io 查看网站。
CNAME
若你使用了一个带有 CNAME 的自定义域名，你需要在 source/ 文件夹中新增 CNAME 文件。 更多信息

# 将 Hexo 部署到 GitLab Pages
在本教程中，我们将会使用 GitLab CI 将 Hexo 博客部署到 GitLab Pages 上。

1. 新建一个 repository。如果你希望你的站点能通过 <你的 GitLab 用户名>.gitlab.io 域名访问，你的 repository 应该直接命名为 <你的 GitLab 用户名>.gitlab.io。
2. 将你的 Hexo 站点文件夹推送到 repository 中。默认情况下 public 目录将不会（并且不应该）被推送到 repository 中，建议你检查 .gitignore 文件中是否包含 public 一行，如果没有请加上。
3. 在你的站点文件夹中新建 .gitlab-ci.yml 文件：
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
4. GitLab CI 应该会自动开始运行，构建成功以后你应该可以在 https://<你的 GitLab 用户名>.gitlab.io 查看你的网站。
5. (可选) 如果你需要查看生成的文件，可以在 job artifact 中找到。
> 在 GitLab.com 上，GitLab CI 是默认启用的。如果你使用的是自托管的 GitLab，你可能需要在 Settings -> CI / CD -> Shared Runners 启用 GitLab CI。

## Project page
如果你更希望你的站点部署在 `<你的 GitLab 用户名>.gitlab.io` 的子目录中，你的 repository 需要直接命名为子目录的名字，这样你的站点可以通过 `https://<你的 GitLab 用户名>.gitlab.io/<repository 的名字>` 访问。你需要检查你的 Hexo 配置文件，将 url 的值修改为` https://<你的 GitLab 用户名>.gitlab.io/<repository 的名字>`、将 root 的值修改为` /<repository 的名字>/`






