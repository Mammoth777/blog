---
title: mysql
subtitle: ""
date: 2024-11-20T01:48:53+08:00
categories: []
draft: false
---
## 客户端

### 1. 登录

1. `mysql -h localhost -P 3306 -u root -p`
2. 会提示输入password： 输入密码

### 2. 创建账号

`create user 'tester' identified by '123456'`

### 3. 操作database

- 展示全部库： `show databases;`
- 创建： `create database test;`
- 进入库： `use test;`

### 4. 操作table

#### 4.1 创建表

```
create table if not exists student(
  id int not null auto_increment comment'主键自增id',
  name char(10) not null comment'姓名',
  addr varchar(100) default '' comment'地址',
  primary key(id),
  unique key idx_name(name),  -- 唯一索引
  key idx_location(province,city) -- 普通索引， 联合索引
)
```

**Tip**: `char`和`varchar`的区别： 。。

#### 索引

- 没加索引， 查的时候需要遍历整张表
- 加了索引， 会基于索引，建立查找树

- 联合索引： `where`的时候， 总是会联合查询两个字段， 就要用联合索引

#### 4.2 插入数据

```
insert into student(name,province,city,enrollment) values
('张三','北京','北京','2002-02-04')
('李四','北京','北京','2002-02-04')
('王五','北京','北京','2002-02-04')
```

#### 4.3 查询

```
select id,name from student where id>1;
```

```
select province,avg(score) as avg_score from student
where score>0
group by province having avg_score>50
order by avg_score desc
```

#### 4.4 修改

```
update student set
score=score+10,addr='海淀'
where province='北京'
```

```
update
  student set 
  score= case province
    when '北京' then score+10
    when '四川' then score+5
    else score+7
  end,
  addr= case provice
    when '北京' then '东城区'
    when '四川' then '幸福里'
    else '朝阳区'
  end
 where id > 0
```

#### 4.5 删除

- 删除一行 `delete from student where city = '郑州'`
- 删除全部行 `delete from student`
- 删除表 `drop table student`

#### 4.6 替换

因为`id`是唯一索引， 所以会根据id去replace

```
REPLACE INTO edge (id, name, created_by) VALUES ("11", "EEE", "张三呀")
```

## 最佳实践

建议

- 写sql用小写
- 建表时先判断表是否已存在 `if not exists`
- 所有的列和表都加comment
- 字符串长短比较短的时候， 尽量使用char， 定长有利于内存对齐， 读写性能更好， varchar字段频繁修改时， 容易引起内存碎片
- 满足需求的前提下， 尽量使用短的数据类型， 如tinyint vs int， float vs double， date vs datetime

## 索引

### B+树

1. B即Balance， 对于m叉树，每个节点上有最多m个数据，最少有m/2个数据（根节点除外）
2. 叶节点上存储了所有数据， 把叶节点连接起来可以顺序遍历所有数据
3. 每个节点设计成内存页的整倍数， mysql的m=1200， 树的前两层放在内存中

tip： **内存页**是一块内存，具体的，百度吧。

- Mysql的索引默认使用B+树
- 主键默认佳索引
- 联合索引的前缀同样具有索引效果
- sql语句前加explain可以查看索引使用情况
- 如果mysql没有选择最有的索引方案， 可以在where前force index（index_name）

### 规避慢查询

常规查询，最好在100ms之内， 超出我们可以认为是慢查询（个人定义）

- 大部分的慢查询都是因为没有正确使用索引
- 一次select不要超过1000行
- 分页查询`limit m,n`会检索前`m+n`行， 只是返回后`n`行， 通常用`id>x`来代替这种分页方式
- 批量操作时最好一条sql语句搞定；其次打包成一个事务， 一次性提交（高并发情况下减少对共享资源的争用）
- 不要使用连表操作， join逻辑在业务代码里完成

## 驱动