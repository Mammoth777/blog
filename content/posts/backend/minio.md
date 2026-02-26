---
title: minio
subtitle: ""
date: 2023-11-20T06:32:24+08:00
categories:
  - server
draft: false
---
对于中小企业, 如果不选择存储上云, 那么Minio是不错的选择.

minio可以直接作为对象存储使用, 也可以作为云上对象存储服务的网关层. 无缝对接到Amazon S3, MicroSoft Azure.

## 优点

- 部署简单
- 支持海量存储, 单个对象最大5Tb
- 兼容Amazon S3接口
- 低冗余切磁盘损坏高容忍
- 读写性能好

## 基本概念

- **Object**: 存储到minio的基本对象, 就是文件
- **Bucket**: 用来存储Object的逻辑空间. 每个Bucket之间的数据相互隔离. 对于客户端来说, 是存放文件的顶层文件夹
- **Drive**: 存储数据的磁盘, 在Minio启动时, 以参数的方式传入. Minio中的所有对象都会存储在drive中
- **Set:** 一组Drive的集合. 分布式部署根据集群规模自动划分一个或多个Set, 每个Set中Drive分布在不同位置. 一个对象存储在一个Set上

参考: [https://xie.infoq.cn/article/66ffc331f851f5873a3e1b2d3](https://xie.infoq.cn/article/66ffc331f851f5873a3e1b2d3)


## 快速启动
参考 [docker hub minio](https://hub.docker.com/r/minio/minio)

```bash
docker run -p 9000:9000 -p 9001:9001 quay.io/minio/minio server /data --console-address ":9001"
```