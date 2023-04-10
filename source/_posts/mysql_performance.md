---
title: MySQL性能优化
date: 2023-02-13 10:37:05
description:
keywords:
tags:
  - MySQL
categories:
  - MySQL
top_img:
cover:
---


# 性能监控

## SHOW PROFILE [TYPE] 
`TYPE`可以指定 可选值以显示特定的附加类型的信息：
- `ALL` 显示所有信息
- `BLOCK` IO显示块输入和输出操作的计数
- `CONTEXT` SWITCHES显示自愿和非自愿上下文切换的计数
- `CPU` 显示用户和系统 CPU 使用时间
- `IPC` 显示发送和接收的消息计数
- `MEMORY` 目前没有实施
- `PAGE FAULTS` 显示主要和次要页面错误的计数
- `SOURCE` 显示源代码中函数的名称，以及函数所在文件的名称和行号
- `SWAPS` 显示交换计数

### 查看&设置profile
```sql
SELECT @@profiling;
SET profiling = 1;
```

```sql
SHOW PROFILES;

+----------+------------+----------------------------+
| Query_ID | Duration   | Query                      |
+----------+------------+----------------------------+
|        1 | 0.00046300 | select * from  data_user   |
|        2 | 0.00018600 | select * from  wechat_keys |
|        3 | 0.00025300 | select * from  wechat_keys |
+----------+------------+----------------------------+
```

```sql
SHOW PROFILE FOR QUERY 2;

+----------------------+----------+
| Status               | Duration |
+----------------------+----------+
| starting             | 0.000035 |
| checking permissions | 0.000006 |
| Opening tables       | 0.000013 |
| init                 | 0.000019 |
| System lock          | 0.000007 |
| optimizing           | 0.000004 |
| statistics           | 0.000009 |
| preparing            | 0.000021 |
| executing            | 0.000002 |
| Sending data         | 0.000032 |
| end                  | 0.000004 |
| query end            | 0.000005 |
| closing tables       | 0.000005 |
| freeing items        | 0.000015 |
| cleaning up          | 0.000009 |
+----------------------+----------+
```

> 未来的 MySQL 版本中被删除。改用 performance_schema（性能模式）

## performance_schema
Performance Schema 维护用于收集当前和最近的语句事件的表，并将该信息聚合在摘要表中。
性能模式语句事件表 描述了语句摘要所基于的事件。
有关语句事件的内容、当前和历史语句事件表以及如何控制语句事件收集的信息

### 数据库中表的分组

1. `设置表` 这些表用于配置和显示监控特性。
2. `当前事件表` 该 events_waits_current表包含每个线程的最新事件。其他类似的表包含事件层次结构不同级别的当前事件：events_stages_current 阶段事件、 events_statements_current语句事件和 events_transactions_current事务事件。
3. `历史表` 这些表与当前事件表具有相同的结构，但包含更多行。例如，对于等待事件，events_waits_history 表包含每个线程最近的 10 个事件。 events_waits_history_long 包含最近的 10,000 个事件。阶段、语句和交易历史存在其他类似的表。
    要更改历史表的大小，请在服务器启动时设置适当的系统变量。例如，要设置等待事件历史表的大小，请设置 performance_schema_events_waits_history_size 和 performance_schema_events_waits_history_long_size。
4. `汇总表` 这些表包含通过事件组聚合的信息，包括那些已从历史表中丢弃的信息。
5. `实例表` 这些表记录了检测的对象类型。被检测对象在被服务器使用时会产生一个事件。这些表提供了事件名称和解释性说明或状态信息。
6. `杂表` 这些不属于任何其他表组

### 配置
查看是否开启
```sql
SHOW VARIABLES LIKE 'performance_schema';
```
my.cnf配置文件，开启performance_schema
```yaml
[mysqld]
performance_schema=ON
```
打开等待事件的采集器和保存表的配置
```sql
UPDATE setup_instruments SET ENABLED="YES",TIMED="YES" WHERE name LIKE "wait%";
UPDATE setup_consumers SET ENABLED="YES" where `NAME` like "%wait%";
```

### events_waits_current
它包含每个线程一行，显示每个线程最近监视的事件。当前事件等待

`THREAD_ID` 事件编号
`EVENT_ID` 
`END_EVENT_ID` 此列设置为NULL事件开始时，并在事件结束时更新为线程当前事件编号
EVENT_NAME 
`SOURCE` 源文件的名称，其中包含生成事件的检测代码以及检测发生的文件中的行号
`TIMER_START` 事件开始时间
`TIMER_END` 事件结束时间
`TIMER_WAIT` 事件花费时间
SPINS NULL
OBJECT_SCHEMA NULL
OBJECT_NAME NULL
INDEX_NAME NULL
OBJECT_TYPE NULL
OBJECT_INSTANCE_BEGIN 140464909592968
NESTING_EVENT_ID 2934
NESTING_EVENT_TYPE STATEMENT
`OPERATION` 执行的操作类型，例如 lock、read或 write
NUMBER_OF_BYTES NULL
FLAGS NULL

### 实践操作
## events_statements_summary_by_digest
> https://dev.mysql.com/doc/refman/8.0/en/performance-schema-statement-summary-tables.html


## show processlist
查看连接线程数量
```sql
show processlist;

+----+------+-----------+--------+---------+------+----------+------------------+
| Id | User | Host      | db     | Command | Time | State    | Info             |
+----+------+-----------+--------+---------+------+----------+------------------+
| 69 | root | localhost | sakila | Query   |    0 | starting | show processlist |
+----+------+-----------+--------+---------+------+----------+------------------+
```

`Id` 连接标识符
`User` MySQL 用户
`Host` 客户端的主机名
`db` 线程的默认数据库，或者 NULL如果未选择任何数据库。
`Command` 线程代表客户端执行的命令类型
`Time` 状态的时间（以秒为单位）
`State` 执行状态
`Info` 线程正在执行的语句

> https://github.com/alibaba/druid/wiki/Druid连接池介绍#1-什么是druid连接池





# 参考
> https://dev.mysql.com/doc/refman/8.0/en/performance-schema-events-waits-current-table.html