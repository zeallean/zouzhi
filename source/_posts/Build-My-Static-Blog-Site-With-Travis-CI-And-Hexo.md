---
layout: post
title: Travis-ci,Hexo与Github三剑合璧打造专属静态博客
date: 2015-09-13 23:56:38
category: [编程]
---

本篇主要针对喜欢写写文字，但又不想受限于千篇一律的博客平台，想寻求一个没有广告，简洁纯净，可以完全按自己的方式来写作的文字爱好者。当然如果有点 geek 范，爱好编程则再好不过了。当然，如果觉得操作过于繁琐难懂，但仍想拥有一个同本站一般的博客，可以文章下面[留言](#comment)、[邮箱](mailto:zeallean5@gmail.com)或者微博[@走之派-zeal](http://weibo.com/crazybd)私信我。很乐意与各位一起探讨，并免费提供帮助（可以的话）。同时也欢迎各位加入Facebook小组-- Free Code Camp Changsha 。大家一起来自由学习编程，与全球的编程爱好者做全球性的公益项目。

## 工具简介

### Hexo

[Hexo][hexo] 是由台湾个人团队基于 Node JS 开发的一个快速、简洁且高效的博客框架。完全开源，源代码托管在 Github 上。安装后，通过其简单的命令就可以在本地快速的搭建起一个个人博客。官网上提供的文档全面且易阅读，非常容易上手。

### Github

[Github][github] 对于经常通过 Google 找轮子的读者应该都比较熟悉它，程序员或多或少都在 Github 上借鉴，搬运，共享过开源代码。应该是全球最火，也是注册人数最多的一个开发者平台。基于强大的分布式版本控制系统 git。以及强大的多人协作工作流。各大互联网公司，也都开始纷纷效仿学习 github 的协作开发模式了。基于 Github的开发工作流，很值得深入学习，相信对于开发团队的流程管理会有很大的帮助（完全从本人的开发经历有感而发）。

好了，上面就是我们搭建静态博客要用到的几个主要工具的简单介绍。对于从来没接触和听说过的朋友，可能有点不知所云。不过不要紧，因为每一个深挖学习都可以写出一个系列来！（那在这里为什么还要写？其实你懂的，为了让文章结构看上去更为严谨。我这就是想装下13）其实他们各自的官网都提供了非常详细的文档说明（如果你英文好，而且会科学上网）

### travis-ci

[Travis-CI][travis] 是一个面向 Github 上的开发者(travis-ci.org 主要针对开源项目)提供的一个符合[敏捷开发模式][1]的[持续化集成][2]Saas 平台。

> 在持续集成中要求将所有工程师对于软件的工作复本，每天整合数次到共用主线（mainline）上。
>
> -- 摘自维基百科

有关 CI 的介绍，请自行 google 。下面也会针对本站点的代码部署做一个简单的CI流程介绍。你会发现 CI 确实为开发者在敏捷开发工作中对于快速提交，测试，及时集成的一系列工作提供了极大的便利。

不过目前貌似 Travis 针对墙内用户已经做了限制。无梯无法正常访问进行注册。这无疑也给很多尝鲜者设置了一道门槛！

**不是我要故意挖坑！提醒：本篇文章的部分操作实现基于一个前提 -- 你会科学上网。关于如何布梯子进行科学上网。可以私信也可以自己** ~~baidu~~ / __google__ `goagent`，`shadowsocks`

## 基础准备

### 帐号注册

1. Github 注册：首先强烈推荐各位成为 Github 上成员（绝对不是广告）。不管是程序员，设计师，文字工作者，whatever··· 通过 Github 的正确使用和对 git 的正确操作，相信对于你的文件管理，代码控制或者是开拓视野都会大受裨益。
注册入口：[github.com][github-signup]，具体流程这里不做过多介绍。

2. Travis-Ci 注册：注册完 Github 帐号，通过科学上网方式访问[travis-ci.org][travis]完成注册。注册会要求绑定 Github 帐号。所以必须先完成上一步的注册。

### 环境安装

1. git 的安装：不多叨叨，直接到 git 的官网[git-scm.com][git]下载与自己的系统相应的版本进行安装。有问题直接留言！使用说明推荐一个 [git-简洁指南][git-guide]

2. node-js 的安装：近年新推出的开发工具。直接官网下载进行安装 [nodejs.org][node]。有问题，来留言！

3. hexo 的安装：hexo 的官网 [hexo.io][hexo] 有介绍，很简单：

	``` bash
	$ npm install hexo-cli -g    # 安装 hexo
	```
	**说明：**由于 node 的包管理工具`npm`  默认采用的源在国内访问受限，so，这里安装可能会卡壳和报错。不过还好 network   是世界的。只需通过 [npm 国内镜像][taobao-npm] 将源换成淘宝npm镜像，问题可轻松解决。
  
	关于 hexo 的操作和介绍，参见[官方文档][hexo-doc]，非常详细，中文支持良好。

4. ruby 的安装：类似 Nodejs 的另一门开发工具。直接官网下载安装[ruby-lang.org][ruby]。它主要作为后面的 travis 工具集的安装提供平台支持。

到这里基础环境已经准备完毕，看上去不简单。但能进行到这里，相信你有足够的兴趣继续下去。好了，休息下。先来听首歌！

---

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=100% height=80 src="http://music.163.com/outchain/player?type=2&id=34248258&auto=0&height=66"></iframe>

---
继续！

下面我想通过一张流程图来简要的介绍下静态博客搭建所用到的各个工具之间的联系！
![work-flow](http://7xl4wx.com1.z0.glb.clouddn.com/static/images/post/work-flow.png)

针对流程图，搭建过程可分为三大部分。

**注意：接下来的操作介绍都建立在上面的环境正常安装的前提下**

## 部署

### 一、本地静态博客搭建

前面已经介绍了，Hexo 是一个用来快速构建本地静态博客的工具。打开终端，通过如下命令
``` bash
$ hexo init "My site"          # 初始化项目，“my site”为自定义项目名
$ cd "My site"
$ npm install                # 安装依赖
$ hexo server                # 生成静态文件, 启动本地web服务器
```
便可以在本地构建一个静态博客。相关的Hexo 的操作，前面已经给出链接：[Hexo官方文档][hexo-doc]。此时创建的博客和内容都只存在与本地。需要想其他博客平台可以通过独立的域名线上访问，我们需要借助 Github。

### 二、将项目托管至 Github

#### 文件托管

首先需要在 Github 上创建一个 repo。
![git-repo](http://7xl4wx.com1.z0.glb.clouddn.com/static/images/post/repo-create.png)

为了避免接下来的操作报错。在创建 repo 时，初始化不要添加 `README` 和 `.gitignore` 文件.
![initialize](http://7xl4wx.com1.z0.glb.clouddn.com/static/images/post/repo-initialize.png)

github 上 repo 新建好以后。回到本机，通过终端，进入刚才通过 hexo  创建好的项目目录，通过 git 进行托管。

``` bash
$ cd mysite  # 进入项目目录
$ git init   # git 初始化
```
将所有文件通过 git 进行本地版本控制，保存至 stage 区
（使用过 SVN 的，这里 Git 在设计上与 SVN 相比多了一个暂存区，它是介于工作区和版本库之间，关于 git 的原理和使用可以查看 [git-scm 上的手册][git-doc]）

``` bash
$ git add .
```
将所有缓存区的文件提交至版本库
``` bash
$ git commit -m "Site init"
```

提交完毕后，回到 github 上来。进入对应的 repo 页面。点击 <i class="icon-clippy"></i> 复制其对应的 repo url 地址

![repo-url](http://7xl4wx.com1.z0.glb.clouddn.com/static/images/post/copy-remote-repository-url.png)

再次回到终端，将刚才复制的 URL 设置为当前项目资源的中心仓库地址。
``` bash
$ git remote add origin “repo url” # 设置中心仓库地址，“repo-url” 为复制的 URL 地址
$ git remote -v  #验证 url 是否可用
```
将同步资源到 Github 中心仓库。
``` bash
$ git push origin master
```
如果之前复制的 URL 为 https 形式
如:`https://github.com/zoorz/hexo-theme-next.git`。
同步时要求你输入 Github 的帐号用户名和密码进行验证。

到这里，流程图中由 Hexo 到 Github 的环节就完成了。如果都能顺利进行的话，接下来的操作会更加顺畅。

---

好了，休息下。看个短片：《Life is Beautiful》

<iframe frameborder="0" width="640" height="498" src="http://v.qq.com/iframe/player.html?vid=n0165gb59wo&tiny=0&auto=0" allowfullscreen></iframe>

这是我个人非常喜欢的一部短片。国外拿奖无数。值得一看和玩味其中所要表达的东西。

---
继续！

**在开始下一个环节的操作之前。这里先来介绍下最终可以通过线上的独立域名：类似[zouzhi.net](zouzhi-net)访问自己的博客需要依赖的工具 Github Pages**

[Github Pages][github-pages] 是 Github 为开发者提供的一个用于快速构建团队或者项目站点主页的工具。通过它你可以快速地搭建起自己的个人主页(User or organization Site) 或者项目主页（Project Site）。Github Pages 默认支持 Jekyll 博客框架（工作原理类似 Hexo，但是 Jekyll 是基于 Ruby开发。相对 Hexo 操作配置较为复杂）。感兴趣的可以在 Pages 的主页或者 Jekyll 官网进行了解。由于这里采用 Hexo 作为博客框架，关于它就不做过多介绍了。


#### 基于 Github Pages 创建线上站点

进入我们之前创建的“my site”项目，为项目创建一个名为“gh-pages”分支。
``` bash
$ git branch -b gh-pages
```
这样就基于当前 master(默认)分支创建了一个新的分支。分支名为"gh-pages"是 Github Pages 上项目主页构建默认采用的分支（具体参照 Pages 的官方介绍）

将分支推送到中心仓库
``` bash
$ git push origin gh-pages
```
此时 gh-pages 是基于 master 分支创建，所包含的是 Hexo 的项目源码。我们最终实现的线上站点 gh-pages 分支所包含的应该是通过 hexo 生成的静态文件。

#### 通过 Hexo-deployer-git 完成线上部署

针对上面 gh-pages 分支。我们需要借助 Deployer 工具完成 hexo 本地生成的项目静态文件的推送。(以下部分可参见:Hexo-doc [Deploy 部分][hexo-deploy])

安装 Hexo-deployer-git
``` bash
$ npm install hexo-deployer-git --save
```
然后在项目目录中找到`_config.yml` 文件，添加如下配置:
``` yaml _config.yml
deploy:
  type: git
  repo: <your repository url>
  branch: gh-pages
```
Option | Description
--- | ---
`repo` | GitHub repository URL
`branch` | Branch name. The deployer will detect branch automatically if you are using GitHub or GitCafe.
`message` | Customize commit message (Default to `Site updated: {% raw %}{{ now('YYYY-MM-DD HH:mm:ss') }}{% endraw %}`)

通过 hexo deploy 将生成的静态文件同步到中心版本库 gh-pages 分支

``` bash
$ hexo generate --deploy
```
推送成功后，可以通过：`http://username.github.io/project`。其中 `project` 为你的项目名

**提醒:** 在同步时可能会出现报错，因为我们在将项目托管到 Github 上的操作时，拷贝的 repo url 为 https。而 Github 做 push 操作时是需要做用户认证的。hexo deploy 要求认证认证方式为 SSH 方式。关于如何将 https 更换为 SSH 认证方式。在接下来的 Travis 部分的操作中，会有相关的介绍。具体参照：[Github Generating SSH keys][ssh-keygen]。

### 三、Travis 配置

由于我们最终需要实现的是类似 Github Pages 默认对Jekyll 的支持一样来适配Hexo，做到写作者只需关心写作，而不需要每次都必须借助 hexo 的指令来完成文章的生成和发布。这时就需要引入 Travis-CI。 

#### 授权

首先登录 Travis-Ci，要求同 Github 帐号进行绑定。完成绑定，通过首页的Account 进入仓库列表，进行仓库同步和授权操作。

![travis account](http://7xl4wx.com1.z0.glb.clouddn.com/static/images/post/travis-account.png)

然后选择对应的项目仓库进行授权。

![toggle-switch](http://7xl4wx.com1.z0.glb.clouddn.com/static/images/post/toggle-switch.png)

其实关于 Travis-ci 将要完成的工作，通过上面的简单介绍和流程图相信有一个大致了解。其实其主要的作用是将原本需要在本地完成的类似 Hexo generate，deploy 的操作，全部移交至 travis-ci 虚拟机的任务来自动处理。我们只需要在项目的目录中添加一个`.travis.yml` 文件，后面在其中配置好我们指定给 travis 要完成的任务就 OK 了。
``` bash
$ touch .travis.yml
```

这里需要注意的是，默认 travis-ci 是不具备 git repo 的写权限的。要实现我们的需求，通过网络找到了这篇博客:http://zespia.tw/blog/2015/01/21/continuous-deployment-to-github-with-travis/。

#### 密钥生成

---
在终端中(Mac/Linux可用,Window 可能通过第三方密钥生成工具或者cygwin实现)生成针对该项目的 SSH 密钥
``` bash
$ ssh-keygen -t rsa -C "your_email@example.com"
```
在生成过程中,passphrase 留空，因为travis-ci 中输入密码无法做到。同时保存目录保存为默认就好(~/.ssh/id_rsa)。这里为了实现今后本地的文章编写完以后同步到 github 版本库时免除每次输入密码的痛苦。针对本地的提交也改为采用 SSH 方式。（其实也可以下载 Github 的图形化客户端工具来实现）。

确保 ssh-agent 能正常工作
``` bash
$ eval "$(ssh-agent) -s"
Agent pid 98304
```

添加生成好的 SSH key 到 ssh-agent
``` bash
$ ssh-add ~/.ssh/id_rsa
```

复制公钥内容到剪切板
``` bash
$ pbcopy < ~/.ssh/id_rsa.pub
```
将公钥配置到 github 上项目的 deploy key 中。

![deploy-key](http://7xl4wx.com1.z0.glb.clouddn.com/static/images/post/deploy-key.png)

测试连接
``` bash
$ ssh -T git@github.com
```
查看提示,是否链接成功。

将本地项目对应的中心仓库 URL 更换为 SSH 格式。
``` bash
$ cd my-site # 进入项目目录
$ git config --local --list # 查看当前中心仓库的 URL, 此时应该为 https 格式

...
remote.origin.url=https://github.com/username/project.git
...

$ git config --local remote.origin.url git@github.com:username/project.git   # 将中心仓库 URL 更换为 SSH 格式 

```

测试同步
``` bash
$ git push
```

修改项目`_config.yml`文件中`deploy`配置段`repo`为 SSH 格式 URL。
``` yaml _config.yml
deploy:
  type: git
  repo: git@github.com:username/project.git
  branch: gh-pages
```

---

以上操作只是为我们以后在文章写好后提交至Github中心仓库时免除了输入用户名和密码的烦恼。涉及到 travis-ci 的自动构建。我们还需要针对密钥进行再次加密。然后在 travis 上进行解密获取同步密钥，用密钥完成 Travis 对 Github 上的项目仓库的写权限。

#### 私钥加密

本地安装 travis-ci。（travis 工具采用 ruby开发。需要本地安装有 ruby 开发环境）
``` bash
$ gem install travis
```

登录 travis
``` bash
$ travis login --auto
```
这样通过 travis 提供的命令工具就可以加密私钥文件，并将加密用的密码存入 travis 服务器。以环境变量形式作为后面解密使用。

加密密钥
``` bash
$ travis encrypt-file ~/.ssh/id_rsa --add
```
这时会生成加密后的密钥文件 id_rsa.enc。同时会将相关的指令插入`.travis.yml`文件中。

推荐在项目目录中创建一个.travis 目录。并将 enc 文件移入其中。同时在.travis 目录中创建一个名为`ssh-config`文件。内容如下
``` yaml ssh-config
Host github.com
	User git
	StrictHostKeyChecking no
	IdentityFile ~/.ssh/id_rsa
	IdentitiesOnly yes
```

#### travis 配置文件

添加上更多针对 hexo 的相关任务配置。最终的`.travis.yml`文件应该为如下所示。具体的细节这里不做过多介绍了。

``` yaml .travis.yml
language: node_js

node_js:
 - "0.12.7"

branches:
  only:
  - master

before_install:
 # Decrypt the private key
 - openssl aes-256-cbc -K $encrypted_d179d3b595b7_key -iv $encrypted_d179d3b595b7_iv -in .travis/id_rsa.enc -out ~/.ssh/id_rsa -d
 # Set the permission of the key
 - chmod 600 ~/.ssh/id_rsa
 # Start SSH agent
 - eval $(ssh-agent)
 # Add the private key to the system
 - ssh-add ~/.ssh/id_rsa
 # Copy SSH config
 - cp .travis/ssh_config ~/.ssh/config
 # Set Git config
 - git config --global user.name "zoorz"
 - git config --global user.email zoechow8@gmail.com

install:
 - npm install hexo-cli -g
 - npm install hexo --save
 - npm install

script:
 - hexo clean 
 - hexo generate 
 - hexo deploy
```

**注意：以上的配置文件中的相关配置内容需要针对各自的项目进行修改。不可直接拷贝。**

完成了上面的一系列操作。终于可以到见证奇迹的时刻了。
```
$ git add .
$ git commit -m "site publish"
```
正常情况下，进行到这里如果能正常同步文件到中心仓库并且调用Travis-ci 实现站点发布的话。对于静态博客整个构建流程图肯定是有了一定了解。此时我们的独立博客只能通过：`http://username.github.io/project` 访问。如果需要为其配以一个独立的域名以显得高端大气上档次，那么我们就还需要再干点活了。

## 独立域名配置

### 注册域名

推荐[万网](http://www.net.cn)（已被阿里收购）进行购买。当然国外的话 [godaddy](https://www.godaddy.com/) 也是不错的选择。具体的域名注册这里就不介绍了。

### 域名解析

注册好域名以后，推荐将域名采用 [DNSPOD](http://www.dnspod.cn) 进行解析。关于如何变更DNS解析。参见：[https://support.dnspod.cn/Kb/showarticle/tsid/40/](https://support.dnspod.cn/Kb/showarticle/tsid/40/)。变更成功以后，我们进入 DNSPOD 对应的域名管理页面。为其添加解析到我们的托管在 Github上的博客 CNAME 记录。

![dnspod-config](http://7xl4wx.com1.z0.glb.clouddn.com/static/images/post/dnspod-cname-config.png)

可能需要5-10分钟解析生效。这期间，我们回到我们本地项目目录。进入项目`source`目录，创建一个名为`CNAME`的文件。内容设置我们的域名。
```txt CNAME
	zouzhi.net 
```

将`CNAME`文件同步到中心仓库。
```bash
$ git add .
$ git commit -m "Config Custom Domain"
$ git push
```

然后网站的构建和发布就交给 travis-ci吧。等待片刻，你就可以通过独立域名：[zouzhi.net](http://zouzhi.net) 访问自己的博客了！

## 优化

### 主题更换

hexo 的默认主题，个人感觉观感体验不是太好，你可以基于默认主题进行自定义修改。这里就能体现出独立静态博客极大的自由度。关于主题的定制和开发作为拓展自行研究。为了更好的体验 Hexo 的便捷性，已经有一系列非常不错的主题可供选用。[Hexo Themes][hexo-theme]。下面以 zouzhi.net 所用主题 [Next][theme-next] 为例进行介绍。

1. 首先通过 git 将主题 clone 到本地的 hexo 项目中

```
	cd my-site # 进入前面通过 hexo 创建的项目目录
	git clone https://github.com/iissnan/hexo-theme-next.git  theme/next

```

2. 修改项目`_config.yml`文件，将主题设置为 `next`

用文本编辑工具打开`_config.yml`。找到 `theme` 配置字段，将 `theme: landscape` 改为 `theme: next`

3. 启动 hexo 服务器，查看是否生效

```
	hexo server
```

访问: [http://0.0.0.0:4000](http://0.0.0.0:4000)

如果主题配置成功，具体的主题细节修改调整，可以参照 Next 主题介绍文档操作。作者非常用心，文档很详细。[Next 使用文档][next-doc]

### 细节自定义

在原有主题的基础上，我为内容区块添加了一个 `texture` 纹理背景，素材来自于[日本传统色][japan-traditional-color]所用纹理背景。感官上使整个站点更有纸张版的阅读质感。同时为首页的各个文章列表项添加了底部border 增强了项与项之间的辨识。此外还有一些其余部分的CSS参数修改。感兴趣的可以直接 fork 项目，自行研究。有意见或建议欢迎一起探讨。

## 文章发布

通过上面的一系列操作。我们就构建起了一个完全属于自己的独立静态博客：采用 Markdown 的友好书写格式，带着 geek 范的高自由度，配以完全独立的域名，永不丢失的内容和版本信息···

文章发布只需要在你的项目 source/_post目录中创建一个`.md` 文件。然后按照 Markdown 的书写格式尽情书写你的文字。完成后同步至 Github。文章就会自动完成线上的发布。
``` bash
$ git add .
$ git commit -m "Article title"
$ git push
```

当然如果是在本机的话。你还可以通过 hexo 命令来生成文章。
```
$ hexo new "your post name"
```
不过，完成上面 travis-ci 环节的接入就是想要摆脱 hexo 的操作。让写作发布可以成为一件随时随地不受设备限制而愉快进行的事。因此这就显得有点多余了。

## 后记

本文所有的操作介绍，部分可能太过粗略，对于完全陌生的读者来说，学习难度可能较高。此外另有部分的操作介绍相对于了解和熟悉工具的读者来说可能又稍显冗繁。其实这篇带点科普性质的实操类文字是我许久前就想写的。只是由于拖延，直到现在才见诸笔端。文字部分难免欠周全，算不上教程。权当是一个学习过程的记录罢了。一来便于日后进行查阅，二来锻炼下自己早已生疏的文字能力。当然，如果能给一直阅读到此处的你带来实际的帮助，那就功不唐捐了。

[travis]: https://travis.org
[hexo]: https://hexo.io
[github]: https://github.com
[github-signup]: https://github.com/join
[git]: https://git-scm.com
[git-guide]: http://www.bootcss.com/p/git-guide/
[node]: https://nodejs.org
[hexo]: https://hexo.io
[taobao-npm]: http://npm.taobao.org/
[ruby]: https://www.ruby-lang.org/zh_cn/
[hexo-doc]: https://hexo.io/zh-cn/docs/
[git-doc]: https://git-scm.com/doc
[github-pages]: https://pages.github.com/
[zouzhi-net]: http://zouzhi.net
[hexo-deploy]: https://hexo.io/zh-cn/docs/deployment.html
[ssh-kegen]: https://help.github.com/articles/generating-ssh-keys/
[hexo-theme]: https://hexo.io/themes/
[theme-next]: https://github.com/iissnan/hexo-theme-next
[next-doc]: http://theme-next.iissnan.com/
[japan-traditional-color]: http://nipponcolors.com/
[1]: https://zh.wikipedia.org/wiki/%E6%95%8F%E6%8D%B7%E5%BC%80%E5%8F%91
[2]: https://zh.wikipedia.org/wiki/%E6%8C%81%E7%BA%8C%E6%95%B4%E5%90%88
