---
title: "Hugo stack 主题美化"
slug: hugo-stack-renovation
date: 2025-03-02 08:13:09
---

装修下博客



## 网站

以下的 `custom.scss` 均指  `博客根目录/assets/scss/custom.scss` 文件。

### 网站头像及名字居中

custom.scss 添加代码

顺便把描述的字体改小了一点

```scss
// 站点头像，网站名字和描述居中
.sidebar header {
  .site-avatar {
    margin: auto;
  }

  .site-name {
    margin: auto;
  }

  .site-description {
    margin: auto;
    font-size: 1.3rem;
    @include respond(2xl) {
      font-size: 1.6rem;
    }
  }
}
// 社交图标居中
.menu-social {
  margin: auto;
}
```

### 归档页面

**分类列表优化，卡片缩放动画**

改小了一点，原先的太大了

custom.scss 添加代码

```scss
// 归档页面 分类列表优化
.subsection-list {
    .article-list--tile {
        display: flex;
        padding-bottom: 15px;

        article {
            width: 200px;
            height: 120px;
            margin-right: 10px;

            .article-title {
                margin: 0;
                font-size: 1.8rem;
            }
      }
    }
}

// 归档页面卡片缩放动画
.article-list--tile article {
  transition: .6s ease;
}
.article-list--tile article:hover {
  transform: scale(1.03, 1.03);
}
```

**归档页面两栏**

```scss
// 归档页面两栏
@media (min-width: 1024px) {
  .article-list--compact {
    display: grid;
    grid-template-columns: 1fr 1fr;
    background: none;
    box-shadow: none;
    gap: 1rem;

    article {
      background: var(--card-background);
      border: none;
      box-shadow: var(--shadow-l2);
      margin-bottom: 8px;
      border-radius: 16px;
    }
  }
}
```

#### 归档页面显示文章副标题/简介

`custom.scss` 添加代码

```scss
.article-subtitle {
    margin-top: -5px;
    font-size: 1.5rem;

    @include respond(md) {
        font-size: 1.6rem;
    }
}
```

`主题根目录/layouts/partials/article-list/compact.html` 开头 h2 下方添加代码

```html
<h2 class="article-title">
    {{- .Title -}}
</h2>
{{ with .Params.description }}
    <div class="article-subtitle">
        {{ . }}
    </div>
{{ end }}
```

### 左侧导航栏菜单间距

custom.scss 添加代码，根据自己需求修改 gap

```scss
// 左侧导航栏菜单间距
#main-menu {
  &, .menu-bottom-section ol {
      flex-direction: column;
      gap: 20px;

      @include respond(xl) {
          gap: 20px;
      }
  }
}
```



### 移动端目录按钮

电脑端保持原来的目录，移动端添加一个按钮可以打开目录。

添加文件 `layouts/partials/widget/toc.html`

