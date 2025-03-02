---
title: Vue Study
abbrlink: vue-study
date: 2021-01-25 10:12:36
tags: [Vue]
categories: Code

---

Vue 学习记录

<!--more-->

# Vue 介绍

Vue (读音 /vjuː/，类似于 **view**) 是一套用于构建用户界面的**渐进式框架**。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与[现代化的工具链](https://vuejs.bootcss.com/guide/single-file-components.html)以及各种[支持类库](https://github.com/vuejs/awesome-vue#libraries--plugins)结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。

# Vue 安装

## CDN 引入

制作原型或学习：

```html
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

生产环境：：

```html
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.12"></script>
```

## 下载引入

[开发版本](https://cn.vuejs.org/js/vue.js)（包含完整的警告和调试模式）

[生产版本](https://cn.vuejs.org/js/vue.min.js)（删除了警告，33.30KB min+gzip）

## NPM 安装

在用 Vue 构建大型应用时推荐使用 NPM 安装[[1\]](https://cn.vuejs.org/v2/guide/installation.html#footnote-1)。NPM 能很好地和诸如 [webpack](https://webpack.js.org/) 或 [Browserify](http://browserify.org/) 模块打包器配合使用。同时 Vue 也提供配套工具来开发[单文件组件](https://cn.vuejs.org/v2/guide/single-file-components.html)。

```shell
# 最新稳定版
$ npm install vue
```