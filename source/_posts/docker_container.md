---
title: Docker容器常用命令-container
date: 2021-06-22
description: Docker常用命令
keywords: Docker|命令|container|容器
tags:
  - command 
categories:
  - Docker
---


## exec

在运行的容器中执行命令

### 命令格式
```shell
docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
```

### 常用参数

- **-d** 分离模式: 在后台运行

- **-i** 即使没有附加也保持STDIN 打开

- **-t** 分配一个伪终端

### 使用示例

```shell
# 指定容器名称
docker exec -it webserver /bin/bash

# 指定容器ID
docker exec -it 9df70f9a0714 /bin/bash
```



## ps

列出容器

### 命令格式

```shell
docker ps [OPTIONS]
```

### 常用参数

- **-a :** 显示所有的容器，包括未运行的。

- **-f :** 根据条件过滤显示的内容。

- **--format :** 指定返回值的模板文件。

- **-l :** 显示最近创建的容器。

- **-n :** 列出最近创建的n个容器。

- **--no-trunc :** 不截断输出。

- **-q :** 静默模式，只显示容器编号。

- **-s :** 显示总的文件大小。

### 使用示例

```shell
# 显示运行中的容器
docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
531d1da7106a        nginx               "/docker-entrypoint.…"   10 hours ago        Up 34 minutes       0.0.0.0:8000->80/tcp   webserver

# 显示所有容器
docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                   PORTS                  NAMES
531d1da7106a        nginx               "/docker-entrypoint.…"   10 hours ago        Up 34 minutes            0.0.0.0:8000->80/tcp   webserver
d71dcdf7c42b        docker101tutorial   "/docker-entrypoint.…"   8 weeks ago         Exited (0) 6 weeks ago                          docker-tutorial

```

### 返回说明

**CONTAINER ID:** 容器 ID。

**IMAGE:** 使用的镜像。

**COMMAND:** 启动容器时运行的命令。

**CREATED:** 容器的创建时间。

**STATUS:** 容器状态。

状态有7种：

- created（已创建）

- restarting（重启中）

- running（运行中）

- removing（迁移中）

- paused（暂停）

- exited（停止）

- dead（死亡）

**PORTS:** 容器的端口信息和使用的连接类型（tcp\udp）。

**NAMES:** 自动分配的容器名称

## run

创建一个新的容器并运行一个命令

### 命令格式

```shell
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

### 常用参数

- **-a stdin:** 指定标准输入输出内容类型，可选 STDIN/STDOUT/STDERR 三项；

- **-d:** 后台运行容器，并返回容器ID；

- **-i:** 以交互模式运行容器，通常与 -t 同时使用；

- **-P:** 随机端口映射，容器内部端口随机映射到主机的端口

- **-p:** 指定端口映射，格式为：主机(宿主)端口:容器端口

- **-t:** 为容器重新分配一个伪输入终端，通常与 -i 同时使用；

- **--name="nginx-lb":** 为容器指定一个名称；

- **--dns 8.8.8.8:** 指定容器使用的DNS服务器，默认和宿主一致；

- **--dns-search example.com:** 指定容器DNS搜索域名，默认和宿主一致；

- **-h "mars":** 指定容器的hostname；

- **-e username="ritchie":** 设置环境变量；

- **--env-file=[]:** 从指定文件读入环境变量；

- **--cpuset="0-2" or --cpuset="0,1,2":** 绑定容器到指定CPU运行；

- **-m :** 设置容器使用内存最大值；

- **--net="bridge":** 指定容器的网络连接类型，支持 bridge/host/none/container: 四种类型；

- **--link=[]:** 添加链接到另一个容器；

- **--expose=[]:** 开放一个端口或一组端口；

- **--volume , -v:** 绑定一个卷

### 使用示例

```shell
docker run hello-world
docker run --name mywebserver -it nginx

#后台运行 -d 
docker run --name mywebserver -itd nginx
#指定端口，后台运行
docker run --name webserver -p 8000:80 -itd nginx
86da2b0476d5eac511d70c19efdd49fd4774ab3e415eceb84a3e77074ff7994f

#查看绑定端口
docker port webserver
80/tcp -> 0.0.0.0:8000

#link
```

> 如果build启动服务，-itd 后台运行 exec 进入容器

```shell
#进入容器，退出自动删除容器
docker run -it --rm --name mynginx mynginx:v2 bash
```

## rm

在运行的容器中执行命令

### 命令格式
```shell
docker rm [OPTIONS] CONTAINER [CONTAINER...]
```

### 常用参数

- **-f :** 通过 SIGKILL 信号强制删除一个运行中的容器。

- **-l :** 移除容器间的网络连接，而非容器本身。

- **-v :** 删除与容器关联的卷。

### 使用示例

```shell
# 指定名称
docker rm mywebserver
# 指定ID
docker rm e6ede0e117ab

