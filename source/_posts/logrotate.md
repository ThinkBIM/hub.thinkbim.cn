---
title: Logrotate uses 100% CPU issue on CentOS
date: 2021-05-20
description: Logrotate在CentOS上使用100%CPU问题
keywords: Logrotate|CentOS上使用100%CPU问题|日志切分
tags:
  - Logrotate
  - Liunx
categories:
  - Liunx
---


## 查看 logrotate.status 文件

```shell
tail /var/lib/logrotate/logrotate.status
```



## 查看文件大小

```
ls /var/lib/logrotate/logrotate.status  -lh
```



## 检查 logrotate 的配置

```
sudo /usr/sbin/logrotate -d /etc/logrotate.conf
```



## cron 任务

```
cat /etc/cron.daily/logrotate
```