```html
{{ if (.Context.Scratch.Get "TOCEnabled") }}
    <!-- toc 按钮，用于展开和收起目录 -->
    <button id="toggle-toc" class="mobile-only">Toc</button>
    <section class="widget archives" id="toc-container">
        <h2 class="widget-title section-title">{{ T "article.tableOfContents" }}</h2>
        <!-- 创建一个带有 "widget-title" 和 "section-title" 类的标题区块，并显示 "article.tableOfContents" 的本地化内容 -->

        <div class="widget--toc">
            {{ .Context.TableOfContents }}
        </div>
    </section>
{{ end }}

{{ if (.Context.Scratch.Get "TOCEnabled") }}
    <section class="widget archives">
        <div class="widget-icon">
            {{ partial "helper/icon" "hash" }}
        </div>
        <h2 class="widget-title section-title">{{ T "article.tableOfContents" }}</h2>
        
        <div class="widget--toc">
            {{ .Context.TableOfContents }}
        </div>
    </section>
{{ end }}

<style>
    /* 默认隐藏移动端目录元素 */
    .mobile-only {
        display: none !important;
    }
    
    #toc-container {
        display: none;
        /* 初始时隐藏目录 */
        position: fixed;
        /* 使用固定定位，使其固定在视口中 */
        bottom: 21%;
        /* 距离视口顶部的距离，可以根据需要进行调整 */
        right: 60px;
        /* 距离视口右侧的距离，可以根据需要进行调整 */
        background-color: var(--card-background);
        /* 可选：设置背景颜色 */
        padding: 10px;
        /* 可选：添加一些内边距 */
        border: 1px solid #96979a50;
        border-radius: var(--card-border-radius);
        box-shadow: rgba(14, 30, 37, 0.12) 0px 2px 4px 0px, rgba(14, 30, 37, 0.32) 0px 2px 16px 0px;
        /* 可选：添加边框样式 */
        z-index: 9998 !important;
        /* 可选：设置 z-index 以确保它显示在其他元素之上 */
        max-height: 80vh;
        /* 设置最大高度为视口高度的 80% */
        overflow-y: auto;
        /* 添加垂直滚动条，以便在内容溢出时滚动 */
        width: auto;
        /* 让容器的宽度自适应内容 */
        max-width: 290px;
    }
    
    #toggle-toc {
        position: fixed;
        bottom: 22%;
        right: 20px;
        padding: 10px 10px;
        z-index: 9998 !important;
        border: 0px solid #96979a50;
        border-radius: 7px;
        box-shadow: var(--shadow-l1);
        background-color: #00640010;
        color: #34495e;
        /* 确保按钮在其他元素之上 */
        /* 其他样式保持不变 */
        display: block;
        /* 显示按钮 */
        margin-bottom: 10px;
        cursor: pointer;
        font-size: 1.2rem;
        /* 可选：改变鼠标光标以指示按钮是可点击的 */
    }
    
    .widget--toc #TableOfContents {
        overflow-x: auto;
        max-height: 66vh;
        width: auto;
    }
    
    @media screen and (max-width: 768px) {
        .mobile-only {
            display: block !important;
        }
        
        #toggle-toc {
            bottom: 100px;
        }
    }
</style>

<script>
    // 获取按钮和目录的元素
    var toggleButton = document.getElementById('toggle-toc');
    var tocContainer = document.getElementById('toc-container');
    var scrollThreshold = 100; // 设置滚动显示的阈值

    // 监听页面滚动事件
    window.addEventListener('scroll', function() {
        // 获取当前滚动位置
        var scrollY = window.scrollY || window.pageYOffset;

        // 检查滚动位置是否超过阈值
        if (scrollY >= scrollThreshold) {
            // 显示按钮
            toggleButton.style.display = 'block';
        } else {
            // 隐藏按钮
            toggleButton.style.display = 'none';
        }
    });

    // 添加点击事件处理程序
    toggleButton.addEventListener('click', function() {
        // 切换目录的显示状态
        if (tocContainer.style.display === 'none' || tocContainer.style.display === '') {
            tocContainer.style.display = 'block';
        } else {
            tocContainer.style.display = 'none';
        }
    });
    // 当鼠标悬浮在按钮上时显示目录
    toggleButton.addEventListener('mouseover', function() {
        tocContainer.style.display = 'block';
    });

    // 添加点击页面空白处的事件处理程序
    document.addEventListener('click', function(event) {
        // 检查点击事件是否发生在目录容器之外，并且不是按钮本身
        if (!tocContainer.contains(event.target) && event.target !== toggleButton) {
            // 点击发生在目录容器之外，隐藏目录容器
            tocContainer.style.display = 'none';
        }
    });
</script>

```

除了中间 if 那块是原来主题根目录下的代码，顶部和尾部的代码是新添加的。

此外，还需要在 `custom.scss` 文件中添加如下代码，不然移动端看不见按钮，就是将右栏改为 flex 布局。

```scss
.container {
  .right-sidebar {
    max-width: 20%;

    // 移动端目录按钮的显示
    display: flex;
  }
}
```







### 主页右侧导航栏去除归档和分类

`hugo.yaml` 配置

