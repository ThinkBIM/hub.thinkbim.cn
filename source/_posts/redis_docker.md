---
title: docker-composer 搭建不同模式的redis服务（主从复制、哨兵、Cluster）
date: 2023-01-30
description: docker compose 部署主从复制、哨兵、Cluster三种模式实例
keywords: docker|redis|docker-composer|master|slave
tags:
  - docker-composer
  - Docker
  - Liunx
  - Redis
categories:
  - Redis
top_img:
cover:
---

受限于redis单点性能，配置主从复制的服务


## 主从复制模式


#### 配置
- master
```yaml
# bind 127.0.0.1
port 6379
daemonize no
protected-mode no
repl-diskless-sync no
repl-disable-tcp-nodelay no
requirepass master
```

- slave
```yaml
# bind 127.0.0.1
port 6379
daemonize no
protected-mode no
masterauth master
requirepass slave
replicaof 172.25.0.100 6379
replica-read-only yes
replica-serve-stale-data yes
```
#### 配置参数说明
`bind` 绑定的主机地址
`prot` 监听端口
`daemonize`  启用守护进程
`protected-mode` 保护模式
`masterauth` 当 master 服务设置了密码保护时，slave 服务连接 master 的密码
`requirepass` 设置 Redis 连接密码，如果配置了连接密码，客户端在连接 Redis 时需要通过 AUTH <password> 命令提供密码，默认关闭
`repl-diskless-sync` RDB 文件有以下两种传输方式（是否写入磁盘）
`repl-disable-tcp-nodelay` 是否设置主从之间tcp链接为nodelay.
`replicaof` 设置当本机为 slave 服务时，设置 master 服务的 IP 地址及端口，在 Redis 启动时，它会自动从 master 进行数据同步
`replica-read-only` 是否只读
`replica-serve-stale-data` 当和master失连或者在运行时 replica 是否提供过期数据



#### 目录结构
```
redis
├── docker-compose.yml
├── master
│   ├── data
│   └── redis-master.conf
├── slave1
│   ├── data
│   └── redis-slave1.conf
└── slave2
    ├── data
    └── redis-slave2.conf
```

### docker-composer.yml
```yaml
version: "3"

networks:
  redis-replication:
    driver: bridge
    ipam:
      config:
        - subnet: 172.25.0.0/24

services:
  master:
    image: redis
    container_name: redis-master
    ports:
      - "6370:6379"
    volumes:
      - "./master/redis-master.conf:/etc/redis.conf"
      - "./master/data:/data"
    command: ["redis-server", "/etc/redis.conf"]
    networks:
      redis-replication:
        ipv4_address: 172.25.0.100

  slave1:
    image: redis
    container_name: redis-slave1
    ports:
      - "6371:6379"
    volumes:
      - "./slave1/redis-slave1.conf:/etc/redis.conf"
      - "./slave1/data:/data"
    command: [ "redis-server", "/etc/redis.conf" ]
    networks:
      redis-replication:
        ipv4_address: 172.25.0.101

  slave2:
    image: redis
    container_name: redis-slave2
    ports:
      - "6372:6379"
    volumes:
      - "./slave2/redis-slave2.conf:/etc/redis.conf"
      - "./slave2/data:/data"
    command: [ "redis-server", "/etc/redis.conf" ]
    networks:
      redis-replication:
        ipv4_address: 172.25.0.102
```


## Sentinel哨兵模式

## Cluster模式




`redis.conf文件中的daemonize参数为yes导致，修改 `/etc/redis.conf` 中的daemonize 为no 重启redis问题`
`解决docker 本身就是后台运行的，daemonize为yes两者会冲突`

## 参考
> https://juejin.cn/post/6997804248457019399
> https://developer.aliyun.com/article/641767

