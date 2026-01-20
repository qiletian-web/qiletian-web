---
title: 快速使用Hexo搭建个人博客
categories: Hexo
tags:
  - Git
  - Hexo
  - GitHub
  - GitLab
abbrlink: d87f7b4f
date: 2023-04-18 16:36:47
updated: 2023-10-13 14:22:29
---

# 环境配置

## 什么是Hexo

Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 [Markdown](http://daringfireball.net/projects/markdown/)（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

安装 Hexo 相当简单，只需要先安装下列应用程序即可：

- [Node.js](http://nodejs.org/) (Node.js 版本需不低于 10.13，建议使用 Node.js 12.0 及以上版本)
- [Git](http://git-scm.com/)

如果您的电脑中已经安装上述必备程序，那么恭喜您！你可以直接前往 [安装 Hexo](https://hexo.io/zh-cn/docs/#安装-Hexo) 步骤。

如果您的电脑中尚未安装所需要的程序，请根据以下安装指示完成安装。

## 安装GIT

- Windows：下载并安装 [git](https://git-scm.com/download/win).
- Mac：使用 [Homebrew](http://mxcl.github.com/homebrew/), [MacPorts](http://www.macports.org/) 或者下载 [安装程序](http://sourceforge.net/projects/git-osx-installer/)。
- Linux (Ubuntu, Debian)：`sudo apt-get install git-core`
- Linux (Fedora, Red Hat, CentOS)：`sudo yum install git-core`

## 安装Node.js

Node.js 为大多数平台提供了官方的 [安装程序](https://nodejs.org/zh-cn/download/)。对于中国大陆地区用户，可以前往 [淘宝 Node.js 镜像](https://npmmirror.com/mirrors/node/) 下载。

其它的安装方法：

- Windows：通过 [nvs](https://github.com/jasongin/nvs/)（推荐）或者 [nvm](https://github.com/nvm-sh/nvm) 安装。
- Mac：使用 [Homebrew](https://brew.sh/) 或 [MacPorts](http://www.macports.org/) 安装。
- Linux（DEB/RPM-based）：从 [NodeSource](https://github.com/nodesource/distributions) 安装。
- 其它：使用相应的软件包管理器进行安装，可以参考由 Node.js 提供的 [指导](https://nodejs.org/zh-cn/download/package-manager/)。

对于 Mac 和 Linux 同样建议使用 nvs 或者 nvm，以避免可能会出现的权限问题。

## 安装Hexo

所有必备的应用程序安装完成后，即可使用 npm 安装 Hexo。

- 全局安装 Hexo 的命令行工具
```
$ npm install -g hexo-cli
```
-g（全局标志）: 表示将包安装到全局环境，而不是当前项目的本地环境。全局安装使得相关的命令行工具在整个系统中都可用，而不仅限于特定项目。

- 对于熟悉 npm 的进阶用户，可以仅局部安装 `hexo` 包。
```
$ npm install hexo
```

安装以后，可以使用以下两种方式执行 Hexo：

1. `npx hexo <command>`
2. 将 Hexo 所在的目录下的 `node_modules` 添加到环境变量之中即可直接使用 `hexo <command>`：

```
echo 'PATH="$PATH:./node_modules/.bin"' >> ~/.profile
```

# Hexo基础使用和命令

## 建站命令`init`

安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。

```
$ hexo init <folder>
$ cd <folder>
$ npm install
```
`hexo init <folder>`表示新建一个网站。如果没有设置 folder ，Hexo 默认在目前的文件夹建立网站。

本命令相当于执行了以下几步：

1. `Git clone hexo-starter` 和 `hexo-theme-landscape` 主题到当前目录或指定目录。
2. 使用 Yarn 1、pnpm 或 npm 包管理器下载依赖（如有已安装多个，则列在前面的优先）。npm 默认随 Node.js 安装。

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

- package.json
  应用程序的信息。

- scaffolds
  模版 文件夹。当您新建文章时，Hexo 会根据 scaffold 来创建文件。
  Hexo 的模板是指在新建的文章文件中默认填充的内容。例如，如果您修改 scaffold/post.md 中的 Front-matter 内容，那么每次新建一篇文章时都会包含这个修改。

- source
  资源文件夹是存放用户资源的地方。除 _posts 文件夹之外，开头命名为 _ (下划线)的文件 / 文件夹和隐藏的文件将会被忽略。Markdown 和 HTML 文件会被解析并放到 public 文件夹，而其他文件会被拷贝过去。

- themes
  主题 文件夹。Hexo 会根据主题来生成静态页面。

## 新建文章new

```
$ hexo new [layout] <title>
```

新建一篇文章。如果没有设置 `layout` 的话，默认使用 [_config.yml](https://hexo.io/zh-cn/docs/configuration) 中的 `default_layout` 参数代替。如果标题包含空格的话，请使用引号括起来。

```
$ hexo new "post title with whitespace"
```

| 参数              | 描述                                          |
| :---------------- | :-------------------------------------------- |
| `-p`, `--path`    | 自定义新文章的路径                            |
| `-r`, `--replace` | 如果存在同名文章，将其替换                    |
| `-s`, `--slug`    | 文章的 Slug，作为新文章的文件名和发布后的 URL |

默认情况下，Hexo 会使用文章的标题来决定文章文件的路径。对于独立页面来说，Hexo 会创建一个以标题为名字的目录，并在目录中放置一个 `index.md` 文件。你可以使用 `--path` 参数来覆盖上述行为、自行决定文件的目录：

```
hexo new page --path about/me "About me"
```

以上命令会创建一个 `source/about/me.md` 文件，同时 Front Matter 中的 title 为 `"About me"`

注意！title 是必须指定的！如果你这么做并不能达到你的目的：

```
hexo new page --path about/me
```

此时 Hexo 会创建 `source/_posts/about/me.md`，同时 `me.md` 的 Front Matter 中的 title 为 `"page"`。这是因为在上述命令中，hexo-cli 将 `page` 视为指定文章的标题、并采用默认的 `layout`。

## 生成静态文件generate

```
$ hexo generate
```

生成静态文件。

| 选项                  | 描述                                                         |
| :-------------------- | :----------------------------------------------------------- |
| `-d`, `--deploy`      | 文件生成后立即部署网站                                       |
| `-w`, `--watch`       | 监视文件变动                                                 |
| `-b`, `--bail`        | 生成过程中如果发生任何未处理的异常则抛出异常                 |
| `-f`, `--force`       | 强制重新生成文件 Hexo 引入了差分机制，如果 `public` 目录存在，那么 `hexo g` 只会重新生成改动的文件。 使用该参数的效果接近 `hexo clean && hexo generate` |
| `-c`, `--concurrency` | 最大同时生成文件的数量，默认无限制                           |

该命令可以简写为

```
$ hexo g
```

### 监视文件变动

Hexo 能够监视文件变动并立即重新生成静态文件，在生成时会比对文件的 SHA1 checksum，只有变动的文件才会写入。

```
$ hexo generate --watch
```

## 发布publish

```
$ hexo publish [layout] <filename>
```

发表草稿。

## 启动服务器server

```
$ hexo server
```

如果在本地启动服务器。默认情况下，访问网址为： `http://localhost:4000/`。

| 选项             | 描述                           |
| :--------------- | :----------------------------- |
| `-p`, `--port`   | 重设端口                       |
| `-s`, `--static` | 只使用静态文件                 |
| `-l`, `--log`    | 启动日记记录，使用覆盖记录格式 |

Hexo 3.0 把服务器独立成了个别模块，必须先安装 hexo-server 才能使用。

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

### 静态模式

在静态模式下，服务器只处理 public 文件夹内的文件，而不会处理文件变动，在执行时，您应该先自行执行 `hexo generate`，此模式通常用于生产环境（production mode）下。

```
$ hexo server -s
```

### 自定义 IP

服务器默认运行在 `0.0.0.0`，您可以覆盖默认的 IP 设置，如下：

```
$ hexo server -i 192.168.1.1
```

指定这个参数后，您就只能通过该IP才能访问站点。例如，对于一台使用无线网络的笔记本电脑，除了指向本机的`127.0.0.1`外，通常还有一个`192.168.*.*`的局域网IP，如果像上面那样使用`-i`参数，就不能用`127.0.0.1`来访问站点了。对于有公网IP的主机，如果您指定一个局域网IP作为`-i`参数的值，那么就无法通过公网来访问站点。

## 部署网站deploy

```
$ hexo deploy
```

部署网站。

| 参数               | 描述                     |
| :----------------- | :----------------------- |
| `-g`, `--generate` | 部署之前预先生成静态文件 |

该命令可以简写为：

```
$ hexo d
```

### 完成后部署

您可执行下列的其中一个命令，让 Hexo 在生成完毕后自动部署网站，两个命令的作用是相同的。

```
$ hexo generate --deploy
$ hexo deploy --generate
```

上面两个命令可以简写为

```
$ hexo g -d
$ hexo d -g
```

## 渲染文件render

```
$ hexo render <file1> [file2] ...
```

渲染文件。

| 参数             | 描述         |
| :--------------- | :----------- |
| `-o`, `--output` | 设置输出路径 |

## 内容迁移migrate

```
$ hexo migrate <type>
```

从其他博客系统 [迁移内容](https://hexo.io/zh-cn/docs/migration)。

## 清除缓存clean

```
$ hexo clean
```

清除缓存文件 (`db.json`) 和已生成的静态文件 (`public`)。

在某些情况（尤其是更换主题后），如果发现您对站点的更改无论如何也不生效，您可能需要运行该命令。

## 列出网站资料list

```
$ hexo list <type>
```

列出网站资料。

## 显示Hexo版本version

```
$ hexo version
```

显示 Hexo 版本。

## 其他选项

### 安全模式

```
$ hexo --safe
```

在安全模式下，不会载入插件和脚本。当您在安装新插件遭遇问题时，可以尝试以安全模式重新执行。

### 调试模式

```
$ hexo --debug
```

在终端中显示调试信息并记录到 `debug.log`。当您碰到问题时，可以尝试用调试模式重新执行一次，并 [提交调试信息到 GitHub](https://github.com/hexojs/hexo/issues/new)。

### 简洁模式

```
$ hexo --silent
```

隐藏终端信息。

### 自定义配置文件的路径

```
# 使用 custom.yml 代替默认的 _config.yml
$ hexo server --config custom.yml

# 使用 custom.yml 和 custom2.json，其中 custom2.json 优先级更高
$ hexo generate --config custom.yml,custom2.json,custom3.yml
```

自定义配置文件的路径，指定这个参数后将不再使用默认的 `_config.yml`。
你可以使用一个 YAML 或 JSON 文件的路径，也可以使用逗号分隔（无空格）的多个 YAML 或 JSON 文件的路径。例如：

```
# 使用 custom.yml 代替默认的 _config.yml
$ hexo server --config custom.yml

# 使用 custom.yml, custom2.json 和 custom3.yml，其中 custom3.yml 优先级最高，其次是 custom2.json
$ hexo generate --config custom.yml,custom2.json,custom3.yml
```

当你指定了多个配置文件以后，Hexo 会按顺序将这部分配置文件合并成一个 `_multiconfig.yml`。如果遇到重复的配置，排在后面的文件的配置会覆盖排在前面的文件的配置。这个原则适用于任意数量、任意深度的 YAML 和 JSON 文件。

### 显示草稿

```
$ hexo --draft
```

显示 `source/_drafts` 文件夹中的草稿文章。

### 自定义 CWD

```
$ hexo --cwd /path/to/cwd
```

自定义当前工作目录（Current working directory）的路径。

## 配置

可以在` _config.yml `或 代替配置文件 中修改大部分的配置。

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

# 写作命令

## 概述命令

```
hexo init myBlog
cd myBlog
npm install
hexo new "Have a Try"
hexo g
hexo d
hexo server
```

上述命令行含义是

1. `hexo init myBlog`创建一个新的文件夹myBlog作为Hexo的工作目录
2. `cd myBlog`进入文件夹myBlog
3. `npm install`局部安装hexo
4. `hexo new "Have a Try"`在source文件夹下的_POST文件夹下创建新的文章 md文档
5. `hexo g`将md文档生成静态html文件
6. `hexo d`部署网站
7. `hexo s`将页面渲染到本地服务器上

## 创建新文章或页面

你可以执行下列命令来创建一篇新文章或者新的页面。

```
$ hexo new [layout] <title>
```

您可以在命令中指定文章的布局（layout），默认为 post，可以通过修改` _config.yml `中的 `default_layout `参数来指定默认布局。

### 布局（Layout）

Hexo 有三种默认布局：`post`、`page` 和 `draft`。在创建这三种不同类型的文件时，它们将会被保存到不同的路径；而您自定义的其他布局和 `post` 相同，都将储存到 `source/_posts` 文件夹。

| 布局    | 路径             |
| :------ | :--------------- |
| `post`  | `source/_posts`  |
| `page`  | `source`         |
| `draft` | `source/_drafts` |

> 禁用布局
>
> 如果你不希望一篇文章（post/page）使用主题处理，请在它的 front-matter 中设置 `layout: false`。详情请参考[本节](https://hexo.io/zh-cn/docs/front-matter#布局)。

### 草稿
刚刚提到了 Hexo 的一种特殊布局：draft，这种布局在建立时会被保存到 `source/_drafts` 文件夹，您可通过 `publish` 命令将草稿移动到` source/_posts` 文件夹，该命令的使用方式与 `new `十分类似，您也可在命令中指定` layout `来指定布局。
```
$ hexo publish [layout] <title>
```
草稿默认不会显示在页面中，您可在执行时加上` --draft` 参数，或是在 `_config.yml` 中把 `render_drafts `参数设为` true` 来预览草稿。
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

### 支持的格式

Hexo 支持以任何格式书写文章，只要安装了相应的渲染插件。

例如，Hexo 默认安装了 `hexo-renderer-marked` 和 `hexo-renderer-ejs`，因此你不仅可以用 Markdown 写作，你还可以用 EJS 写作。如果你安装了 `hexo-renderer-pug`，你甚至可以用 Pug 模板语言书写文章。

只需要将文章的扩展名从 `md` 改成 `ejs`，Hexo 就会使用 `hexo-renderer-ejs` 渲染这个文件，其他格式同理。

# Front-matter

Front-matter 是文件最上方以 `---` 分隔的区域，用于指定个别文件的变量，举例来说：

```
    ---
    title: Hello World
    date: 2013/7/13 20:46:25
    ---
```

以下是预先定义的参数，您可在模板中使用这些参数值并加以利用。

| 参数              | 描述                                                         | 默认值                                                       |
| :---------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| `layout`          | 布局                                                         | [`config.default_layout`](https://hexo.io/zh-cn/docs/configuration#文章) |
| `title`           | 标题                                                         | 文章的文件名                                                 |
| `date`            | 建立日期                                                     | 文件建立日期                                                 |
| `updated`         | 更新日期                                                     | 文件更新日期                                                 |
| `comments`        | 开启文章的评论功能                                           | `true`                                                       |
| `tags`            | 标签（不适用于分页）                                         |                                                              |
| `categories`      | 分类（不适用于分页）                                         |                                                              |
| `permalink`       | 覆盖文章的永久链接，永久链接应该以 `/` 或 `.html` 结尾       | `null`                                                       |
| `excerpt`         | 纯文本的页面摘要。使用 [该插件](https://hexo.io/zh-cn/docs/tag-plugins#文章摘要和截断) 来格式化文本 |                                                              |
| `disableNunjucks` | 启用时禁用 Nunjucks 标签 `{{ }}`/`{% %}` 和 [标签插件](https://hexo.io/zh-cn/docs/tag-plugins) 的渲染功能 | false                                                        |
| `lang`            | 设置语言以覆盖 [自动检测](https://hexo.io/zh-cn/docs/internationalization#路径) | 继承自 `_config.yml`                                         |
| `published`       | 文章是否发布                                                 | 对于 `_posts` 下的文章为 `true`，对于 `_draft` 下的文章为 `false` |

## 布局

根据 `_config.yml` 中 [`default_layout`](https://hexo.io/zh-cn/docs/configuration#文章) 的设置，默认布局是 `post` 。当文章中的布局被禁用(`layout: false`)，它将不会使用主题处理。然而，它仍然会被任何可用的渲染引擎渲染：如果一篇文章是用 Markdown 写的，并且安装了 Markdown 渲染引擎（比如默认的 [hexo-renderer-marked](https://github.com/hexojs/hexo-renderer-marked))，它将被渲染成HTML。

除非通过 `disableNunjucks` 设置或 [渲染引擎](https://hexo.io/zh-cn/api/renderer#禁用-Nunjucks-标签) 禁用，否则无论布局如何，[标签插件](https://hexo.io/zh-cn/docs/tag-plugins) 总是被处理。

## 分类和标签

只有文章支持分类和标签，您可以在 Front-matter 中设置。在其他系统中，分类和标签听起来很接近，但是在 Hexo 中两者有着明显的差别：分类具有顺序性和层次性，也就是说 `Foo, Bar` 不等于 `Bar, Foo`；而标签没有顺序和层次。

```
categories:
- Diary
tags:
- PS3
- Games
```

> 分类方法的分歧
>
> 如果您有过使用 WordPress 的经验，就很容易误解 Hexo 的分类方式。WordPress 支持对一篇文章设置多个分类，而且这些分类可以是同级的，也可以是父子分类。但是 Hexo 不支持指定多个同级分类。下面的指定方法：
>
> ```
> categories:
>   - Diary
>   - Life
> ```
>
> 会使分类 `Life` 成为 `Diary` 的子分类，而不是并列分类。因此，有必要为您的文章选择尽可能准确的分类。
>
> 如果你需要为文章添加多个分类，可以尝试以下 list 中的方法。
>
> ```
> categories:
> - [Diary, PlayStation]
> - [Diary, Games]
> - [Life]
> ```
>
> 此时这篇文章同时包括三个分类： `PlayStation` 和 `Games` 分别都是父分类 `Diary` 的子分类，同时 `Life` 是一个没有子分类的分类。

## JSON Front-matter

除了 YAML 外，你也可以使用 JSON 来编写 Front-matter，只要将 `---` 代换成 `;;;` 即可。

```
"title": "Hello World",
"date": "2013/7/13 20:46:25"
;;;
```

# 资源文件夹


对于那些想要更有规律地提供图片和其他资源以及想要将他们的资源分布在各个文章上的人来说，Hexo也提供了更组织化的方式来管理资源。这个稍微有些复杂但是管理资源非常方便的功能可以通过将 config.yml 文件中的 `post_asset_folder `选项设为` true` 来打开。

```
_config.yml
post_asset_folder: true
```

当资源文件管理功能打开后，Hexo将会在你每一次通过` hexo new [layout] <title>` 命令创建新文章时自动创建一个文件夹。这个资源文件夹将会有与这个文章文件一样的名字。将所有与你的文章有关的资源放在这个关联文件夹中之后，你可以通过相对路径来引用它们，这样你就得到了一个更简单而且方便得多的工作流。

# 在Hexo中插入图片的方法

> 见原文[hexo给文章插入图片、进行图片样式控制](https://blog.51cto.com/u_15477117/4919656)

## img路径方法插入图片

markdown是支持html语句的，直接插入就可以使用了。所以该方法用到了HTML的标签，采用img标签相对链接的方式引入图片。

### 优缺点

优点：灵活，可以进行样式控制。

缺点：稍微麻烦了点。

### 适用环境

用于顶部导航选项的页面（如：关于、标签、分类）中引入图片。

因为在HEXO生成静态界面时，同一篇文章会在多处页面生成，例如首页、文章详情页等，而不同页面与图片的相对位置是不一样的，而该方式hexo不会自动处理图片引用，所以使用该方式引用本地图片时必须以“/”开头，表示地址都是基于主目录定位的，不会出现有的界面图片显示错误的情况。

不是“/”开头表相对当前文档位置进行定位。

而顶部导航页只会在一处地方生成，所以不带“/”开头不会出现失效，建议也统一使用“/”，开头。

### 使用方法

在source中新建一个“images”目录用于存放图片，然后再使用“/images/图片名”引用图片。也可以分文章存放图片，会稍微麻烦点。

## `![]()`方式插入图片

`![]()`是markdown的插入图片语句，语法为：

`![图片加载失败的描述](图片链接)`

### 优缺点

优点：插入图片简便。

缺点：不能控制图片样式。

### 适用环境

给普通文章插入图片，且无须样式控制；

给顶部导航选项的页面（如：关于、标签、分类）中插入图片，且无须样式控制。

使用该方法引入本地图片同样需要以“/”，开头定位，否则有的界面将会无法正常显示图片，也可以将引图片转换为Base64字符串，然后再引用Base64字符串，Base64字符串太长，写文章时很影响阅读。

### 使用方法

链接插入图片

插入网络图片比较简单，直接在“图片链接中写入图片的网络链接就好”

示例：

`![玖涯](http://www.nineya.com/android/download/img/logo.png)`

效果如下，已经显示了我们插入的图片。

在source中新建一个“images”目录用于存放图片，将图片放在该目录下，使用“/images/图片名”引用，示例：

`![玖涯](/images/logo.png)`

## Base64方法插入本地图片

使用markdown图片插入语句插入本地图片时可以使用Base64方法，base64方法只需要将图片转换为base64格式，将Base64字符串输入图片路径位置即可。网上可以找到在线图片转Base64的工具。

`![图片加载失败的描述](Base64字符串)`

示例：

`![图片加载失败的描述](data:image/png;base64,iVBORw0KGgoAAA...)`

效果如下，但是强烈不建议使用该方法，因为图片转换成的Base64字符串特别长，影响写作。

## 通过`%%`插入本地图片

### 优缺点

优点：插入较为便捷，图片按文章存储

缺点：不能控制样式，不能在顶部导航选项的页面（如：关于、标签、分类）中插入图片。

### 适用环境

普通文章中插入本地图片,在顶部导航选项的页面中使用该方法，什么都不会显示（不知道是不是我使用的主题的原因），总之是失败了，什么都没显示，在普通文章中可以正常显示。不能用于插入网络图片。

### 使用方法

要使用该方法首先要修改博客的配置文件`_config.yml`,把配置文件里的post_asset_folder:设置为true，表示启动Asset资源文件夹。这时候新建文章就会自动添加一个同名的文件夹，用于存放资源文件。

这时候我们把图片放入对应的文件夹即可，但是我们使用`![描述](图片路径)`插入图片却不能成功，因为只是将图片放入文件夹，hexo生成静态界面时并没有处理该图片，所以运行后就找不到图片了。

所以我们需要使用`<%%>`方法，使用该方法必须将图片放在新建文件时生成的与该文件同名的目录下，然后使用以下命令格式即可。

```
{% asset_img 图片文件名 图片加载失败的描述 %}
```
示例

我文章文件为

`--tupian.md`

图片目录为

`--tupian/logo.png`

插入语句为
```
{% asset_img logo.png 玖涯 %}
```
## 建议使用方式

![1697286761146](../images/1697286761146.png)

## 关于使用hexo-asset-image插件插入图片

在我写这篇文章之前就有大佬做了一个插入图片的开源框架，只需要使用`<%%>`方法引用图片，无论是网络图片还是本地图片，插件都会自动帮助我们将图片下载到source/image目录，然后自动更新图片引用，可以说非常方便。

### 插件的问题

但是该插件目前有一个问题，貌似和不同的操作系统有关，我使用时没有成功插入图片。

解决方法：出现这种问题，删除插件引用，然后换一个版本重新添加插件，不行就多换几个，基本上就可以解决问题了。

该问题大佬可能也已经在最新版本解决了，附上大佬Git项目地址 [hexo-easy-images]([GitHub - boboidream/hexo-easy-images](https://github.com/boboidream/hexo-easy-images))，可以去围观。

### 插件的使用

首先我们添加插件，添加命令如下。

`npm install hexo-asset-image --save`

如果你配置了淘宝的数据源，可以使用以下命令，添加插件时网络会稍微稳定一点：

`cnpm install hexo-asset-image --save`

添加插件之后使用`!()[]`正常引用图片就好了，插件会自动处理。

添加插件后运行可以发现hexo自动处理了我们添加的图片。但是可以看到，插件把我图片的引用链接转换成了`.com//logo.png`，然后我查看目录并没有自动下载图片，这可能和我这个版本有关，多换几个版本就好，或者去围观大佬GitHub，可能会有解决。

## 6.关于hexo-admin插件

这是一个可视化写作文章的插件，同时也可以进行图片上传，但是使用上可能会出现一些问题，所以在这里不详细介绍。

## 7.总结

总体hexo插入图片有多种方式，插入网络图片用`![]()`，插入本地图片用`{% %}`就可以解决基本问题。大佬的插件方式插入图片很简洁，要是有时间大家可以去研究研究。有不清楚的地方欢迎评论留言，看到的我都会回复的。本节到此结束，有什么不足的地方请大家不吝指正。

另外本人找过了网上的教程，没有找到控制图片格式的功能，只在大佬的插件上看到可以统一控制图片大小，貌似是没有这个功能，要是有懂得大佬还望指教。



# 生成器

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

3. 使用`node --version` 指令检查你电脑上的 Node.js 版本，并记下该版本 (例如：`v16.y.z`)
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

## 将 Hexo 部署到 GitLab Pages
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

## 一键部署
Hexo 提供了快速方便的一键部署功能，让您只需一条命令就能将网站部署到服务器上。
```
$ hexo deploy
```
在开始之前，您必须先在 _config.yml 中修改参数，一个正确的部署配置中至少要有 type 参数，例如：
```
deploy:
  type: git
```
您可同时使用多个 deployer，Hexo 会依照顺序执行每个 deployer。
```
deploy:
- type: git
  repo:
- type: heroku
  repo:
```
关于更多的部署插件，请参考 插件 列表。

>缩进
YAML依靠缩进来确定元素间的从属关系。因此，请确保每个deployer的缩进长度相同，并且使用空格缩进。

### Git
1. 安装 hexo-deployer-git。

```
$ npm install hexo-deployer-git --save
```
2. 修改配置。

```
  deploy:
  type: git
  repo: <repository url> #https://bitbucket.org/JohnSmith/johnsmith.bitbucket.io
  branch: [branch]
  message: [message]
```
|参数|	描述|	默认|
|-|-|-|
|repo|	库（Repository）地址||
|branch	|分支名称|	`gh-pages (GitHub) coding-pages (Coding.net) master (others)`|
|message|	自定义提交信息|  |
|token|	可选的令牌值，用于认证 repo。用 $ 作为前缀从而从环境变量中读取令牌||
3. 生成站点文件并推送至远程库。执行 `hexo clean && hexo deploy`。
- 除非你使用令牌或 SSH 密钥认证，否则你会被提示提供目标仓库的用户名和密码。
- hexo-deployer-git 并不会存储你的用户名和密码. 请使用 git-credential-cache 来临时存储它们。
4. 登入 Github/BitBucket/Gitlab，请在库设置（Repository Settings）中将默认分支设置为`_config.yml`配置中的分支名称。稍等片刻，您的站点就会显示在您的Github Pages中。

# 进阶使用

## 创建自定义主题

创建 Hexo 主题非常容易，您只要在 `themes` 文件夹内，新增一个任意名称的文件夹，并修改 `_config.yml` 内的 `theme` 设定，即可切换主题。一个主题可能会有以下的结构：

```
.
├── _config.yml
├── languages
├── layout
├── scripts
└── source
```

### _config.yml

主题的配置文件。和 Hexo 配置文件不同，主题配置文件修改时会自动更新，无需重启 Hexo Server。

### languages

语言文件夹。请参见 [国际化 (i18n)](https://hexo.io/zh-cn/docs/internationalization)。

### layout

布局文件夹。用于存放主题的模板文件，决定了网站内容的呈现方式，Hexo 内建 [Nunjucks](https://mozilla.github.io/nunjucks/) 模板引擎，您可以另外安装插件来获得 [EJS](https://github.com/hexojs/hexo-renderer-ejs) 或 [Pug](https://github.com/hexojs/hexo-renderer-pug) 支持，Hexo 根据模板文件的扩展名来决定所使用的模板引擎，例如：

```
layout.ejs   - 使用 EJS
layout.swig  - 使用 Swig
```

您可参考 [模板](https://hexo.io/zh-cn/docs/templates) 以获得更多信息。

### scripts

脚本文件夹。在启动时，Hexo 会载入此文件夹内的 JavaScript 文件，请参见 [插件](https://hexo.io/zh-cn/docs/plugins) 以获得更多信息。

### source

资源文件夹，除了模板以外的 Asset，例如 CSS、JavaScript 文件等，都应该放在这个文件夹中。文件或文件夹开头名称为 `_`（下划线）或隐藏的文件会被忽略。

如果文件可以被渲染的话，会经过解析然后储存到 `public` 文件夹，否则会直接拷贝到 `public` 文件夹。

### 发布

当您完成主题后，可以考虑将它发布到 [主题列表](https://hexo.io/themes)，让更多人能够使用您的主题。在发布前建议先进行 [主题单元测试](https://github.com/hexojs/hexo-theme-unit-test)，确保每一项功能都能正常使用。发布主题的步骤和 [更新文档](https://hexo.io/zh-cn/docs/contributing.html#更新文档) 非常类似。

1. Fork [hexojs/site](https://github.com/hexojs/site)

2. 把库（repository）复制到电脑上，并安装所依赖的插件。
```
$ git clone https://github.com/<username>/site.git
$ cd site
$ npm install
```
3. 在 `source/_data/themes/` 中创建一个新的 yaml 文件，使用您的主题名称作为文件名。

4. 编辑 `source/_data/themes/<your-theme-name>.yml` 并添加您的主题。例如：
```
   description: A brand new default theme for Hexo.
   link: https://github.com/hexojs/hexo-theme-landscape
   preview: http://hexo.io/hexo-theme-landscape
   tags:
     - official
     - responsive
     - widget
     - two_column
     - one_column
```
5. 在 `source/themes/screenshots` 中添加一张截图（名称与主题相同），图片必须为 800x500 的 PNG 文件。

6. 推送（push）分支。

7. 建立一个新的合并申请（pull request）并描述改动。

## 更换已有主题

更换默认主题，访问[主题列表](https://hexo.io/themes/)，挑选一个自己喜欢的主题。如下图：

![](../images/refefine缩略图.png)

### 安装和使用redefine主题

- [主题GitHub地址]([GitHub - EvanNotFound/hexo-theme-redefine: Simplicity in Speed, Purity in Design: Redefine Your Hexo Journey.](https://github.com/EvanNotFound/hexo-theme-redefine))
- [主题使用教程]([项目介绍 - Redefine Docs (ohevan.com)](https://redefine-docs.ohevan.com/introduction))

#### 安装主题

在 Hexo 根目录执行以下命令安装主题，有两种方式：

- npm

```
npm install hexo-theme-redefine@latest
```

- git

```
git clone https://github.com/EvanNotFound/hexo-theme-redefine.git themes/redefine
```

将主题克隆到 themes 目录下，以下截图就是 clone 之后的结果。

![](../images/2.png)

#### 启用主题

在 Hexo 根目录的 `_config.yml` 文件中，将 `theme` 值修改为 `redefine`。

```
theme: redefine
```

#### 创建主题配置文件

在 Hexo 根目录下创建 `_config.redefine.yml` 文件。

并将[此处(opens in a new tab)](https://github.com/EvanNotFound/hexo-theme-redefine/blob/main/_config.yml)的所有内容复制进去。

本文件会自动覆盖主题的配置项，创建本文件的目的是为了方便你在升级主题时，不会丢失你的配置。

#### VOILA!

现在你可以启动 Hexo，看看效果了。

接下来请先阅读配置注意事项，然后继续配置主题。

### Redefine主题基本配置

配置 Hexo 主题的基本信息，包括标题，描述，作者，图片等。

## Hexo添加分类和标签

添加分类效果

![](../images/88475b8866d348a13b7816e14666dde2.png)

### 创建分类页面

在 Hexo 根目录执行以下命令：

```
hexo new page categories
```

### 导航栏添加分类页面

在 Redefine 主题配置文件 `_config.redefine.yml` 的 `navbar` 配置项里面启用 `categories`。

_config.redefine.yml

```
navbar:  
	categories:    
		Categories: #取名随意        
		icon: fa-solid fa-folder #图标        
		path: /categories/ #链接
```

（放在二级菜单也可以）

### 修改标题（可选）

Categories 分类页默认根据 `title: categories` 来匹配。

如果需要自定义页面的标题，需要在 Front Matter 里面添加 `type: categories`，即可自定义页面标题。

> 标签页面和分类页面同理

## Hexo修改文章永久链接

> 默认的文章访问链路径，应该是这样的：2022/09/16/子文件夹/文章标题，完整链接类似：https://qi-letian.github.io/2022/09/16/Hexo/hello-world。这种默认风格的话，很清楚的展示了文章的写作日期、子文件夹信息等。
> 
> 其实访问路径的配置，跟生成的静态文件挂钩，如果配置成这样的“日期、文件名类型”最终生成静态页面时，也会按照这样的规则生成对应的文件目录，例如：2022/09/16/子文件夹/文章标题/index.html。【这个是题外话，静态文件怎么样分布，其实并不影响】
> 
> 个人来说，不太喜欢这样的风格，一串数字在路径里。比较理想的风格是：类别/文章标题，例如：Hexo/hello-world，为了不跟其他导航界面冲突，再在开头加个pages，pages/Hexo/hello-world.

说到底，就是不喜欢默认风格的文章访问路径的格式。
× https://qi-letian.gitee.io/2022/09/16/Hexo/hello-world/
√ https://qi-letian.gitee.io/pages/Hexo/hello-world/

### 配置项介绍

您可以在 `_config.yml` 配置中调整网站的永久链接或者在每篇文章的 Front-matter 中指定。

#### 变量

除了下列变量外，您还可使用 Front-matter 中的所有属性。

| 变量          | 描述                                                         |
| :------------ | :----------------------------------------------------------- |
| `:year`       | 文章的发表年份（4 位数）                                     |
| `:month`      | 文章的发表月份（2 位数）                                     |
| `:i_month`    | 文章的发表月份（不含前导零）                                 |
| `:day`        | 文章的发表日期 (2 位数)                                      |
| `:i_day`      | 文章的发表日期（不含前导零）                                 |
| `:hour`       | 文章发表时的小时 (2 位数)                                    |
| `:minute`     | 文章发表时的分钟 (2 位数)                                    |
| `:second`     | 文章发表时的秒钟 (2 位数)                                    |
| `:title`      | 文件名称 (相对于 “source/_posts/“ 文件夹)                    |
| `:name`       | 文件名称                                                     |
| `:post_title` | 文章标题                                                     |
| `:id`         | 文章 ID (*清除缓存时不具有持久性*)                           |
| `:category`   | 分类。如果文章没有分类，则是 `default_category` 配置信息。   |
| `:hash`       | 文件名（与 `:title` 相同）和日期的 SHA1 哈希值（12位16进制数） |

您可在 `permalink_defaults` 参数下调整永久链接中各变量的默认值：

```
permalink_defaults:
  lang: en
```

#### 示例

```
source/_posts/hello-world.mdtitle: Hello World
date: 2013-07-14 17:01:34
categories:
- foo
- bar
```

| 参数                            | 结果                        |
| :------------------------------ | :-------------------------- |
| `:year/:month/:day/:title/`     | 2013/07/14/hello-world/     |
| `:year-:month-:day-:title.html` | 2013-07-14-hello-world.html |
| `:category/:title/`             | foo/bar/hello-world/        |
| `:title-:hash/`                 | hello-world-a2c8ac003b43/   |

```
source/_posts/lorem/hello-world.mdtitle: Hello World
date: 2013-07-14 17:01:34
categories:
- foo
- bar
```

| 参数                        | 结果                          |
| :-------------------------- | :---------------------------- |
| `:year/:month/:day/:title/` | 2013/07/14/lorem/hello-world/ |
| `:year/:month/:day/:name/`  | 2013/07/14/hello-world/       |

### 具体配置

#### url

我的是部署到Github上，所以此处配置的就是Github主页的默认地址：https://qi-letian.github.io

####  permalink

- permalink:
  - 文章链接格式，也就是 文章访问链接 的模板：
  - 我的配置是：pages/:category/:title/
  简单说明一下 :带个前缀 pages；类别/文件名。
  
```
# URL
## Set your site url here. For example, if you use GitHub Page, set url as 'https://username.github.io/project'
url: https://qi-letian.gitee.io/
permalink: pages/:category/:abbrlink/
```

这么一波配置，分类为`Hexo`文件名为`d87f7b4f.md`的文章访问链接就如下图所示：

![](../images/1697274417448.png)

### 文档目录具体对应【更直观】

文章都放在` _post`目录下。

因为配置`permalink`时，只用到文件名，所以`_post`下的子目录并不影响最终生成的静态文件的具体分布。

注意文件头的categories项，对应:category变量。

如果地址处配置了该变量，那么写文章时，注意categories设置为**单值**。

> 也就是说，一篇文章只有一个分类，如果想有多个标识，那么可以配置到 tags标签项，为文章添加多个标签。

### 修改永久链接的默认格式

如果你的文章名称是中文的，那么 Hexo 默认生成的永久链接也会有中文，这样不利于 SEO，且 gitment 评论对中文链接也不支持。

在 Hexo 根目录下的 `_config.yml` 文件采用初始设置。这里因为用“年月日”会让文章链接的层次太深，所以我用`pages/category`代替。这样既能够区分文章，也能显示文章分类。

生成的文章链接就是（标题为“我的个人博客”）：

https://[你的网站域名]/pages/category/我的个人博客。

链接中出现中文显然不太好，所以下面给出一种替代中的方法。

**安装插件方法一（推荐）**

在 Hexo 根目录下使用 `git bash` 执行命令：
```
npm install hexo-abbrlink --save
```
在 Hexo 根目录下的` _config.yml` 文件，修改为如下配置：
```
permalink: pages/catrgory/:title/
abbrlink:
  alg: crc32  # 算法：crc16(default) and crc32
  rep: hex    # 进制：dec(default) and hex
permalink_defaults:
```
然后在 `git bash` 按顺序运行如下命令：
```
hexo clean #清除缓存 网页正常情况下可以忽略此条命令
hexo g #生成静态网页
hexo d #开始部署
```
再打开网站的文件就可以看到效果。

效果（其中60762就是随机生成的）

https://qi-letian.gitee.io/pages/Hexo/d87f7b4f/