```yaml
    widgets:
        homepage:
            - type: search
            # - type: archives
            #   params:
            #       limit: 5
            # - type: categories
            #   params:
            #       limit: 10
            - type: tag-cloud
              params:
                  limit: 10
        page:
            - type: toc
```

### 添加上一篇下一篇文章

`主题根目录/layouts/_default/single.html`

在 {{ partial "article/components/related-content" . }} 下方添加代码

```html
    <div class="pre-next">
        {{with .PrevInSection}}
            <a class="pre-next-btn bg" href="{{.Permalink}}"><< {{ .Title }}</a>
        {{end}}
        {{with .NextInSection}}
            <a class="pre-next-btn bg" href="{{.Permalink}}">{{ .Title }} >></a>
        {{end}}
    </div>
```

`custom.scss`添加样式

```scss
// 上一篇下一篇的样式
.pre-next {
  display: flex;
  text-align: center;
  justify-content: space-between;
  align-items: center;
  margin: 20px 0;
}
.pre-next-btn {
  font-size: 1.4rem;
  padding: 8px 18px;
  border-radius: 20px;
  text-decoration: none;
  display: inline-block;
}
@media (max-width: 768px) {
  .pre-next {
    flex-direction: column;
    align-items: center;
  }
  .pre-next-btn {
    font-size: 3.5vw;
    padding: 12px 25px;
    margin: 10px 0;
  }
}
```

### 博客文章下缩小左导航栏

当在阅读文章页面时，我觉得左侧导航栏有点不好看，希望能沉浸式阅读，于是有了下面的修改。

具体修改：电脑端时且在阅读博客文章时，不显示头像，描述和社交链接，以及左导航栏的文字内容。移动端需要显示，所以这就涉及到结合 css 媒体查询进行条件渲染了。

效果：

![shrink-result](shrink-result.png)

添加文件 `/layouts/partials/sidebar/left.html`

先将主题根目录的此文件复制过来，我们在此基础修改，很简单。

顶行添加变量定义：

```html
{ $isBlogPost := eq .Section "post" }}
```

我们用这个判断当前页面是不是处于 post 下，这里根据你自己的主题可能需要修改具体的值，因为 stack 主题博文都是保存在 `/content/post` 下，所以这里写的是post，根据你自己的情况调整。

最后一行添加如下代码：

```html
<style>
    /* 默认状态：始终显示 */
    .hidden-post {
        display: block;
    }

    /* 判断isBlogPost为真且是非移动端时隐藏 */
    @media (min-width: 769px) {
        {{ if $isBlogPost }}
        .hidden-post {
            display: none;
        }
        {{ end }}
    }

    /* 在移动端（max-width: 768px）时，强制显示 */
    @media (max-width: 768px) {
        .hidden-post {
            display: block !important;
        }
    }
</style>
```

我们用 hidden-post 来控制是否隐藏，现在只需要在我们希望的元素上添加上这个 class 即可。

最终的完整代码：

