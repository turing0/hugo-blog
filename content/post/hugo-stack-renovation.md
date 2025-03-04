---
title: "Hugo stack 主题美化"
slug: hugo-stack-renovation
date: 2025-03-02 08:13:09
---

装修下博客

---

```python
@bot.command(aliases=['s'])
async def stock(ctx, stock: str, days: int = 93):
    channel_id = ctx.channel.id
    if channel_id not 7494]:
        await ctx.send(content=f"此频道不可使用此命令")
        return
    stock = stock.upper()
    stock_list = stock.split(',')
    for stock in stock_list:
        try:
            if len(stock) < 3 or stock[-3] != '.':
                stock = stock+'.US'
            today = datetime.today()
            days_ago = toda
            df = pd.DataFrame(candle_data)
            df['Date'] = pd.to_datetime(df['timestamp'], unit='s')

            # 按日期排序
            df = df.sort_values('Date').reset_index(drop=True)
            # 转换数值字段
            numeric_fields = ['open', 'close', 'low', 'high', 'volume', 'turnover']
            for field in numeric_fields:
                df[field] = pd.to_numeric(df[field], errors='coerce')
            df.set_index('Date', inplace=True)
```





## 网站

以下的 `custom.scss` 均指  `博客根目录/assets/scss/custom.scss` 文件。



### 左侧导航栏菜单间距

custom.scss 添加代码，根据自己需求修改 gap

```scss
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

https://www.blain.top/p/renovation/

[个人网站的建立过程（三）：Hugo主题stack的使用与优化](https://jinli.io/p/%E4%B8%AA%E4%BA%BA%E7%BD%91%E7%AB%99%E7%9A%84%E5%BB%BA%E7%AB%8B%E8%BF%87%E7%A8%8B%E4%B8%89hugo%E4%B8%BB%E9%A2%98stack%E7%9A%84%E4%BD%BF%E7%94%A8%E4%B8%8E%E4%BC%98%E5%8C%96/#%E4%BF%AE%E6%94%B9%E5%B9%B6%E4%BC%98%E5%8C%96%E4%B8%BB%E9%A2%98)

https://zhuanlan.zhihu.com/p/688275787

[Hugo博客 | stack主题修改第一站](https://munlelee.github.io/post/hugo%E5%8D%9A%E5%AE%A2-stack%E4%B8%BB%E9%A2%98%E4%BF%AE%E6%94%B9%E7%AC%AC%E4%B8%80%E7%AB%99/)

[Hugo Stack 魔改美化 | Naive Koala](https://www.xalaok.top/post/stack-modify/)

[Hugo Stack主题更新小记](https://xrg.fj.cn/p/hugo-stack%E4%B8%BB%E9%A2%98%E6%9B%B4%E6%96%B0%E5%B0%8F%E8%AE%B0/)

https://yelleis.top/p/61fdb627/

https://www.sleepymoon.cyou/2023/hugo-shortcodes/

https://ghjayce.github.io/p/static-site-generator/hugo/hugo-theme-stack-gallery-study/

https://www.xalaok.top/post/stack-modify/