#强制删除容器 db01、db02
docker rm -f db01 db02
```



## top

查看容器中运行的进程信息，支持 ps 命令参数

### 命令格式

```shell
docker top [OPTIONS] CONTAINER [ps OPTIONS]
```


### 使用示例

```shell
docker top webserver
PID                 USER                TIME                COMMAND
1704                root                0:00                nginx: master process nginx -g daemon off;
1755                101                 0:00                nginx: worker process
docker top webserver 1755
PID                 USER                TIME                COMMAND
1704                root                0:00                nginx: master process nginx -g daemon off;
1755                101                 0:00                nginx: worker process

```





## export

将文件系统作为一个tar归档文件导出到STDOUT，本地归档

### 命令格式

```shell
docker export [OPTIONS] CONTAINER
```

### 常用参数

- ** :** 将输入内容写到文件

### 使用示例

```text
docker export -o webserver.tar webserver
ls
Dockerfile    webserver.tar
```

## port

列出指定的容器的端口映射，或者查找将PRIVATE_PORT NAT到面向公众的端口


### 使用示例

```shell
docker port webserver
80/tcp -> 0.0.0.0:8000

```

## logs

获取容器的日志

### 命令格式

```shell
docker logs [OPTIONS] CONTAINER
```

### 常用参数

- **-f :** 跟踪日志输出

- **--since :** 显示某个开始时间的所有日志

- **-t :** 显示时间戳

- **--tail :** 仅列出最新N条容器日志

### 使用示例

```shell
docker logs webserver
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
172.17.0.1 - - [20/Oct/2020:15:59:52 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.80 Safari/537.36" "-"
172.17.0.1 - - [20/Oct/2020:16:15:39 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.80 Safari/537.36" "-"
172.17.0.1 - - [20/Oct/2020:16:15:42 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.80 Safari/537.36" "-"
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: error: IPv6 listen already enabled
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
```

## kill

杀掉一个运行中的容器

### 命令格式

```shell
docker kill [OPTIONS] CONTAINER [CONTAINER...]
```

### 使用示例

```shell
docker kill webserver
```





## cp

用于容器与主机之间的数据拷贝

### 命令格式

```shell
docker diff [OPTIONS] CONTAINER
```


### 使用示例

```text
# 本地复制到容器
docker cp /etc/hosts webserver:/tmp/
# 容器复制到本地
docker cp webserver:/tmp/hosts ./
```



## commit

从容器创建一个新的镜像

### 命令格式
```shell
docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
```

### 常用参数

- **-a :** 提交的镜像作者；

- **-c :** 使用Dockerfile指令来创建镜像；

- **-m :** 提交时的说明文字；

- **-p :** 在commit时，将容器暂停。

### 使用示例

```shell
docker commit -a 'xx' -m 'xxx' webserver webserver:v1
sha256:a3038edc18d1fe39c43ff90c5ac765bd9b1246ff4b03a430c95651e94d38df2a
docker history webserver
Error response from daemon: No such image: webserver:latest
docker history webserver:vq
Error response from daemon: No such image: webserver:vq
docker history webserver:v1
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
a3038edc18d1        19 seconds ago      nginx -g daemon off;                            2.23kB              xxx
f35646e83998        7 days ago          /bin/sh -c #(nop)  CMD ["nginx" "-g" "daemon…   0B                  
```



## diff

检查容器里文件结构的更改

### 命令格式

```shell
docker diff [OPTIONS] CONTAINER
```


### 使用示例

```bash
docker diff webserver
C /tmp
A /tmp/hosts
C /run
```



## rename

重命名容器

### 命令格式
```shell
docker rename CONTAINER NEW_NAME
```


### 使用示例

```shell
docker rename mywebserver webserver
```



## inspect

获取容器/镜像的元数据

### 命令格式
```shell
docker inspect [OPTIONS] NAME|ID [NAME|ID...]
```

### 常用参数

- **-f :** 指定返回值的模板文件

- **-s :** 显示总的文件大小

- **--type :** 为指定类型返回JSON

### 使用示例

:::details inspect

```shell
docker inspect webserver
[
    {
        "Id": "531d1da7106a9b436f826e48ea213f251510edcc1b4e8e22d1b7ed2abca86996",
        "Created": "2020-10-20T15:59:22.7661026Z",
        "Path": "/docker-entrypoint.sh",
        "Args": [
            "nginx",
            "-g",
            "daemon off;"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 1704,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2020-10-21T01:43:28.0403569Z",
            "FinishedAt": "2020-10-20T16:17:30.9283364Z"
        },
        "Image": "sha256:f35646e83998b844c3f067e5a2cff84cdf0967627031aeda3042d78996b68d35",
        "ResolvConfPath": "/var/lib/docker/containers/531d1da7106a9b436f826e48ea213f251510edcc1b4e8e22d1b7ed2abca86996/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/531d1da7106a9b436f826e48ea213f251510edcc1b4e8e22d1b7ed2abca86996/hostname",
        "HostsPath": "/var/lib/docker/containers/531d1da7106a9b436f826e48ea213f251510edcc1b4e8e22d1b7ed2abca86996/hosts",
        "LogPath": "/var/lib/docker/containers/531d1da7106a9b436f826e48ea213f251510edcc1b4e8e22d1b7ed2abca86996/531d1da7106a9b436f826e48ea213f251510edcc1b4e8e22d1b7ed2abca86996-json.log",
        "Name": "/webserver",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {
                "80/tcp": [
                    {
                        "HostIp": "",
                        "HostPort": "8000"
                    }
                ]
            },
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "Capabilities": null,
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "KernelMemory": 0,
            "KernelMemoryTCP": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/42902b2f7fed18c296c035b20b6c526a0ec3c5f566f48bbdba851c272d8138d4-init/diff:/var/lib/docker/overlay2/58ed84f3691674f7f7c7f99ea4252eda0200c8161cb455a0251204c8507ed25b/diff:/var/lib/docker/overlay2/0a7d19be8978f302b7d3224fb363679fb8c218fae422da9f95464d41169c0b3c/diff:/var/lib/docker/overlay2/6c088bb628ab7820b0d0d6d95cd03f1f3999114da446c513b5f5014e6583a0fa/diff:/var/lib/docker/overlay2/24932a2ad99af3baac795cd7c151d914b0db8843d4097d0bacd7eb7dea89343e/diff:/var/lib/docker/overlay2/f2ab2e434f230a0227dc277e3a6e3141e2c560b183bcb432a624072f4cabc4cf/diff",
                "MergedDir": "/var/lib/docker/overlay2/42902b2f7fed18c296c035b20b6c526a0ec3c5f566f48bbdba851c272d8138d4/merged",
                "UpperDir": "/var/lib/docker/overlay2/42902b2f7fed18c296c035b20b6c526a0ec3c5f566f48bbdba851c272d8138d4/diff",
                "WorkDir": "/var/lib/docker/overlay2/42902b2f7fed18c296c035b20b6c526a0ec3c5f566f48bbdba851c272d8138d4/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "531d1da7106a",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "80/tcp": {}
            },
            "Tty": true,
            "OpenStdin": true,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NGINX_VERSION=1.19.3",
                "NJS_VERSION=0.4.4",
                "PKG_RELEASE=1~buster"
            ],
            "Cmd": [
                "nginx",
                "-g",
                "daemon off;"
            ],
            "Image": "nginx",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": [
                "/docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {
                "maintainer": "NGINX Docker Maintainers <docker-maint@nginx.com>"
            },
            "StopSignal": "SIGTERM"
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "039b5861e5a286e6f4c2f545703fd35d75a7fd1676305692344818db40d58630",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {
                "80/tcp": [
                    {
                        "HostIp": "0.0.0.0",
                        "HostPort": "8000"
                    }
                ]
            },
            "SandboxKey": "/var/run/docker/netns/039b5861e5a2",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "95aa24006b353356739ee27db494c787bc8ddb669ac06934f71fb17ac1a6fdb8",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "248f83eea2e6ec52b9e7218be989a2fce09365fe57fdb9c7ce0af6f52ec2cc5a",
                    "EndpointID": "95aa24006b353356739ee27db494c787bc8ddb669ac06934f71fb17ac1a6fdb8",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:02",
                    "DriverOpts": null
                }
            }
        }
    }
]



