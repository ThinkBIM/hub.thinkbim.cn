---
title: Redis数据结构详解
date: 2023-02-06 10:34:49
description:
keywords:
tags:
  - Redis
categories:
  - Redis
top_img: false
cover: false
---

## Redis有哪些数据结构。list和set有什么区别?set和zset呢?zset的底层实现

## String（字符串）对象、
## List（列表）对象、
## Hash（哈希）对象、
## Set（集合）对象 
## Zset（有序集合）
## Stream (流)

## 概念
SDS
    len 字符长度
    alloc 分配空间长度
    flags sds类型
    buf[] 字节数组

ziplist(压缩列表)
quicklist(快速链表)双向链表
hash 哈希表
inset 数据整合
skiplist 跳表
listpack 紧凑列表

### 事务
multi
exec
discard

# 参考
> https://www.cnblogs.com/xiaolincoding/p/15628854.html
> https://www.cnblogs.com/xiaolincoding/p/15628854.html