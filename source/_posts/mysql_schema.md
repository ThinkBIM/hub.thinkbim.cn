---
title: schema与数据类型优化
date: 2023-02-13 15:11:11
description:
keywords:
tags:
  - MySQL
categories:
  - MySQL
top_img: false
cover: false
---

# 数据类型的优化
1. 设计合适的数据类型，更小的数据通常更快
2. 简单数据类型的操作需要更少的CPU周期（整型比字符串、日期时间、IP地址）
3. 尽量避免使用null
4. 实际细则

date 3个字节 
timestamp 4个字节
枚举

# 合理使用范式和反范式


# 主键的选择
代理主键
自然主键
主键生成器


# 字符集的选择


# 存储引擎的选择

# 适当的数据冗余

# 适当拆分
垂直拆分 按照不同业务进行拆分，
水平拆分 按照1-1000，10001-20000

