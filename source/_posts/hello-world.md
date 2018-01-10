---
title: Hello World
date: 2017/10/16 20:33:25
---
Welcome to [Hexo](https://hexo.io/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).

## Quick Start

### Create a new post

``` bash
$ hexo new "My New Post"
```

<!--more-->

More info: [Writing](https://hexo.io/docs/writing.html)

### Run server

``` bash
$ hexo server
```

More info: [Server](https://hexo.io/docs/server.html)

### Generate static files

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### Deploy to remote sites

``` bash
$ hexo deploy
```

More info: [Deployment](https://hexo.io/docs/deployment.html)

## 修改备注

### 修改文章底部标签(#)

修改模板`/themes/next/layout/_macro/post.swig`，搜索 `rel="tag">#`，将 # 换成`<i class="fa fa-tag"></i>` 

### 背景透明

博客根目录 `themes\next\source\css\_schemes\Pisces\_layout.styl`这个文件的 
第65行`background:`删除掉

**按钮背景**

博客根目录 `themes\next\source\css\_common\components\post\post-button.styl` 第七行修改成`background: transparent;`

**站点概况背景**

博客根目录 `themes\next\source\css\_schemes\Pisces\_sidebar.styl` 
18行删除

**菜单栏背景**

`next\source\css\_schemes\Pisces\_layout.styl` 文件里`.header-inner` 这个选择器下的`background` 就是背景色

### 星空背景

// 页面背景
```css
@media screen and (min-width:1200px) {
    body {
    background-image: url(/images/background.jpg);
    background-repeat: no-repeat;
    background-attachment: fixed;
    background-position: 50% 50%; 
    background-size: cover;
    }
    #footer a {
        color:#eee;
    }
}
```
### 添加tag-cloud

找到文件 `next/layout/_macro/sidebar.swig`, 然后添加如下内容。

```javascript
{% if site.tags.length > 1 %}
<script type="text/javascript" charset="utf-8" src="/js/tagcloud.js"></script>
<script type="text/javascript" charset="utf-8" src="/js/tagcanvas.js"></script>
<div class="widget-wrap">
    <h3 class="widget-title">Tag Cloud</h3>
    <div id="myCanvasContainer" class="widget tagcloud">
        <canvas width="250" height="250" id="resCanvas" style="width=100%">
            {{ list_tags() }}
        </canvas>
    </div>
</div>
{% endif %}
```

### 添加DaoVoice

需要注册DaoVoice的账号，注意注册后获取到的app_id，使用脚本需要用到

`themes\next-reloaded\layout\_partials\head\custom-head.swig` ，写下如下代码

```javascript
{% if theme.daovoice %}
  <script>
  (function(i,s,o,g,r,a,m){i["DaoVoiceObject"]=r;i[r]=i[r]||function(){(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;a.charset="utf-8";m.parentNode.insertBefore(a,m)})(window,document,"script",('https:' == document.location.protocol ? 'https:' : 'http:') + "//widget.daovoice.io/widget/0f81ff2f.js","daovoice")
  daovoice('init', {
      app_id: "{{theme.daovoice_app_id}}"
    });
  daovoice('update');
  </script>
{% endif %}
```