```html
{{ $isBlogPost := eq .Section "post" }}

<aside class="sidebar left-sidebar sticky {{ if .Site.Params.sidebar.compact }}compact{{ end }}">
    <button class="hamburger hamburger--spin" type="button" id="toggle-menu" aria-label="{{ T `toggleMenu` }}">
        <span class="hamburger-box">
            <span class="hamburger-inner"></span>
        </span>
    </button>

    <header>
        {{ with .Site.Params.sidebar.avatar }}
            {{ if (default true .enabled) }}
                <figure class="site-avatar hidden-post">
                    <a href="{{ .Site.BaseURL | relLangURL }}">
                        {{ if not .local }}
                            <img src="{{ .src }}" width="300" height="300" class="site-logo" loading="lazy" alt="Avatar">
                        {{ else }}
                            {{ $avatar := resources.Get (.src) }}

                            {{ if $avatar }}
                                {{ $avatarResized := $avatar.Resize "300x" }}
                                <img src="{{ $avatarResized.RelPermalink }}" width="{{ $avatarResized.Width }}"
                                    height="{{ $avatarResized.Height }}" class="site-logo" loading="lazy" alt="Avatar">
                            {{ else }}
                                {{ errorf "Failed loading avatar from %q" . }}
                            {{ end }}
                        {{ end }}
                    </a>
                    {{ with $.Site.Params.sidebar.emoji }}
                        <span class="emoji">{{ . }}</span>
                    {{ end }}
                </figure>
            {{ end }}
        {{ end }}

        <div class="site-meta">
            <h1 class="site-name hidden-post"><a href="{{ .Site.BaseURL | relLangURL }}">{{ .Site.Title }}</a></h1>
            <h2 class="site-description hidden-post">{{ .Site.Params.sidebar.subtitle }}</h2>
        </div>
    </header>

    {{ with .Site.Menus.social -}}
        <ol class="menu-social">
            {{ range . }}
                <li class="hidden-post">
                    <a 
                        href='{{ .URL }}'
                        {{ if eq (default true .Params.newTab) true }}target="_blank"{{ end }}
                        {{ with .Name }}title="{{ . }}"{{ end }}
                        rel="me"
                    >
                        {{ $icon := default "link" .Params.Icon }}
                        {{ with $icon }}
                            {{ partial "helper/icon" . }}
                        {{ end }}
                    </a>
                </li>
            {{ end }}
        </ol>
    {{- end -}}

    <ol class="menu" id="main-menu">
        {{ $currentPage := . }}
        {{ range .Site.Menus.main }}
        {{ $active := or (eq $currentPage.Title .Name) (or ($currentPage.HasMenuCurrent "main" .) ($currentPage.IsMenuCurrent "main" .)) }}
        <li {{ if $active }} class='current' {{ end }}>
            <a href='{{ .URL }}' {{ if eq .Params.newTab true }}target="_blank"{{ end }}>
                {{ $icon := default .Pre .Params.Icon }}
                {{ if .Pre }}
                    {{ warnf "Menu item [%s] is using [pre] field to set icon, please use [params.icon] instead.\nMore information: https://stack.jimmycai.com/config/menu" .URL }}
                {{ end }}
                {{ with $icon }}
                    {{ partial "helper/icon" . }}
                {{ end }}
                    <span class="hidden-post">{{- .Name -}}</span>
            </a>
        </li>
        {{ end }}
        <li class="menu-bottom-section">
            <ol class="menu">
                {{- $currentLanguageCode := .Language.Lang -}}
                {{ if ( compare.Gt .Site.Home.AllTranslations.Len 1 ) }}
                    {{ with .Site.Home.AllTranslations }}
                        <li id="i18n-switch">  
                            {{ partial "helper/icon" "language" }}
                            <select name="language" title="language" onchange="window.location.href = this.selectedOptions[0].value">
                                {{ range . }}
                                    <option value="{{ .Permalink }}" {{ if eq .Language.Lang $currentLanguageCode }}selected{{ end }}>{{ .Language.LanguageName }}</option>
                                {{ end }}
                            </select>
                        </li>
                    {{ end }}
                {{ end }}

                {{ if (default false .Site.Params.colorScheme.toggle) }}
                    <li id="dark-mode-toggle">
                        {{ partial "helper/icon" "toggle-left" }}
                        {{ partial "helper/icon" "toggle-right" }}
                        <span class="hidden-post">{{ T "darkMode" }}</span>
                    </li>
                {{ end }}
            </ol>
        </li>
    </ol>
</aside>

<style>
    /* 默认状态：始终显示 */
    .hidden-post {
        display: block;
    }

    /* 判断isBlogPost为真且是非移动端时隐藏 */
    @media (min-width: 769px) {
        {{ if $isBlogPost }}
        .hidden-post {
            display: none;
        }
        {{ end }}
    }

    /* 在移动端（max-width: 768px）时，强制显示 */
    @media (max-width: 768px) {
        .hidden-post {
            display: block !important;
        }
    }
</style>
```

如果你在用的编辑器报错，不用管他，这是因为 html 没有 hugo 的模板语法。

