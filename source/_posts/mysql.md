---
title: LEFT JOIN 查询结果不是左表的全部数据的解决方法
date: 2021-07-22
description: 查询结果不是左表的全部数据的解决方法
keywords: LEFT JOIN查询
tags:
  - F&Q
categories:
  - MySQL
top_img: false
cover: false
---

## LEFT JOIN  查询结果不是左表的全部数据的解决方法

> 常见以下查询，但是发现查询结果A表的数据不是全部数据？
```sql
SELECT
    a.id b.id,
	...
FROM
	A a
	LEFT JOIN B b ON a.id = b.id
WHERE
    a.name = 'xxx'
  AND b.name = 'xxx'
```

> 如果过滤条件是A表的字段  例如：a.xx = 'xxx'

```sql
SELECT
    a.id b.id,
	...
FROM
	A a
	LEFT JOIN B b ON a.id = b.id
WHERE
    a.name = 'xxx'
```

> 如果过滤的是B表的字段  例如：b.xx = 'xxx'

```sql
SELECT
    a.id b.id,
	...
FROM
	A a
	LEFT JOIN B b ON a.id = b.id AND b.name='xxx'
```

> 如果同时过滤2个表的字段

```sql
SELECT
	a.id b.id,
	...
FROM
	A a
	LEFT JOIN B b ON a.id = b.id AND b.NAME = 'xxx'
WHERE
	a.NAME = 'xxx' 
```