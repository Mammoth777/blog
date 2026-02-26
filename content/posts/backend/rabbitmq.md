---
title: rabbitmq
subtitle: ""
date: 2023-11-20T14:28:43+08:00
categories: []
draft: false
---
## 基本概念

- Server(Broker): 接收客户端连接， 实现AMPQ的实体服务

- Connection: 连接， 客户端和Server的网络连接

- Channel: 网络信道。消息读写的通道。每个channel代表一个会话任务

- Message: C/S之间传输的数据，有`Properties`和`Body`组成

- Properties： 消息的优先级, 延迟等高级特性

- 常用属性 : delivery mode, headers(自定义属性)
- 其他属性

- content_type, content_encoding, priority
- correlation_id : 可以认为是消息的唯一id
- replay_to : 重回队列设定
- expiration : 消息过期时间
- message_id : 消息id
- timestamp, type, user_id, app_id, cluster_id

- Body: 消息体

- Visual Host：逻辑隔离， 多个产线用一个rabbitMQ，就可以用这个做分离

- Exchange： 交换机。用于接收消息， 和根据routing key绑定队列

- Type：direct, topic, fanout, headers

- Direct： 直连（默认exchange）： 当routing key完全匹配， 则消息被投递
- Fanout：扇出：将消息路由给绑定到它身上的所有队列

- 不需要绑定routing key，只要把queue绑在这个exchange上
- 此类型会把消息写到绑定的全部队列上
- 此类型最快

- Topic：队列通过路由键绑定到交换机上，然后，交换机根据消息里的路由值，将消息路由给一个或多个绑定队列（模糊匹配）

- “#” : 匹配一个或多个词
- “*” : 匹配一个词

- Headers： 不常用

- Binding： Exchange和Queue之间的虚拟连接，binding可以包含多个routing key
- Routing Key: 路由规则
- Queue： 也称 Message Queue，用于保存消息和转发给消费者

## 工作模式

通过使用exchange, routing key, queue的不同组合方式， 可以配合出不同的工作模式

1. 点对点（简单）队列（routing key一对一）

- 不需要exchange
- 一个producer ，一个customer

2. 工作队列（公平性）（一对多， 只有一个能收到）

- 不需要exchange
- 一个producer， 多个customer， 但生产的一个消息， 只会给到一个消费者
- 分配方式：todo

3. 发布/订阅（一对多， 都能收到）

- 一个producer， 多个customer
- 每个消费者都有自己的队列
- 生产者吧消息发给exchange
- 每个消费者的队列都绑定到exchange上
- 消息通过交换机传到每个消费者队列

4. 路由

- 生产者发送消息到exchange， 并指定routing key
- exchange根据routing key， 转给消费者队列。
- 消费者队列把routing key绑到exchange上

5. 主题

- 可以理解为带通配符的“路由”模式

参考地址： [https://juejin.cn/post/6844904083875168263](https://juejin.cn/post/6844904083875168263)