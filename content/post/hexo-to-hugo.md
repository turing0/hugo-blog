+++
title = "从 Hexo 到 Hugo "
slug = "hexo-to-hugo"
date = "2025-02-28"
description = "博客搬到 Hugo 啦"
tags = [
    "shortcodes",
    "hugo",
]

+++

因为 hexo 速度较慢，且受限于 npm 版本，管理起来较为繁琐，所以换到 hugo 啦，也是开源的，而且社区良好！





## 部署到 CloudFlare Pages

我用的 extended 版本，部署到 cf pages上 时设置 hugo 的版本直接写的版本号，发现会报错：提示需要 extended 版本，那要怎么写呢？

Google 搜索关键词：`cloudflare hugo extended`，在 [这个issue](https://github.com/cloudflare/cloudflare-docs/issues/6630) 看到了写法：

需要在版本号前面加 `extended_`，即 `HUGO_VERSION = extended_0.145.0`，然后正常部署就行啦。







## 博客装修美化

缝缝补补啦~

[Hugo stack 主题美化](https://blog.laphel.com/posts/hugo-stack-renovation/)

---

## Ref

[Quickly Build Blog with Hugo-theme-stack](https://liuhouliang.com/en/post/hugo_theme/)

[个人网站的建立过程（二）：使用Hugo框架搭建个人网站](https://jinli.io/p/%E4%B8%AA%E4%BA%BA%E7%BD%91%E7%AB%99%E7%9A%84%E5%BB%BA%E7%AB%8B%E8%BF%87%E7%A8%8B%E4%BA%8C%E4%BD%BF%E7%94%A8hugo%E6%A1%86%E6%9E%B6%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E7%BD%91%E7%AB%99/)

https://zhuanlan.zhihu.com/p/688275787

https://tomo.dev/posts/create-hugo-theme-from-scratch/part-two/

重定向旧链接

[Redirects · Cloudflare Pages docs](https://developers.cloudflare.com/pages/configuration/redirects/)

[将博客迁移到了 Cloudflare Pages](https://qcrao.com/post/migrate-blog-to-cloudflare-pages/)
