---
title: hexo 使用手册
tags:
---
## 简单上手

**要求：** 安装了node.js和Git 

```shell
npm install hexo-cli -g
hexo init blog #在blog文件夹(若没有该文件夹则会自动创建)下面克隆hexo需要的启动文件
cd blog
npm install #安装package.json中的依赖
```

敲完上述指令，hexo的雏形就出来了
![hexo](/images/hexo site.png)
<!--more-->

**tips:** 

```shell
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@^1.0.0 (node_modules\chokidar\node_modules\fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.1.2: wanted {"os":"darwin","arch":"any"} (current: {"os":"win32","arch":"x64"})
```

当你在安装的时候看到这样的提示信息，不要忧伤，不要心急。这很正常！这是因为一个叫`fsevents` 的依赖它只支持`darwim` 操作系统，也就是苹果系统喽。

## 站点配置

配置站点之前，首先简单介绍一下目录结构

| 文件名          | 说明                        |
| ------------ | ------------------------- |
| _config.yml  | 站点配置文件                    |
| package.json | 安装依赖文件                    |
| scaffolds    | 模板文件夹。hexo新建文章时所用模板存放的地方。 |
| scripts      | 脚本文件夹。存放在此的js文件将被自动执行。    |
| source       | 资源文件夹。                    |
| themes       | 主题文件夹                     |

一般配置站点我们主要是修改`_config.yml` 文件，比如:

```shell
# Site
title: Hexo	   
subtitle: 
description: 
author: XXXX XXX
language: zh-Hans
timezone:
```

> 其中，`description`主要用于SEO，告诉搜索引擎一个关于您站点的简单描述，通常建议在其中包含您网站的关键词。`author`参数用于主题显示文章的作者。

`timezone` 默认是使用我们电脑的时区，一般不需要填。`language` 默认英文，简体中文是填`zh-Hans` 。其它部分，按个人喜好填写就行了。

然后修改下网址链接：

```shell
# URL
## 如果您的网站存放在子目录中，例如 http://yoursite.com/blog，则请将您的 url 设为 http://yoursite.com/blog 并把 root 设为 /blog/。
url: http://yoursite.com
root: /
permalink: :year/:month/:day/:title/
permalink_defaults:
```

大多数情况下填个自己的网址就好了，在这里我习惯将站点的链接格式修改为`permalink: :year/:month/:title/` 缩短链接地址的长度。

```shell
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
#theme: landscape
theme: next #这里采用一个大众主题next，热门主题往往能省下不少时间

# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git 
  repo: git@github.com:<username>/<username>.github.io.git
  branch: master
  message: update hexo
  name: [git user]
  email: [git email]
```

