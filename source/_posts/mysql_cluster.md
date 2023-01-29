---
title: mysql-5.7数据库主从复制
date: 2021-07-22
description: mysql-5.7数据库主从复制
keywords: LEFT JOIN查询
tags:
  - 主从
categories:
  - MySQL
  - Docker
---

## master
mkdir -p /usr/local/docker-data/master
cd /usr/local/docker-data/master
mkdir conf data
chmod 777 * -R
cd /usr/local/docker-data/master/conf

- my.cnf
```
log-bin=mysql-bin #开启二进制日志
server-id=1 #服务id，不可重复

docker run -itd --name mysql_master \
-v /usr/local/docker-data/master/data:/var/lib/mysql 
-v /usr/local/docker-data/master/conf:/etc/my.cnf.d 
-p 3306:3306 -e MYSQL_ROOT_PASSWORD='abcd!234' percona
```

#  创建用户授权
create user 'slave'@'%' identified by 'abcd!234';
grant replication slave on *.* to 'slave'@'%';
flush privileges;

#查看master状态
show master status;
#查看二进制日志相关的配置项
show global variables like 'binlog%';
#查看server相关的配置项
show global variables like 'server%';

## slave
mkdir -p /usr/local/docker-data/slave
cd /usr/local/docker-data/slave
mkdir conf data
chmod 777 * -R
cd /usr/local/docker-data/slave/conf
vim my.cnf
#   -----
[mysqld]
log-bin=mysql-bin #开启二进制日志
server-id=2 #服务id，不可重复
#   ----
docker run -itd --name slave -v /usr/local/docker-data/slave/data:/var/lib/mysql -v /usr/local/docker-data/slave/conf:/etc/my.cnf.d -p 3307:3306 -e MYSQL_ROOT_PASSWORD='abcd!234' percona

#设置master相关信息
CHANGE MASTER TO
master_host='192.168.137.133',
master_user='slave',
master_password='abcd!234',
master_port=3306,
master_log_file='mysql-bin.000003',
master_log_pos=749;
#启动同步
START slave;
#查看master状态
show slave status;