# 查看容器IP
docker inspect --format='{{.NetworkSettings.IPAddress}}' myMysql

```
:::

## stats

显示容器使用的资源信息

### 命令格式
```shell
docker stats [OPTIONS] [CONTAINER...]
```

### 使用示例

```shell
#每秒执行一次
docker stats mywebserver

CONTAINER ID        NAME                CPU %               MEM USAGE / LIMIT     MEM %               NET I/O             BLOCK I/O           PIDS
69600e5663f0        mywebserver         0.00%               1.887MiB / 1.945GiB   0.09%               1.05kB / 0B         0B / 0B             2

```



## pause/unpause

- **docker pause** :暂停容器中所有的进程。

- **docker unpause** :恢复容器中所有的进程。

### 命令格式

```shell
docker pause [OPTIONS] CONTAINER [CONTAINER...]
docker unpause [OPTIONS] CONTAINER [CONTAINER...]
```

### 使用示例

```shell
#暂停
docker pause webserver

#恢复
docker unpause webserver
```

## start/stop/restart

- **start** :启动一个或多个已经被停止的容器
- **stop** :停止一个运行中的容器
- **restart** :重启容器

### 命令格式

```shell
docker start [OPTIONS] CONTAINER [CONTAINER...]
docker stop [OPTIONS] CONTAINER [CONTAINER...]
docker restart [OPTIONS] CONTAINER [CONTAINER...]
```

### 常用参数



### 使用示例

```shell
#启动已被停止的容器
docker start webserver

#停止运行中的容器
docker stop webserver

#重启容器webserver
docker restart webserve
```