设定完主题和部署方式，剩下的就可以根据自己选择的主题来个性定制了。如果想更深入配置站点的话，参考[官方文档](https://hexo.io/docs/configuration.html) 。

启用next主题，需要在终端窗口进行安装，指令如下

```shell
$ cd blog
$ git clone https://github.com/iissnan/hexo-theme-next themes/next
```

启用git部署之前记得安装`npm install hexo-deployer-git --save` 

### GitHub pages



### 写作

category 层级分类

tag 同级分类

在 `Front-matter` 中设置 layout: false

### 多终端同步

**github配置** 

```shell
初始化本地仓库： git init

添加本地所有文件到仓库：git add -A

添加commit：git commit -m "blog源文件"

添加本地仓库分支hexo：git branch hexo

添加远程仓库：git remote add origin git@github.com:yourname/yourname.github.io.git

将本地仓库的源文件分支hexo强制推送到远程仓库hexo分支：git push origin hexo -f 

注意这里有个巨大的坑！！！如果你用的是第三方的主题theme，是使用git clone下来的话，要把主题文件夹下面把.git文件夹删除掉，不然主题无法push到远程仓库，导致你发布的博客是一片空白
```

**其它终端配置** 

```shell
git clone -b hexo git@github.com:yourname/yourname.github.io.git  //将Github中hexo分支clone到本地

cd  yourname.github.io  //切换到刚刚clone的文件夹内

npm install    //注意，这里一定要切换到刚刚clone的文件夹内执行，安装必要的所需组件，不用再init

hexo new post "new blog name"   //新建一个.md文件，并编辑完成自己的博客内容

git add source  //经测试每次只要更新sorcerer中的文件到Github中即可，因为只是新建了一篇新博客

git commit -m "XX"

git push origin hexo  //更新分支

hexo d -g   //push更新完分支之后将自己写的博客对接到自己搭的博客网站上，同时同步了Github中的master
```

**终端同步** 

```shell
git pull origin hexo  //先pull完成本地与远端的融合

hexo new post " new blog name"

git add source

git commit -m "XX"

git push origin hexo

hexo d -g
```

## 主题配置

> 在 Hexo 中有两份主要的配置文件，其名称都是 `_config.yml`。 其中，一份位于站点根目录下，主要包含 Hexo 本身的配置；另一份位于主题目录下，这份配置由主题作者提供，主要用于配置主题相关的选项。
>
> 为了描述方便，在以下说明中，将前者称为**站点配置文件** ， 后者称为**主题配置文件** 。

所有我们先`cd blog/theme/next/` 然后在主题目录下用你熟悉的编辑器修改配置文件`_config.yml` 。

### 选择主题类型

打开文件后我们搜索`Scheme Setting` ，这里有4行配置，默认的选项是Muse。我觉得Gemini比较合适，便注释掉了Muse，去掉Gemini前的#，这样便选好了自己喜欢的主题类型。

```shell
# Schemes
#scheme: Muse
#scheme: Mist
#scheme: Pisces
scheme: Gemini
```

下面4个是原作者文档中提供的各个主题参考示例：

-  Muse scheme: [XiaMo](https://notes.wanghao.work/) | [OAwan](https://oawan.me/) | [Hui Wang](http://hui-wang.info/)
-  Mist scheme: [Jeff](https://blog.zzbd.org/) | [uchuhimo](http://uchuhimo.me/) | [xirong](http://www.ixirong.com/)
-  Pisces scheme: [Vi](http://notes.iissnan.com/) | [Acris](https://blog.mrx.one/) | [Rainy](https://rainylog.com/)
-  Gemini scheme: [Ivan.Nginx](https://almostover.ru/) | [Alynx](http://sh.alynx.xyz/) | [Raincal](https://raincal.top/)

### 菜单设置

主题作者的注释已经写的很清楚了，基本上我们可以从注释中了解的差不多了。我，我就做下笔记。

```shell
menu:
  home: / || home
  about: /about/ || user
  tags: /tags/ || tags
  categories: /categories/ || th
  archives: /archives/ || archive
  #schedule: /schedule/ || calendar
  #sitemap: /sitemap.xml || sitemap
  #commonweal: /404/ || heartbeat

# Enable/Disable menu icons.
menu_icons:
  enable: true
```

>用法: `Key: /link/ || icon`
>
>**Key** 是菜单项，区分大小写。以简体中文为例，菜单项的名称可以在主题目录下languages/zh-Hans.yml中修改和添加。
>
>**link** 是菜单项链接的内容，若你的站点运行在子目录中，请将链接前缀的 / 去掉(例：/archives -> archives).
>
>**icon** 是菜单项显示的图标，通过[Font Awesome](http://fontawesome.io/icons/) 的图标名字来启用，如果不设置或无效的设置便会自动加载一个问号图标。

### 侧栏设置

#### 社交链接

```shell
# Social Links.
social:
  GitHub: https://github.com/yourname || github
  微博: http://weibo.com/your-user-name || weibo

social_icons:
  enable: true
  icons_only: false #是否只展示图标
  transition: false #过渡属性？

#links_layout: block #每个一行
links_layout: inline #不换行
```

`# Blog rolls` 中是友情链接的设置，这里感觉没什么好说的。

#### 头像设置

```shell
# Sidebar Avatar
# in theme directory(source/images): /images/avatar.gif
# in site  directory(source/uploads): /uploads/avatar.gif
avatar: /images/avatar.gif
```

头像图片放在主题目录下 source/images/ ，去掉`avatar: /images/avatar.gif` 的注释并将avatar.gif替换为你使用头像的图片名。

也可以放在站点下新建一个uploads文件夹或使用头像链接地址。但是，嫌弃，麻烦。

#### 目录设置

```shell
# Table Of Contents in the Sidebar
toc:
  enable: true

  # Automatically add list number to toc.
  number: true

  # If true, all words will placed on next lines if header width longer then sidebar width.
  wrap: false

# Creative Commons 4.0 International License.
# http://creativecommons.org/
# Available: by | by-nc | by-nc-nd | by-nc-sa | by-nd | by-sa | zero
creative_commons: by-nc-sa
#creative_commons:
```

进入文章后，侧栏展示目录。设置了自动添加目录序号，目录名超出部分隐藏。基本上不需要改动。主要是装X，取消了`creative_commons`  的注释，也就是加入了知识共享。

哪有什么知识共享，都是**划重点，做笔记** 。

#### 侧栏属性

```shell
  # Sidebar offset from top menubar in pixels (only for Pisces | Gemini).
  offset: 12

  # Back to top in sidebar (only for Pisces | Gemini).
  b2t: true

  # Scroll percent label in b2t button.
  scrollpercent: true

  # Enable sidebar on narrow view (only for Muse | Mist).
  onmobile: false
```

侧栏的位置(position)和展示(display)效果的默认设置已经很合适了。侧栏和菜单栏之间间距为12像素，看上去也很舒服，都没必要改。

只是启用了`b2t` ，右下角的**回到顶部** 在阅读的时候感觉没有侧栏的回到顶部友好。

目录的百分比标签(scrollpercent)纯粹是为了好看。。。

### 站点图标设置

```shell
favicon:
  small: /images/favicon-16x16-next.png
  medium: /images/favicon-32x32-next.png
  apple_touch_icon: /images/apple-touch-icon-next.png
  safari_pinned_tab: /images/logo.svg
  #android_manifest: /images/manifest.json
  #ms_browserconfig: /images/browserconfig.xml
```

主题作者提供了一个很棒的网站https://realfavicongenerator.net，可以检测站点的图标还可以生成站点的图标，其实默认的设置已经让我很满足了，不想再花时间自己找图片。。。追求个性可以从提供的网站生成好站点图标，然后放在主题目录的images文件夹内。当然放在站点目录下的images文件夹中也可以，但是记得移除路径中的/images/前缀。

**站点页脚设置** 一般就是设置个站点时间，默认会采取当前年份，所有这里不大需要怎么配置。

rss和seo的设置还没怎么研究过

### 发表文章设置

在`Post Settings` 里可以设置阅读全文、首页文章标签、文章计数、微信订阅、打赏和许可声明等。

推荐在文章中手动输入`<!--more-->`  来摘录首页展示的文章内容。这里我只设置了一个文章计数，做笔记做的丰不丰富，心里还是得有点B number的。

```shell
post_wordcount:
  item_text: true
  wordcount: true #字数统计
  min2read: true #阅读时长
  totalcount: true #Site words total count
  separated_meta: true 
```

文章计数各个选项的说明文字都可以在language目录下找到配置文件配，例：languages/zh-Hans.yml

### 第三方服务

在多方评论都挂掉，`Hypercomments` 要翻墙的情况下，这里出现了`Gitment` ，fxxking awesome！！！

```shell
# Gitment
# Introduction: https://imsun.net/posts/gitment-introduction/
gitment:
  enable: false
  mint: true # RECOMMEND, A mint on Gitment, to support count, language and proxy_gateway
  count: true # Show comments count in post meta area
  lazy: false # Comments lazy loading with a button
  cleanly: false # Hide 'Powered by ...' on footer, and more
  language: # Force language, or auto switch by theme
  github_user: # MUST HAVE, Your Github ID
  github_repo: # MUST HAVE, The repo you use to store Gitment comments
  client_id:   # MUST HAVE, Github client id for the Gitment
  client_secret: # EITHER this or proxy_gateway, Github access secret token for the Gitment
  proxy_gateway: # Address of api proxy, See: https://github.com/aimingoo/intersect
  redirect_protocol: # Protocol of redirect_uri with force_redirect_protocol when mint enabled
```

$ npm install --save gitment

https://imsun.net/posts/gitment-introduction/

分享

```shell
# NeedMoreShare2
# This plugin is a pure javascript sharing lib which is useful in China.
# See: https://github.com/revir/need-more-share2
# Also see: https://github.com/DzmVasileusky/needShareButton
# iconStyle: default | box
# boxForm: horizontal 水平| vertical 垂直
# position: top / middle / bottom + Left / Center / Right
# networks: Weibo,Wechat,Douban,QQZone,Twitter,Linkedin,Mailto,Reddit,
#           Delicious,StumbleUpon,Pinterest,Facebook,GooglePlus,Slashdot,
#           Technorati,Posterous,Tumblr,GoogleBookmarks,Newsvine,
#           Evernote,Friendfeed,Vkontakte,Odnoklassniki,Mailru
needmoreshare2:
  enable: false
  postbottom: 
    enable: false
    options:
      iconStyle: box
      boxForm: horizontal
      position: bottomCenter
      networks: Weibo,Wechat,Douban,QQZone,Twitter,Facebook
  float: 
    enable: false
    options:
      iconStyle: box
      boxForm: horizontal
      position: middleRight
      networks: Weibo,Wechat,Douban,QQZone,Twitter,Facebook
```

busuanzi统计

```shell
# Show PV/UV of the website/page with busuanzi.
# Get more information on http://ibruce.info/2015/04/04/busuanzi/
busuanzi_count:
  # count values only if the other configs are false
  enable: false
  # custom uv span for the whole site
  site_uv: true
  site_uv_header: <i class="fa fa-user"></i>
  site_uv_footer:
  # custom pv span for the whole site
  site_pv: true
  site_pv_header: <i class="fa fa-eye"></i>
  site_pv_footer:
  # custom pv span for one page only
  page_pv: true
  page_pv_header: <i class="fa fa-file-o"></i>
  page_pv_footer:
```

本地搜索

```shell
# Local search
# Dependencies: https://github.com/flashlab/hexo-generator-search
local_search:
  enable: false
  # if auto, trigger search by changing input
  # if manual, trigger search by pressing enter key or search button
  trigger: auto
  # show top n results per article, show all results by setting to -1
  top_n_per_article: 1
```

$ npm install hexo-generator-searchdb --save

站点配置

search:
  path: search.xml
  field: post
  format: html
  limit: 10000

### 站点背景设置

```shell
# Progress bar in the top during page loading. #进度条
pace: false
# Themes list:
#pace-theme-big-counter
#pace-theme-bounce
#pace-theme-barber-shop
#pace-theme-center-atom *
#pace-theme-center-circle
#pace-theme-center-radar
#pace-theme-center-simple
#pace-theme-corner-indicator
#pace-theme-fill-left
#pace-theme-flash *
#pace-theme-loading-bar *
#pace-theme-mac-osx
#pace-theme-minimal
# For example
# pace_theme: pace-theme-center-simple
pace_theme: pace-theme-minimal

# Canvas-nest
canvas_nest: false #鸟巢

# three_waves
three_waves: false #波纹

# canvas_lines
canvas_lines: #线路

# canvas_sphere
canvas_sphere: false #球

# Only fit scheme Pisces
# Canvas-ribbon
canvas_ribbon: false
```

动画设置

```shell
motion:
  enable: true
  async: false
  transition:
    # Transition variants:
    # fadeIn | fadeOut | flipXIn | flipXOut | flipYIn | flipYOut | flipBounceXIn | flipBounceXOut | flipBounceYIn | flipBounceYOut
    # swoopIn | swoopOut | whirlIn | whirlOut | shrinkIn | shrinkOut | expandIn | expandOut
    # bounceIn | bounceOut | bounceUpIn | bounceUpOut | bounceDownIn | bounceDownOut | bounceLeftIn | bounceLeftOut | bounceRightIn | bounceRightOut
    # slideUpIn | slideUpOut | slideDownIn | slideDownOut | slideLeftIn | slideLeftOut | slideRightIn | slideRightOut
    # slideUpBigIn | slideUpBigOut | slideDownBigIn | slideDownBigOut | slideLeftBigIn | slideLeftBigOut | slideRightBigIn | slideRightBigOut
    # perspectiveUpIn | perspectiveUpOut | perspectiveDownIn | perspectiveDownOut | perspectiveLeftIn | perspectiveLeftOut | perspectiveRightIn | perspectiveRightOut
    post_block: flipXIn #文章
    post_header: slideDownIn #文章标题
    post_body: slideDownIn #文章内容
    coll_header: slideLeftIn
    # Only for Pisces | Gemini.
    sidebar: slideUpIn
```

TODO:

启用资源文件夹来存放文章需要使用的图片等，markdown的引用可以将图片放在source/images下

注：启用的资源文件不要含有空格，因为通过`标签插件` 引用的时候是根据空格来做判断的，且此时直接输入文件名即可不用再加文件路径

保存图片，大图建议使用.jpg格式，小图建议使用.png格式

启用数据文件夹来试验next主题配置功能

研究标签插件给写文章带来的便利

研究去掉文章中的一些设置 比如说权限声明

一般配置站点信息已经第三方服务，需要清缓存

查看github账户信息

https://api.github.com/users/7ummy

