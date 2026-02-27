---
title: "Docker 国内镜像源"
date: 2023-11-20
categories: ["运维", "Docker"]
draft: false
---

## 国内 Docker 镜像源

```sh
# 这个源好用
docker.m.daocloud.io
```

## 使用方法

在拉取镜像时替换默认的 Docker Hub 地址：

```bash
# 原始方式
docker pull nginx

# 使用镜像源
docker pull docker.m.daocloud.io/nginx
```

## 配置 Docker 守护进程

编辑 `/etc/docker/daemon.json`（Linux）或 Docker Desktop 设置（Mac/Windows）：

```json
{
  "registry-mirrors": [
    "https://docker.m.daocloud.io"
  ]
}
```

重启 Docker 服务：

```bash
sudo systemctl restart docker
```
