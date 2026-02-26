---
title: redis
subtitle: ""
date: 2023-11-20T14:29:42+08:00
categories: []
draft: false
---
## 客户端启动

`redis-cli`

```
redis-cli
ping
> PONG
```

远程: `redis-cli -h host -p -a password`

## Key相关

- `set key value`
- `del key`
- `dump key`序列化, 返回被序列化的值
- `exists key`
- `expire key`设置过期时间, 到期删除
- ``