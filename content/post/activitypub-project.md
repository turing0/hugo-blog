---
title: Activitypub Project
slug: activitypub-project
date: 2023-02-03 22:36:18

---

# Intro 介绍

ActivitypubProject 项目招人（具体项目在介绍之后）

一些相关介绍

<!--more-->

## Mastodon 长毛象

[Mastodon](https://mastodon.social/) **长毛象**（开源去中心化的社交平台）：
Mastodon 是一个免费的开源社交网络程序，一个商业平台的替代方案，避免了单个公司垄断你沟通的风险。选择你信任的服务器，无论选择的是哪个，你都可以与其他人进行互动。任何人都可以运行自己的 Mastodon 实例，并无缝地参与到社交网络中。

> 如果你没有使用过 mastodon 等软件，强烈建议你使用一番。

它是当前推特最好的替代品，好到连推特都感到有压力。推特曾经[修改用户使用协议](https://www.nytimes.com/2022/12/18/business/twitter-ban-social-media-competitors-mastodon.html)，禁止用户在其平台上推广 Mastodon 等竞争对手，但迫于大面积的用户反对而取消。

**去中心化**的好处是即使有人做恶，那也不会影响到整个系统。去中心化使得整个系统保持了最大程度的健壮性。也就是说，我们每个人发言的权利通过去中心化技术得到了保障。

> 我们已然失去了最初的互联网精神。——Tim Berners-Lee

## ActivityPub 协议

Mastodon 的核心是 [ActivityPub 协议](https://www.w3.org/TR/activitypub/)，Mastodon 就是通过支持 ActivityPub 协议来实现去中心化的。而 ActivityPub 协议早在 Mastodon 之前就存在了，目前已由 [W3C](https://www.w3.org/) 将制定并发布为标准。

**ActivityPub 协议的神奇之处在于，只要是实现了这个协议的服务都可以相互交互，所以其他 ActivityPub 服务可以和  Mastodon 进行交互，也就是说你不用 Mastodon 就可以看 Mastodon 上的帖子以及关注 Mastodon 上的账户。**

这就引出 [Fediverse](https://en.wikipedia.org/wiki/Fediverse) 的概念，Mastodon 就是诞生于这样的概念之下的。Fediverse 是由 "federation" 和 "universe" 组合而成的新词，意思是“联邦宇宙”。

> 关于 Fediverse 更详细的解释，请看 [Fediverse 联邦宇宙](https://wzyboy.im/post/1486.html#:~:text=Fediverse%20%E6%98%AF%20federation,%2B%20universe%20%E7%9A%84%E9%80%A0%E8%AF%8D%EF%BC%8C%E4%B8%80%E8%88%AC%E8%AF%91%E4%B8%BA%E8%81%94%E9%82%A6%E5%AE%87%E5%AE%99%EF%BC%8C%E5%8D%B3%E6%98%AF%E7%94%B1%E5%90%84%E7%A7%8D%E7%A4%BE%E4%BA%A4%E7%BD%91%E7%BB%9C%E7%AB%99%E7%82%B9%E7%BB%84%E6%88%90%E7%9A%84%E4%B8%80%E4%B8%AA%E5%85%81%E8%AE%B8%E4%B8%8D%E5%90%8C%E7%AB%99%E7%82%B9%E4%B8%8A%E7%9A%84%E7%94%A8%E6%88%B7%E4%B9%8B%E9%97%B4%E4%BA%92%E7%9B%B8%E4%BA%A4%E6%B5%81%E7%9A%84%E8%81%94%E9%82%A6%E3%80%82)

联邦宇宙这个社交网络不同于主流平台（脸书、推特、Instagram、Pinterest 等）。主流平台会把上亿的用户集中在同一个网站里，然后他们就可以完全掌控决策权，监控用户，强迫内容审查，把用户的数据用于每一个可能的商业利益。**而联邦宇宙的目标则是去中心化和高度用户自治。**

Fediverse 是一个宏伟的概念，Mastodon 只是联邦宇宙这个中的一个小成员，还有很多符合 ActivityPub 协议的平台都可以被纳入其中，比如说 [Pleroma](https://pleroma.social/)、[Misskey](https://misskey-hub.net/en/)、[GoToSocial](https://gotosocial.org/)、[Friendica](https://friendi.ca/)、[Funkwhale](https://funkwhale.audio/)、[PeerTube](https://joinpeertube.org/)、[BookWyrm](https://joinbookwyrm.com/) 等等。

基于 ActivityPub 协议的服务都是可以相互交互的，所以在这个联邦宇宙中的所有软件都是互通的，比如说，你可以在 Mastodon  这样的微博客平台直接欣赏 Funkwhale 上的音乐，也可以在 Misskey 里直接观看 PeerTube 上的视频，也可以在  Pleroma 上阅读 BookWyrm 里别人的阅读笔记和书评……这就好比一下子打通了  Facebook、Twitter、YouTube、Spotify、Blogger 和 GoodRead！

**这将会是一个万物互联，万物互通的宇宙！**

------

*请注意：*

**本项目为爱发电（我们不提供酬劳），但根据 [Patreon](https://patreon.com/mastodon) 数据显示：目前有将近一万人在 [Patreon](https://patreon.com/mastodon) 上为 Mastodon 项目资助，每月有近 4 万美元。**

------

# Project 项目

## Project 1 项目 1

 ActivityPub 协议是公开的，用户也可以随意选择使用任何客户端来连接联邦宇宙，为此，我们想为各联邦软件提供客户端（包括 iOS 、Android、Web），如 PeerTube、Misskey、Funkwhale、BookWyrm 等。

**有人想问，既然这个没有酬劳，为什么还会有人愿意参加呢？？**
是的，这是一个没有酬劳的项目，Mastodon 也是一样，我们参加的动力在于兴趣、对自由的信念以及对互联网的信仰。其实，为 Mastodon 工作的人，还有很多其他的因素，例如与志同道合的人交流、分享知识、拓展人际关系等等。 所以，即使没有酬劳，也有很多人会参与其中，因为它给他们带来了很多其他的价值。

**那么我可以获得什么呢？**
帮助增强自我能力和技能，团队合作和沟通能力，可能的捐赠收入，成功的自豪感、成就感！在这样的环境中，你可以不断学习和成长，从而提高自身价值，利于个人发展和成长。

> 我总是深入思考，我希望别人也能想远一点。我为理想而工作，并从别人身上学习，我不喜欢拒人于外。我是个完美主义者，但我不会要求出版界也精益求精。除了教育和娱乐以外，我不会浪费时间在那些不会有影响的事情上。我不记恨他人，因为这于创造无益。但我从自身经历中学习，我想让世界变得更美好。
> 
> ——Aaron Swartz

## Project 2 项目 2

开发自动化工具，为广大的联邦节点主提供便捷的自动化工具，让节点主可以快速部署或卸载 ActivityPub 服务、备份和恢复数据、迁移、监控服务数据等。

在项目 1 成熟的情况下，这个会有利润，所以目前我们着力发展项目 1。

# We need 我们需要

- iOS 开发（Swift、Objective-C）
- Web 开发（语言不限）
- 后端开发（语言不限）
- Android 开发（语言不限）

# We hope you 我们希望你

别担心自己的能力，我们需要志同道合的朋友！

- 阅读英文文档能力
- 保持好奇心
- 学习的激情
- 热爱开源

> Success is not the key to happiness. Happiness is the key to success. If you love what you are doing, you will be successful.    —— John Ruskin

# Contact 联系

如果你感兴趣，请联系 QQ：1750421753

期待与你合作~
