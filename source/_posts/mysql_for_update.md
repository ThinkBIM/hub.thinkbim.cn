---
title: MySQL的FOR UPDATE详解
date: 2024-04-23
description: MySQL的FOR UPDATE详解
keywords: MySQL FORUPDATE
tags:
  - F&Q
categories:
  - MySQL
top_img: false
cover: false
---

用于在事务中锁定选择的数据行，确保在事务结束前其他事务无法修改这些数据



```sql
-- 用户1购买
START TRANSACTION;
SELECT * FROM inventory WHERE product_id = 1001 FOR UPDATE;
-- 检查库存，减少库存
-- ...

-- 用户2购买
START TRANSACTION;
SELECT * FROM inventory WHERE product_id = 1001 FOR UPDATE;
-- 由于用户1已锁定这些行，用户2需要等待
```

