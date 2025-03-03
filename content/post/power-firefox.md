---
title: 打造你的最强Firefox浏览器
date: 2020-06-20 22:57:04
tags: 
 - "插件"
categories: "实用"
---

打造强大、安全、实用的Firefox浏览器

<!--more-->

# 下载 Firefox

国际版官网：[https://mozlilla.org/zh-CN/firefox](https://mozlilla.org/zh-CN/firefox)，时刻注意链接重定向

下面网址下载**国际英文版**

```
https://www.mozilla.org/en-US/firefox/
```

下面网址下载**国际中文版**

```
https://www.mozilla.org/zh-CN/firefox/
```

国内版官网：[http://firefox.com.cn](http://firefox.com.cn)，很有中国味道

# 插件&扩展

## **捕捉网页截图**

捕捉网页截图，编辑并将它们保存为PDF，JPEG，GIF，PNG或BMP；上传，打印，在Photoshop中打开，复制到剪贴板或电子邮件

https://getfireshot.com

## Easy Screenshot

https://addons.mozilla.org/en-US/firefox/addon/easyscreenshot/

## Absolute Enable Right Click & Copy

使不能复制的网站可以复制

https://addons.mozilla.org/en-US/firefox/addon/absolute-enable-right-click/

## Bitwarden

Free Password Manager

https://bitwarden.com/

## Saladict

Saladict 沙拉查词是一款专业划词翻译扩展，为交叉阅读而生。大量权威词典涵盖中英日韩法德西语，支持复杂的划词操作、网页翻译、生词本与 PDF 浏览。

https://saladict.crimx.com/

## Bypass Paywalls

https://github.com/iamadamdev/bypass-paywalls-chrome

## Enhancer for YouTube

YouTube 功能增强

https://www.mrfdev.com/enhancer-for-youtube

## Return YouTube Dislike

Returns ability to see dislikes

https://returnyoutubedislike.com/

## Modern for Hacker News

A redesigned web interface for Hacker News

https://www.modernhn.com

## Octotree

GitHub code tree

https://www.octotree.io

## OneTab

Save up to 95% memory and reduce tab clutter

http://www.one-tab.com

## Undo Close Tab

Reopens the last closed tab.

https://github.com/M-Reimer/undoclosetab

## Fire Drag

Drag texts and links that is also fully compatible with multiprocess Firefox

https://github.com/erictsangx/fire-drag

## **Gesturefy**

Navigate, operate and  browse faster with mouse gestures! A customizable mouse gesture add-on  with a variety of different commands.

鼠标手势

https://github.com/Robbendebiene/Gesturefy

## NoScript

Maximum protection for  your browser: NoScript allows active content only for trusted domains of your choice to prevent exploitation.

https://noscript.net

## **Tampermonkey **

油猴

The world's most popular userscript manager!

https://www.tampermonkey.net/

## **Wappalyzer**

Identify web technologies

https://www.wappalyzer.com

## BuiltWith

https://builtwith.com

## Video Speed Controller

Speed up, slow down, advance and rewind HTML5 audio/video with shortcuts

https://github.com/codebicycle/videospeed

## **Video DownloadHelper**

Download Videos from the Web

http://www.downloadhelper.net/

## **Proxy SwitchyOmega**

轻松快捷地管理和切换多个代理设置。

https://github.com/FelisCatus/SwitchyOmega

# 推荐首选项配置 Preferences

 Firefox 地址栏并输入 about:config 进入首选项配置页面

在搜索框中输入下面的内容，把对应的值双击修改为`true`即可实现。

### 新建标签页在当前标签页的右侧

```
browser.tabs.insertAfterCurrent
```

### 书签内容在当前标签页的右侧打开

```
browser.tabs.loadBookmarksInTabs
```

### 在当前标签页的右侧打开

地址栏： `browser.urlbar.openintab`

搜索框： `browser.search.openintab` 

### 双击标签页实现关闭标签页

```
browser.tabs.closeTabByDblclick
```

### 在新选项卡中打开新搜索结果

Firefox 在地址栏的右侧为您提供了一个搜索框。 这通常是一个 Google 搜索框。  如果您使用它来搜索有关特定关键字的信息，新信息将出现在您当前的选项卡中。 通过使用此搜索框进入新页面，您多久擦除您所在的页面？  如果您想让该网页保持打开状态，这可能会很麻烦。

您可以通过设置 about:config 在新选项卡中打开新搜索来避免这种情况。 以下是该怎么做：

打开 about:config 并搜索：

```
browser.search.openintab
```

双击设置将其更改为“true”。
