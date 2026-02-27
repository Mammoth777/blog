---
title: "Makefile 入门"
date: 2023-11-20
categories: ["后端", "构建工具"]
draft: false
---

## 基本语法

- 声明变量：`xxx=xxx`
- 声明命令：`xxx:`

- 不输出：前面加个 `@`

## 示例

```makefile
VERSION=0.0.1

install: ## 安装依赖
	go mod tidy

installSlient: ## 安装依赖，不输出
	@go mod tidy

list: ## 显示全部依赖
	go list -m all

local-list: ## 显示本地依赖
	go list cmdb/...

ver: ## 打印版本
	echo $(VERSION)
```

## 常用技巧

- 使用 `##` 添加注释
- 使用 `$(变量名)` 引用变量
- 使用 `@` 静音执行命令
