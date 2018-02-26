---
title: hexo-写作须知
date: 2018-01-09 16:59:53
tags:
- hexo
categories:
- [hexo, 写作]
---

## 自定义配置文件

```
$ hexo --config custom.yml
```

自定义配置文件的路径，执行后将采用custom.yml 中的配置，而不再使用 _config.yml。

主题配置最佳实现

1. 要求使用hexo3版本或以上。
2. 在站点目录中source/_data 文件夹下创建名为next.yml 的文件。(自行创建_data文件夹，如果它不存在的话。)
3. 将站点目录和主题目录下config.yml 的内容复制到next.ynl 文件中去。
4. 使用参数--config source/_data/next.yml 来启动、生成或部署网站，举个栗子：hexo d -g --config source/_data/next.yml 。

<!--more-->

## 资源文件夹

对于那些想要更有规律地提供图片和其他资源以及想要将他们的资源分布在各个文章上的人来说，Hexo也提供了更组织化的方式来管理资源。这个稍微有些复杂但是管理资源非常方便的功能可以通过将 config.yml文件中的 post_asset_folder 选项设为 true 来打开。

    _config.yml
    post_asset_folder: true

当资源文件管理功能打开后，Hexo将会在你每一次通过 hexo new [layout] <title> 命令创建新文章时自动创建一个文件夹。这个资源文件夹将会有与这个 markdown 文件一样的名字。将所有与你的文章有关的资源放在这个关联文件夹中之后，你可以通过相对路径来引用它们，这样你就得到了一个更简单而且方便得多的工作流。

## 草稿

**发表草稿**

刚刚提到了 Hexo 的一种特殊布局：draft，这种布局在建立时会被保存到 source/_drafts 文件夹，您可通过 publish 命令将草稿移动到 source/_posts 文件夹，该命令的使用方式与 new 十分类似，您也可在命令中指定 layout 来指定布局。以上为标准操作，实际上直接将文件Ctrl+x 剪切到发表的文件夹下(source/_post )也可以达到发表效果，只是缺少对应布局效果。

    $ hexo publish [layout] <title>

**显示草稿**

    $ hexo --draft

显示 source/_drafts 文件夹中的草稿文章。

## Front-Matter

category 层级分类

tag 同级分类

如果你不想你的文章被处理，你可以将 Front-Matter 中的layout: 设为 false 。

Please use <!-- more -->  in the post to control excerpt accurately.

## 标签插件

标签插件和 Front-matter 中的标签不同，它们是用于在文章中快速插入特定内容的插件。

### 引言

在文章中插入引言，可包含作者、来源和标题。

别号： quote

    {% blockquote [author[, source]] [link] [source_link_title] %}
    content
    {% endblockquote %}

**引用网络上的文章**

    {% blockquote Seth Godin http://sethgodin.typepad.com/seths_blog/2009/07/welcome-to-island-marketing.html Welcome to Island Marketing %}
    Every interaction is both precious and an opportunity to delight.
    {% endblockquote %}

Every interaction is both precious and an opportunity to delight.

Seth GodinWelcome to Island Marketing

### 文本居中引用

    <!-- HTML方式: 直接在 Markdown 文件中编写 HTML 来调用 -->
    <!-- 其中 class="blockquote-center" 是必须的 -->
    <blockquote class="blockquote-center">blah blah blah</blockquote>
    
    <!-- 标签 方式，要求版本在0.4.5或以上 -->
    {% centerquote %}blah blah blah{% endcenterquote %}
    
    <!-- 标签别名 -->
    {% cq %} blah blah blah {% endcq %}

**效果示例：** 

{% cq %} 

...

逢人且说三分话，未可全抛一片心。

有意栽花花不发，无心插柳柳成荫。

画虎画皮难画骨，知人知面不知心。

...

 {% endcq %}

### Gist

在文章中嵌入 Gist

    {% gist gist_id [filename] %}

效果示例： 

{% gist 78136dbf532878db40c59b60214cf0f4 gistfile1.txt %}
