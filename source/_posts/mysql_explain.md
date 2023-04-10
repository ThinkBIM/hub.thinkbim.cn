---
title: MySQL执行计划 explain详解
date: 2023-02-13 23:18:16
description:
keywords: MySQL查询执行计划|EXPLAIN计划
tags:
  - MySQL
  - explain
categories:
  - MySQL
top_img:
cover:
---

根据您的表、列、索引和WHERE子句中的条件的详细信息，
MySQL 优化器考虑了许多技术来有效地执行 SQL 查询中涉及的查找。
可以在不读取所有行的情况下执行对巨大表的查询；
可以在不比较行的每个组合的情况下执行涉及多个表的连接。
优化器选择执行最高效查询的一组操作称为“查询执行计划”，也称为 EXPLAIN计划。

```sql
explain select * from table;
```
# 参数说明

## id
select查询的序列号，包含一组数字，表示查询中执行select子句或者操作表的顺序
1. 如果id相同，那么执行顺序从上到下
2. 如果id不同，如果是子查询，id的序号会递增，id值越大优先级越高，越先被执行
3. id相同和不同的，同时存在：相同的可以认为是一组，从上往下顺序执行，在所有组中，id值越大，优先级越高，越先执行

## select_type
主要用来分辨查询的类型，是普通查询还是联合查询还是子查询

|                       |                                                     |
|-----------------------|-----------------------------------------------------|
| SIMPLE                | 	简单的 select 查询,查询中不包含子查询或者UNION                     |
| PRIMARY	              | 	查询中若包含任何复杂的子部分，最外层查询则被标记为Primary                   |
| UNION	                | 	SELECT中的 第二个或后面的语句UNION                            |
| DEPENDENT UNION	      | 	a 中的第二个或后面的SELECT语句 UNION，取决于外部查询                  |
| UNION RESULT	         | 	的结果UNION。                                          |
| `SUBQUERY`	           | 	在SELECT或WHERE列表中包含了子查询                             |
| DEPENDENT SUBQUERY	   | 	首先SELECT在子查询中，依赖于外部查询                              |
| DERIVED	              | 	派生表，该临时表是从子查询派生出来的，位于form中的子查询                     |
| DEPENDENT DERIVED	    | 	派生表依赖于另一个表                                         |
| MATERIALIZED	         | 	物化子查询                                              |
| UNCACHEABLE SUBQUERY	 | 	无法缓存结果且必须为外部查询的每一行重新评估的子查询                         |
| UNCACHEABLE UNION	    | 	UNION 属于不可缓存子查询的 第二个或后面的选择（参见UNCACHEABLE SUBQUERY） |




## table
对应行正在访问哪一个表，表名或者别名

## partitions
查询将匹配记录的分区。该值NULL适用于非分区表

## type
显示的是访问类型以何种方式去访问我们的数据，最容易想的是全表扫描，
直接暴力的遍历一张表去寻找需要的数据，效率非常低下
效率从最好到最坏依次是
`system` > `const` > eq_ref > `ref` > fulltext > ref_or_null > index_merge > unique_subquery > index_subquery > `range` > `index` > `ALL`
一般情况下，得保证查询至少达到range级别，最好能达到ref

## possible_keys
显示可能应用在这张表中的索引，一个或多个，查询涉及到的字段上若存在索引，则该索引将被列出，但不一定被查询实际使用

## key
实际使用的索引，如果为null，则没有使用索引，查询中若使用了覆盖索引，则该索引和查询的select字段重叠。

## key_len
表示索引中使用的字节数，可以通过key_len计算查询中使用的索引长度，在不损失精度的情况下长度越短越好。

## ref
显示索引的哪一列被使用了，如果可能的话，是一个常数

## rows
根据表的统计信息及索引使用情况，大致估算出找出所需记录需要读取的行数，此参数很重要，直接反应的sql找了多少数据，在完成目的的情况下越少越好

## filtered
该filtered列指示按表条件过滤的表行的估计百分比。

## Extra
包含额外的信息


# 参考
> https://dev.mysql.com/doc/refman/5.5/en/explain-output.html