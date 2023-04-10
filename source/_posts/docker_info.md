---
title: Docker常用命令-info
date: 2021-06-20 18:49:36
description: docker常用命令
keywords: Docker|命令|info
tags:
  - Command
categories:
  - Docker
---
Docker 是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的镜像中，然后发布到任何流行的 Linux或Windows 机器上，也可以实现虚拟化。容器是完全使用沙箱机制，相互之间不会有任何接口

- [Docker](https://www.docker.com/) 官网
- [Doc](https://docs.docker.com/) 文档
- [Hub](https://hub.docker.com/) Hub

# Docker入门

## info

显示 Docker 系统信息，包括镜像和容器数

### 命令格式

docker info [OPTIONS]

### 常用参数



### 使用实例



```shell
docker info
Client:
 Debug Mode: false

Server:
 Containers: 1
  Running: 0
  Paused: 0
  Stopped: 1
 Images: 29
 Server Version: 19.03.13
 Storage Driver: overlay2
  Backing Filesystem: extfs
  Supports d_type: true
  Native Overlay Diff: true
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
 Swarm: inactive
 Runtimes: runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 8fba4e9a7d01810a393d5d25a3621dc101981175
 runc version: dc9208a3303feef5b3839f4323d9beb36df0a9dd
 init version: fec3683
 Security Options:
  seccomp
   Profile: default
 Kernel Version: 4.19.76-linuxkit
 Operating System: Docker Desktop
 OSType: linux
 Architecture: x86_64
 CPUs: 2
 Total Memory: 1.945GiB
 Name: docker-desktop
 ID: QTGW:P4FS:GJ7T:ZC3F:RRFB:ACDX:YYE5:TOPG:4GSQ:FFM5:6GFM:3CEN
 Docker Root Dir: /var/lib/docker
 Debug Mode: true
  File Descriptors: 39
  Goroutines: 46
  System Time: 2020-10-16T01:27:03.542085876Z
  EventsListeners: 3
 HTTP Proxy: gateway.docker.internal:3128
 HTTPS Proxy: gateway.docker.internal:3129
 Registry: https://index.docker.io/v1/
 Labels:
 Experimental: false
 Insecure Registries:
  127.0.0.0/8
 Live Restore Enabled: false
 Product License: Community Engine

```

## version

显示 Docker 版本信息

### 命令格式

docker version [OPTIONS]

### 常用参数

- **-f** 指定返回值的模板文件

### 使用实例


```shell
docker version
Client: Docker Engine - Community
 Cloud integration  0.1.18
 Version:           19.03.13
 API version:       1.40
 Go version:        go1.13.15
 Git commit:        4484c46d9d
 Built:             Wed Sep 16 16:58:31 2020
 OS/Arch:           darwin/amd64
 Experimental:      false

Server: Docker Engine - Community
 Engine:
  Version:          19.03.13
  API version:      1.40 (minimum version 1.12)
  Go version:       go1.13.15
  Git commit:       4484c46d9d
  Built:            Wed Sep 16 17:07:04 2020
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          v1.3.7
  GitCommit:        8fba4e9a7d01810a393d5d25a3621dc101981175
 runc:
  Version:          1.0.0-rc10
  GitCommit:        dc9208a3303feef5b3839f4323d9beb36df0a9dd
 docker-init:
  Version:          0.18.0
  GitCommit:        fec3683

```



# FAQ

:::danger Docker:Error response from daemon
Error response from daemon: Get https://registry-1.docker.io/v2/: read tcp 172.17.29.69:44568->52.55.168.20:443: read: connection reset by peer
:::

:::details Error response from daemon

- 通过dig @114.114.114.114 registry-1.docker.io找到可用IP
```shell
dig @114.114.114.114 registry-1.docker.io
; <<>> DiG 9.11.4-P2-RedHat-9.11.4-26.P2.el7_9.5 <<>> @114.114.114.114 registry-1.docker.io
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 47457
;; flags: qr rd ra; QUERY: 1, ANSWER: 8, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;registry-1.docker.io.          IN      A

;; ANSWER SECTION:
registry-1.docker.io.   33      IN      A       35.169.249.115
registry-1.docker.io.   33      IN      A       18.214.230.110
registry-1.docker.io.   33      IN      A       34.238.187.50
registry-1.docker.io.   33      IN      A       52.72.232.213
registry-1.docker.io.   33      IN      A       34.197.211.151
registry-1.docker.io.   33      IN      A       52.55.168.20
registry-1.docker.io.   33      IN      A       54.152.28.6
registry-1.docker.io.   33      IN      A       34.231.251.252

;; Query time: 10 msec
;; SERVER: 114.114.114.114#53(114.114.114.114)
;; WHEN: Wed Jul 21 11:44:46 CST 2021
;; MSG SIZE  rcvd: 177
```

- 修改/etc/hosts
```shell
echo "35.169.249.115 registry-1.docker.io" >> /etc/hosts
```

:::