---

## Shortcoeds

以下代码块的内容实际使用请记得将大括号换成双大括号哦。

### animated-text 动态文字

`{< animated-text text="L a p h e l"  >}`

{{< animated-text  text="L a p h e l"  >}}

`{< animated-text text="哈哈" align="right" >}`

{{< animated-text text="哈哈" align="right"  >}}

`layouts/shortcodes/animated-text.html`代码：

```html
{{ $text := .Get "text" | default "L a p h e l" }}
{{ $align := .Get "align" | default "center" }}
{{ $fontSize := .Get "font-size" | default "90" }}

<div class="" style="text-align: {{ $align }}; width: 100%; max-width: 100%;">
  <svg xmlns="http://www.w3.org/2000/svg" class="name" font-size="{{ $fontSize }}" viewBox="0 0 1000 200" preserveAspectRatio="xMidYMid meet">
    {{ $textAnchor := "middle" }}
    {{ $xPosition := "50%" }}
    {{ if eq $align "left" }}
      {{ $textAnchor = "start" }}
      {{ $xPosition = "0%" }}
    {{ else if eq $align "right" }}
      {{ $textAnchor = "end" }}
      {{ $xPosition = "100%" }}
    {{ end }}

    <text text-anchor="{{ $textAnchor }}" x="{{ $xPosition }}" y="66%" text-transform="uppercase" fill="none" stroke="#5d3d21" stroke-width="1px" stroke-dasharray="90 310">
      {{ $text }}
      <animate attributeName="stroke-dashoffset" begin="-1.5s" dur="6s" from="0" to="-400" repeatCount="indefinite"></animate>
    </text>

    <text text-anchor="{{ $textAnchor }}" x="{{ $xPosition }}" y="66%" text-transform="uppercase" fill="none" stroke="#212c27" stroke-width="1px" stroke-dasharray="90 310">
      {{ $text }}
      <animate attributeName="stroke-dashoffset" begin="-3s" dur="6s" from="0" to="-400" repeatCount="indefinite"></animate>
    </text>

    <text text-anchor="{{ $textAnchor }}" x="{{ $xPosition }}" y="66%" text-transform="uppercase" fill="none" stroke="#ebb10d" stroke-width="1px" stroke-dasharray="90 310">
      {{ $text }}
      <animate attributeName="stroke-dashoffset" begin="-4.5s" dur="6s" from="0" to="-400" repeatCount="indefinite"></animate>
    </text>

    <text text-anchor="{{ $textAnchor }}" x="{{ $xPosition }}" y="66%" text-transform="uppercase" fill="none" stroke="#9b59b6" stroke-width="1px" stroke-dasharray="90 310">
      {{ $text }}
      <animate attributeName="stroke-dashoffset" begin="-6s" dur="6s" from="0" to="-400" repeatCount="indefinite"></animate>
    </text>
  </svg>
</div>

```





### glow-quote 发光的quote

{{< glow-quote>}}
YouTube has surpassed 50 million Music and Premium subscribers, including trialers, and is the fastest growing music subscription service out there (MiDIA).

{{< /glow-quote>}}

---

{{< glow-quote glowColor="rgba(214, 236, 255, 0.95)" glowSize="50px" blurAmount="25px" fontSize="1.8rem" >}}
“ The unique offerings of YouTube Music and Premium are 
resonating in established and emerging music markets alike. We’re seeing
 impressive growth in countries like Korea, India, Japan, Russia & 
Brazil where music is a top passion.”
{{< /glow-quote>}}





<font class="colorfulfont"> 我挑的配色很好看吧！<br>好喜欢蓝色（再次）（再次）<br> 但总之换行的话就加个空标签。</font>

```
{< mark text="好喜欢蓝色！" >}
```

{{< mark text="好喜欢蓝色！" >}}

<span class="blur">一些手动打码效果！<br>但总之换行的话就加个空标签。</span>

<span class="shady">数据删除！数据删除！<br>但总之换行的话就加个空标签。</span>

