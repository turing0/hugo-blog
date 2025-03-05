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



### 主页右侧导航栏去除归档和分类

`hugo.yaml` 配置

```scss
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







---

## Shortcoeds

以下代码块的内容实际使用请记得将大括号换成双大括号哦。

### animated_text 动态文字

`{< animated_text text="L a p h e l"  >}`

{{< animated_text  text="L a p h e l"  >}}

`{< animated_text text="哈哈" align="right" >}`

{{< animated_text text="哈哈" align="right"  >}}

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
