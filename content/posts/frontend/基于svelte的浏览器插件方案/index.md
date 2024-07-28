---
title: "基于svelte的浏览器插件方案"
date: 2024-07-18T13:46:06+08:00
draft: false
---

最近需要制作一个浏览器插件，实现通过插件， 修改目标页面的时间。
这里选择svelte作为开发框架，因为svelte的编译方式，可以减少代码体积。

关于svelte和vue体积的对比， 前端圈子争论不休，挑出几个风靡一时的帖子看一下：
- [尤雨溪对比svelte和vue的构建体积](https://github.com/yyx990803/vue-svelte-size-analysis)
- [Jacek Schae 前端各框架对比](https://medium.com/dailyjs/a-realworld-comparison-of-front-end-frameworks-2020-4e50655fe4c1)

> ![fe-frameworks](./fe-frameworks.png)
> Jacek Scheae对多框架体积的对比图

## 浏览器插件简述

浏览器插件能做什么？ chrome 给出三个能力分类：
- 设计界面
- 控制浏览器
- 控制网络

详情可参考 [chrome插件开发文档](https://developer.chrome.com/docs/extensions/develop?hl=zh-cn) 了解具体使用。

本次浏览器插件有这几种部分组成：
- manifest.json 插件的配置文件
- background.js 后台脚本
- content.js 内容脚本
- popup.html 弹出页面


## 项目结构

## 构建配置

## 构建后的结构


