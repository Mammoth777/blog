---
title: "Hugo + GitHub Pages + Actions 个人博客搭建"
date: 2024-07-04T08:27:09+08:00
draft: false
categories: ["General", "Hugo", "todo"]
---

## 1. 通过Hugo生成站点

## 2. 通过GitHub Pages发布站点

## 3. 通过GitHub Actions自动化部署

## 4. 映射到自己的域名

### 4.1 搞个域名

### 4.2 配置https

## FAQ

### 1. 为什么启动后， 是空白页页面， 报错如下


`WARN 2024/07/04 21:05:13 found no layout file for "HTML" for kind "page": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.
`

这里是因为主题加载失败， 通常我们是通过`submodule`加载的主题， 重新拉取主题即可

```bash
git submodule update --init --recursive
```