`{< shake effect="shake" >}这是基本的摇晃效果。{< /shake >}`

{{< shake effect="shake" >}}这是基本的摇晃效果。{{< /shake >}}

{{< shake effect="shake-hard" >}}这个段落有剧烈摇晃效果。{{< /shake >}}

{{< shake effect="shake-slow" >}}这个段落有慢速摇晃效果。{{< /shake >}}

{{< shake effect="shake-little" >}}这个段落有轻微摇晃效果。{{< /shake >}}

{{< shake effect="shake-horizontal" >}}这个段落有水平摇晃效果。{{< /shake >}}

{{< shake effect="shake-vertical" >}}这个段落有垂直摇晃效果。{{< /shake >}}

{{< shake effect="shake-rotate" >}}这个段落有旋转摇晃效果。{{< /shake >}}

{{< shake effect="shake-opacity" >}}这个段落有透明度变化摇晃效果。{{< /shake >}}

{{< shake effect="shake-crazy" >}}这个段落有疯狂摇晃效果。{{< /shake >}}

{{< shake effect="shake-freeze" >}}这个段落在悬停时冻结。{{< /shake >}}

{{< shake effect="shake-constant" >}}这个段落持续摇晃。{{< /shake >}}

{{< card >}}
可以在这里插入链接假装是卡片式链接。
<br>
好像不能插入图片？
<br>
换行需要空标签。实际使用需要双括号。
{{< /card >}}

{{< underline color="#ffdd00" content="谁在用琵琶弹奏一曲东风破" >}}
<br/>
{{< underline color="#ff2200" content="岁月在墙上剥落看见小时候" >}}

## REF

[建站技术 | 使用 Hugo &#43; Stack 简单搭建一个博客](https://blog.reincarnatey.net/2023/build-hugo-blog-with-stack-mod/#%E6%B7%BB%E5%8A%A0%E8%87%AA%E5%B7%B1%E7%9A%84%E7%A4%BE%E4%BA%A4%E5%AA%92%E4%BD%93%E8%81%94%E7%B3%BB%E6%96%B9%E5%BC%8Frss)

[小白hugo博客装修笔记（1）](https://www.blain.top/p/renovation/)

[个人网站的建立过程（三）：Hugo主题stack的使用与优化](https://jinli.io/p/%E4%B8%AA%E4%BA%BA%E7%BD%91%E7%AB%99%E7%9A%84%E5%BB%BA%E7%AB%8B%E8%BF%87%E7%A8%8B%E4%B8%89hugo%E4%B8%BB%E9%A2%98stack%E7%9A%84%E4%BD%BF%E7%94%A8%E4%B8%8E%E4%BC%98%E5%8C%96/#%E4%BF%AE%E6%94%B9%E5%B9%B6%E4%BC%98%E5%8C%96%E4%B8%BB%E9%A2%98)

https://zhuanlan.zhihu.com/p/688275787

[Hugo博客 | stack主题修改第一站](https://munlelee.github.io/post/hugo%E5%8D%9A%E5%AE%A2-stack%E4%B8%BB%E9%A2%98%E4%BF%AE%E6%94%B9%E7%AC%AC%E4%B8%80%E7%AB%99/)

[Hugo Stack 魔改美化 | Naive Koala](https://www.xalaok.top/post/stack-modify/)

[Hugo Stack主题更新小记](https://xrg.fj.cn/p/hugo-stack%E4%B8%BB%E9%A2%98%E6%9B%B4%E6%96%B0%E5%B0%8F%E8%AE%B0/)

https://innerso.prvcy.page/posts/configure-waline/

https://yelleis.top/p/61fdb627/

https://www.sleepymoon.cyou/2023/hugo-shortcodes/

https://ghjayce.github.io/p/static-site-generator/hugo/hugo-theme-stack-gallery-study/

https://www.xalaok.top/post/stack-modify/#%E9%A6%96%E9%A1%B5%E6%AC%A2%E8%BF%8E%E6%A8%AA%E5%B9%85
