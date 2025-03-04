---
title: Hexo Next优化之路
tags:
  - Hexo
  - Next
categories: 
  - Hexo
date: 2020-03-08 22:27:48
---

# Next7.7.1

## 添加页面载条

1. 打开 `\themes\next\_config.yml`
2. 搜索 **pace:** ，设置为 true，**theme** 为 minimal
3. 下载依赖资源，[点击查看其他加载样式](https://github.hubspot.com/pace/docs/welcome/)

```
$ cd <blog-folder>/themes/next
$ git clone https://github.com/theme-next/theme-next-pace source/lib/pace
```

<!--more-->

## 侧边栏阅读进度 + Top

1. 打开 `\themes\next\_config.yml`
2. 搜索 **back2top** ，如下设置

```
back2top:
  enable: true
  # 回页面顶部
  sidebar: true
  # 显示阅读百分比
  scrollpercent: true
```

## 顶部文章读进度条

1. 打开 `\themes\next\_config.yml`
2. 搜索 **reading_progress:** ，进行如下配置

```
reading_progress:
  # 是否开启
  enable: true
  # 顶部 top，顶部 bottom
  position: top
  # 进度条颜色
  color: "#37c6c0"
  # 进度条高度
  height: 3px
```

## 文章结束标志

1. 在 `\source` 目录下，新建 `_data` 文件夹

2. 进入 `_data` 文件夹，创建文件 `post-body-end.swig`

3. 编辑文件，添加如下内容
   
   ```
   <div>
       {% if not is_index %}
           <div style="text-align:center;color: #ccc;font-size:14px;">
           ------------------------------<em>THE END. </em><!--<i class="fa fa-paw"></i>-->------------------------------
           </div>
       {% endif %}
   </div>
   ```

4. 打开 `\themes\next\_config.yml`

5. 搜索 **custom_file_path** ，将如下内容取消注释
   
   ```
   postBodyEnd: source/_data/post-body-end.swig
   ```

## 文章底部标签样式优化

1. 打开 `\themes\next\_config.yml`

2. 搜索 **creative_commons:** ，进行如下配置
   
   ```
   creative_commons:
     license: by-nc-sa
     sidebar: true
     post: true
   ```

## 修改文章内链接文本样式

1. 打开文件 `themes/next/source/css/_common/components/post/post.styl`

2. 在文件尾添加如下样式代码
   
   ```
   .post-body p a {
       color: #007ab2;
       border-bottom: none;
       border-bottom: 1px solid #007ab2;
       &:hover {
       color: #ff4f79;
       border-bottom: none;
       border-bottom: 1px solid #004f79;
   }}
   ```

## 修改底部年份和名称中间的图标

1. 打开 `\themes\next\_config.yml`

2. 搜索 **footer** ，设置如下
   
   ```
   footer:
     icon:
       # 图标名称
       name: user
       # 是否开启动画效果
       animated: false
       # 图标颜色
       color: "#808080"
   ```
   
   [点击查看更多图标](https://fontawesome.com/v4.7.0/icons/)

## 显示总访问量

1. 打开 `\themes\next\_config.yml`

2. 搜索 **busuanzi_count** ，设置如下
   
   ```
   busuanzi_count:
     enable: true
     # 总访问人数
     total_visitors: true
     total_visitors_icon: user
     # 总访问量
     total_views: true
     total_views_icon: eye
     # 主题访问量
     post_views: true
     post_views_icon: eye
   ```

## 开启 SEO

1. 打开 `\themes\next\_config.yml`
2. 搜索 **seo:**
   将其设置为`true`

## 添加站点地图

### 安装插件

安装插件来生成 sitemap 文件，传统的 sitemap。

``npm install hexo-generator-sitemap --save``

### 修改配置文件

1. 打开 `\_config.yml`

2. 添加如下信息
   
   ```
   sitemap: 
     path: sitemap.xml
   ```

安装完成后执行 `hexo clean & hexo g` 即会在站点 public 目录下生成 `sitemap.xml` 和 `baidusitemap.xml`。

### 添加蜘蛛协议 robots

1. \source 文件夹下新建 robots.txt 文件

2. 文件内容如下
   
   ```
   User-agent: *
   Allow: /
   Allow: /archives/
   Allow: /categories/
   Allow: /tags/ 
   Allow: /resources/ 
   Disallow: /vendors/
   Disallow: /js/
   Disallow: /css/
   Disallow: /fonts/
   Disallow: /vendors/
   Disallow: /fancybox/
   
   Sitemap: https://你的域名/sitemap.xml
   ```

> Allow 字段的值即为允许搜索引擎爬取的内容

### 为外链添加 nofollow 标签

这个还没搞懂怎么回事 ，待更

### 文章优化

#### 修改文章访问路径

默认的链接太过冗长，不利于seo，我们需要修改链接样式

1. 打开 `\_config.yml`
2. 将 **permalink** 修改为如下内容

``permalink: posts/:abbrlink/ #:year/:month/:day/:title/``

## Mathjax

https://blog.csdn.net/wgshun616/article/details/81019687

参考：

https://blog.csdn.net/weixin_41024483/article/details/104801164?%3E

------

# **以下不是Next7.7.1版本的设置**

## 自定义友链页面

Next默认的友链时在主题配置文件中links下面，链接变多后，侧栏页面的排版很不美观，这时候我们可以给友链新增一个单独的页面。

### 新增links页面

```bash
hexo new page links
```

然后再博客根目录/source 下会生成一个links文件夹，打开其中的index.md, 在其头部加上type: "links"

###配置menu
主题配置文件中menu下添加

```
Links: /links/|| link
```

在/themes/next/languages/zh-Hans.yml文件中menu下增加中文描述

```
links: 友链
```

##文章底部标签显示的优化
修改/themes/next/layout/_macro/post.swig，搜索 rel="tag">#，将 # 换成 

```
<i class="fa fa-tag"></i>
```

##Hexo-Next搭建个人博客（代码块复制功能）
为了提高博客代码块的用户体验，仅仅代码高亮还不行，最好还能一键复制代码。故此文将讲述Hexo NexT主题博客的代码块复制功能配置。

###下载 clipboard.js
三方插件 clipboardjs ，相关介绍和兼容性我就不赘述了，去它[主页](https://clipboardjs.com/)或[github](https://github.com/zenorocha/clipboard.js)上看。
下载地址：

[clipboard.js](https://raw.githubusercontent.com/zenorocha/clipboard.js/master/dist/clipboard.js)
[clipboard.min.js](https://raw.githubusercontent.com/zenorocha/clipboard.js/master/dist/clipboard.min.js) 推荐
保存文件clipboard.js / clipboard.min.js ，目录如下：
.\themes\next\source\js\src

###clipboardjs 使用
也是在.\themes\next\source\js\src目录下，创建clipboard-use.js，文件内容如下：

```
  /*页面载入完成后，创建复制按钮*/
  !function (e, t, a) { 
    /* code */
    var initCopyCode = function(){
      var copyHtml = '';
      copyHtml += '<button class="btn-copy" data-clipboard-snippet="">';
      //fa fa-globe可以去字体库替换自己想要的图标
copyHtml += '  <i class="fa fa-clipboard"></i><span>copy</span>';
      copyHtml += '</button>';
      $(".highlight .code pre").before(copyHtml);
      new ClipboardJS('.btn-copy', {
          target: function(trigger) {
              return trigger.nextElementSibling;
          }
      });
    }
    initCopyCode();
  }(window, document);
```

在.\themes\next\source\css\_custom\custom.styl样式文件中添加下面代码：

```
//代码块复制按钮
.highlight{
  //方便copy代码按钮（btn-copy）的定位
  position: relative;
}
.btn-copy {
    display: inline-block;
    cursor: pointer;
    background-color: #eee;
    background-image: linear-gradient(#fcfcfc,#eee);
    border: 1px solid #d5d5d5;
    border-radius: 3px;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    -webkit-appearance: none;
    font-size: 13px;
    font-weight: 700;
    line-height: 20px;
    color: #333;
    -webkit-transition: opacity .3s ease-in-out;
    -o-transition: opacity .3s ease-in-out;
    transition: opacity .3s ease-in-out;
    padding: 2px 6px;
    position: absolute;
    right: 5px;
    top: 5px;
    opacity: 0;
}
.btn-copy span {
    margin-left: 5px;
}
.highlight:hover .btn-copy{
  opacity: 1;
}
```

###引用
在.\themes\next\layout\_layout.swig文件中，添加引用（注：在 swig 末尾或 body 结束标签（</body>）之前添加）：

```
<!-- 代码块复制功能 -->
<script type="text/javascript" src="/js/src/clipboard.min.js"></script>  
<script type="text/javascript" src="/js/src/clipboard-use.js"></script>
```

###补充
懂代码的也可以将clipboard.min.js和clipboard-use.js合并为一个文件，再在.\themes\next\layout\_layout.swig文件中使用。当然clipboard.min.js也可以直接用三方cdn的方式引入也行。

##去除NexT主题Markdown分割线渲染效果
修改/source/css/_common/scaffolding/base.styl，注释或删除以下内容：

```
background-image: repeating-linear-gradient(
    -45deg,
    white,
    white 4px,
    transparent 4px,
    transparent 8px
  );
```

##不蒜子统计文章阅读数

打开主题配置文件，这里我用的next主题
搜索busuanzi_count:
将enable对应的false改为true即可
enable: true 

由于busuanzi(不蒜子)的网址更新,导致了使用Hexo Next主题时统计浏览数失效.
不蒜子官网:http://ibruce.info/2015/04/04/busuanzi/
解决方法:
到hexo的themes文件夹下, 进入
\themes\next\layout_third-party\analytics
打开: busuanzi-counter.swig
将src=“https://dn-lbstatics.qbox.me/busuanzi/2.3/busuanzi.pure.mini.js”
修改为src=“https://busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js”
即可.

##修改[Read More]按钮样式

修改themes\next\source\css\_custom\custom.styl文件，加入自定义样式

```
 // [Read More]按钮样式
.post-button .btn {
    color: #555 !important;
    background-color: rgb(255, 255, 255);
    border-radius: 3px;
    font-size: 15px;
    box-shadow: inset 0px 0px 10px 0px rgba(0, 0, 125, 0.35);
    border: none !important;
    transition-property: unset;
    padding: 0px 15px;
}

.post-button .btn:hover {
    color: rgb(255, 255, 255) !important;
    border-radius: 3px;
    font-size: 15px;
    box-shadow: inset 0px 0px 10px 0px rgba(0, 0, 0, 0.35);
    background-image: linear-gradient(90deg, #a166ab 0%, #ef4e7b 25%, #f37055 50%, #ef4e7b 75%, #a166ab 100%);
}
```

##修改标签云（tagcloud）的颜色

修改themes/next/layout/page.swig文件，加入自定义样式:

```
- {{ tagcloud({min_font: 12, max_font: 30, amount: 300, color: true, start_color: '#ccc', end_color: '#111'}) }}
+ {{ tagcloud({min_font: 13, max_font: 31, amount: 1000, color: true, start_color: '#9733EE', end_color: '#FF512F'}) }}
```

修改对应参数值即可，参数说明见 [Hexo官方文档](https://hexo.io/zh-cn/docs/helpers.html#tagcloud)

##文章加密访问

打开next\layout\_partials\head\head.swig文件,插入以下代码:

```
<script>
    (function(){
        if('{{ page.password }}'){
            if (prompt('请输入文章密码') !== '{{ page.password }}'){
                alert('密码错误！');
                history.back();
            }
        }
    })();
</script>
```

在文章头中加入password: 123456就可以了

(发现还是有 bug 的，就是右键在新标签中打开,然后无论是否输入密码，都能看到内容)

这里提供一种更好的办法
[hexo-blog-encrypt](https://easyhexo.com/3-Plugins-use-and-config/3-4-hexo-blog-encrypt/)
##移动端显示 back-to-top 按钮和侧栏

我的博客主题是Mist，主题的设计模版是 Muse 或 Mist,就可以直接在主题配置文件中配置：
修改主题配置themes/next/_config.yml

```
# Enable sidebar on narrow view
onmobile: true
```

你也可以自己调试页面
页面调试好之后将代码复制到:themes\next\source\css\_custom\custom.styl
参考custom.styl样式文件
不建议全部复制粘贴使用，最好是F12打开，根据关键ID找到对应的样式，复制到自己的文件中

```
// Custom styles.
/*******************首页样式*****************************/
// 顶栏宽度
.container .header-inner {
    width: 100%;
}

// .headband {
//     height: 1.5px;
//     background-image: linear-gradient(90deg, #F79533 0%, #F37055 15%, #EF4E7B 30%, #A166AB 44%, #5073B8 58%, #1098AD 72%, #07B39B 86%, #6DBA82 100%);
// }

// 页面顶部行高
.header {
    line-height: 1.5;
}

// // 页面背景色
// .container {
//     background-color: rgba(0, 0, 0, 0.75);
// }

// 页面留白更改
.header-inner {
    padding-top: 35px;
    padding-bottom: 0px;
}
.posts-expand {
    padding-top: 50px;
}
.posts-expand .post-meta {
    margin: 5px 0px 0px 0px;
}
.post-button {
    margin-top: 0px;
}
// 顶栏宽度
.container .header-inner {
    width: 100%;
}
// 渐变菜带，CSS代码copy自https://githubuniverse.com
// .site-meta {
//     background-image: linear-gradient(90deg, #F79533 0%, #F37055 15%, #EF4E7B 30%, #A166AB 44%, #5073B8 58%, #1098AD 72%, #07B39B 86%, #6DBA82 100%);
// }

//缩略图指定宽度值显示。
img.img-topic {
    width: 75%;
}


/*******************文章样式*****************************/
// 文章
.post {
    margin-bottom: 50px;
    padding: 45px 36px 36px 36px;
    box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.5);
    background-color: rgb(255, 255, 255);
}

// 文章标题字体
.posts-expand .post-title {
    font-size: 26px;
    font-weight: 700;
}
// 文章标题动态效果
.posts-expand .post-title-link::before {
    background-image: linear-gradient(90deg, #a166ab 0%, #ef4e7b 25%, #f37055 50%, #ef4e7b 75%, #a166ab 100%);
}
// 文章元数据（meta）留白更改
.posts-expand .post-meta {
    margin: 10px 0px 20px 0px;
}
// 文章的描述description
.posts-expand .post-meta .post-description {
    font-style: italic;
    font-size: 14px;
    margin-top: 30px;
    margin-bottom: 0px;
    color: #666;
}
// [Read More]按钮样式
.post-button .btn {
    color: #555 !important;
    background-color: rgb(255, 255, 255);
    border-radius: 3px;
    font-size: 15px;
    box-shadow: inset 0px 0px 10px 0px rgba(0, 0, 0, 0.35);
    border: none !important;
    transition-property: unset;
    padding: 0px 15px;
}

.post-button .btn:hover {
    color: rgb(255, 255, 255) !important;
    border-radius: 3px;
    font-size: 15px;
    box-shadow: inset 0px 0px 10px 0px rgba(0, 0, 0, 0.35);
    background-image: linear-gradient(90deg, #a166ab 0%, #ef4e7b 25%, #f37055 50%, #ef4e7b 75%, #a166ab 100%);
}
// 去除在页面文章之间的分割线
.posts-expand .post-eof {
    margin: 0px;
    background-color: rgba(255, 255, 255, 0);
}
// 去除页面底部页码上面的横线
.pagination {
    border: none;
    margin: 0px;
}

// 文章内标题样式（左边的竖线）
.post-body h2, h3, h4, h5, h6 {
    border-left: 4px solid rgb(161, 102, 171);
    margin-left: -36px;
    padding-left: 32px;
}
// 去掉图片边框
.posts-expand .post-body img {
    border: none;
    padding: 0px;
}
// 文章``代码块的自定义样式
code {
    margin: 0px 3px;
    border: 1px solid #999;
}

// 文章```代码块顶部样式
.highlight figcaption {
    margin: 0em;
    padding: 0.5em;
    background: #eee;
    border-bottom: 1px solid #e9e9e9;
}
.highlight figcaption a {
    color: rgb(80, 115, 184);
}
// 文章```代码块diff样式
pre .addition {
    background: #e6ffed;
}
pre .deletion {
    background: #ffeef0;
}

//文章内链接文本样式
.post-body p a{
  color: #0593d3;
  border-bottom: none;
  border-bottom: 1px solid #0593d3;
  &:hover {
    color: #fc6423;
    border-bottom: none;
    border-bottom: 1px solid #fc6423;
  }
}

// 自定义的文章摘要图片样式
img.img-topic {
    width: 100%;
}

/*************************侧栏样式****************************/
// 自定义的侧栏时间样式
#days {
    display: block;
    color: rgb(7, 179, 155);
    font-size: 13px;
    margin-top: 15px;
}
// 右下角侧栏按钮样式
.sidebar-toggle {
    right: 10px;
    bottom: 43px;
    background-color: rgba(247, 149, 51, 0.75);
    border-radius: 5px;
    box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.35);
}
.page-post-detail .sidebar-toggle-line {
    background: rgb(7, 179, 155);
}
// 右下角返回顶部按钮样式
.back-to-top {
    line-height: 1.5;
    right: 10px;
    padding-right: 5px;
    padding-left: 5px;
    padding-top: 2.5px;
    padding-bottom: 2.5px;
    background-color: rgba(247, 149, 51, 0.75);
    border-radius: 5px;
    box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.35);
}

// 侧栏
.sidebar {
    box-shadow: inset 0px 0px 10px 0px rgba(0, 0, 0, 0.5);
    background-color: rgba(0, 0, 0, 0.75);
}
.sidebar-inner {
    margin-top: 30px;
}
// 侧栏顶部文字
.sidebar-nav li {
    font-size: 15px;
    font-weight: bold;
    color: rgb(7, 179, 155);
}
.sidebar-nav li:hover {
    color: rgb(161, 102, 171);
}
.sidebar-nav .sidebar-nav-active {
    color: rgb(7, 179, 155);
    border-bottom-color: rgb(161, 102, 171);
    border-bottom-width: 1.5px;
}
.sidebar-nav .sidebar-nav-active:hover {
    color: rgb(7, 179, 155);
}
// 侧栏站点作者名
.site-author-name {
    display: none;
}
// 侧栏站点描述
.site-description {
    letter-spacing: 5px;
    font-size: 15px;
    font-weight: bold;
    margin-top: 15px;
    margin-left: 13px;
    color: rgb(243, 112, 85);
}
// 侧栏站点文章、分类、标签
.site-state {
    line-height: 1.3;
    margin-left: 12px;
}
.site-state-item {
    padding: 0px 15px;
    border-left: 1.5px solid rgb(161, 102, 171);
}
// 侧栏RSS按钮样式
.feed-link {
    margin-top: 15px;
    margin-left: 7px;
}
.feed-link a {
    color: rgb(255, 255, 255);
    border: 1px solid rgb(158, 158, 158) !important;
    border-radius: 15px;
}
.feed-link a:hover {
    background-color: rgb(161, 102, 171);
}
.feed-link a i {
    color: rgb(255, 255, 255);
}
// 侧栏社交链接
.links-of-author {
    margin-top: 0px;
}
// 侧栏友链标题
.links-of-blogroll-title {
    margin-bottom: 10px;
    margin-top: 15px;
    color: rgba(7, 179, 155, 0.75);
    margin-left: 6px;
    font-size: 15px;
    font-weight: bold;
}
// 侧栏超链接样式（友链的样式）
.sidebar a {
    color: #ccc;
    border-bottom: none;
}
.sidebar a:hover {
    color: rgb(255, 255, 255);
}
// 自定义的侧栏时间样式
#days {
    display: block;
    color: rgb(7, 179, 155);
    font-size: 13px;
    margin-top: 15px;
}
// 侧栏目录链接样式
.post-toc ol a {
    color: rgb(7, 179, 155);
    border-bottom: 1px solid rgb(96, 125, 139);
}
.post-toc ol a:hover {
    color: rgb(161, 102, 171);
    border-bottom-color: rgb(161, 102, 171);
}
// 侧栏目录链接样式之当前目录
.post-toc .nav .active > a {
    color: rgb(161, 102, 171);
    border-bottom-color: rgb(161, 102, 171);
}
.post-toc .nav .active > a:hover {
    color: rgb(161, 102, 171);
    border-bottom-color: rgb(161, 102, 171);
}
/* 修侧栏目录bug，如果主题配置文件_config.yml的toc是wrap: true */
.post-toc ol {
    padding: 0px 10px 5px 10px;
}
/* 侧栏目录默认全展开，已注释
.post-toc .nav .nav-child {
    display: block;
}
*/

/************************移动端样式*******************************/
@media (max-width: 1023px) {
    .container {
        background-color: rgba(0, 0, 0, 0);
    }
    .sidebar {
        // box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.5);
        border-top-left-radius: 5px;
        border-bottom-left-radius: 5px;
    }
    .feed-link {
        display: none !important;
    }
}
@media (max-width: 767px) {
    .main {
        padding-bottom: 120px;
    }
    .posts-expand {
        margin: 0px;
        padding-top: 10px;
    }
    .posts-expand .post-title {
        font-size: 22px;
    }
    .posts-expand .post-meta {
        font-size: 10px;
    }
    .post {
        margin-bottom: 30px !important;
        padding: 20px 15px 15px 15px !important;
    }
    .post-body h2, h3, h4, h5, h6 {
        margin-left: -15px;
        padding-left: 11px;
    }
    .posts-expand .post-tags {
        margin-top: 10px;
    }
    .post-widgets {
        margin-top: 10px;
    }
    .comments {
        margin: 40px 0px 40px 0px !important;
    }
    .footer {
        // box-shadow: 0px -5px 10px 0px rgba(0, 0, 0, 0.5);
    }
}
.sidebar-active #sidebar-dimmer {
    opacity: 0;
}
// 移动端左上角菜单按钮
.site-nav-toggle {
    top: 35px;
    left: 91px;
    // background-color: #222;
}
.btn-bar {
    background-color: rgb(255, 255, 255);
}
// 移动端菜单
@media (max-width: 767px) {
    .menu {
        text-align: center;
        // box-shadow: 0px 5px 10px 0px rgba(0, 0, 0, 0.5);
    }
    .site-nav {
        top: initial;
        background-color: rgba(255, 255, 255, 0.75);
        border-top: none;
        border-bottom: none;
        position: relative;
        z-index: 1024;
    }
}
//移动端顶部
@media (max-width: 767px) {
    .site-title {
        font-size: 28px !important;
        letter-spacing: 0px !important;
    }
    .site-subtitle{
        letter-spacing: 0px !important;
        padding-bottom: 0px !important;
    }
    .site-meta {
        // box-shadow: 0px 5px 10px 0px rgba(0, 0, 0, 0.5);
    }
    .menu .menu-item {
        margin: 0px 10px !important;
    }
}
```

## Hexo 中 MathJax 的静态显示（svg）

[Hexo 中 MathJax 的静态显示（svg）](https://io-oi.me/tech/hexo-mathjax-svg/)
