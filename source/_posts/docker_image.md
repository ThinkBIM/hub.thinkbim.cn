---
title: Docker镜像常用命令-image
date: 2021-06-21
description: Docker常用命令
keywords: Docker|命令|image|镜像
tags:
  - command 
categories:
  - Docker
---


## search
查找镜像

### 命令格式
```shell
docker search [OPTIONS] TERM
```

### 使用示例

```shell
docker search nginx
NAME                               DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
nginx                              Official build of Nginx.                        13865               [OK]                
jwilder/nginx-proxy                Automated Nginx reverse proxy for docker con…   1896                                    [OK]
richarvey/nginx-php-fpm            Container running Nginx + PHP-FPM capable of…   791                                     [OK]

#查看stars>=100 nginx镜像
search -f stars=100 nginx
NAME                      DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
nginx                     Official build of Nginx.                        13865               [OK]                
jwilder/nginx-proxy       Automated Nginx reverse proxy for docker con…   1896                                    [OK]
richarvey/nginx-php-fpm   Container running Nginx + PHP-FPM capable of…   791                                     [OK]
linuxserver/nginx         An Nginx container, brought to you by LinuxS…   127
```

### 参数说明

- NAME  镜像仓库源的名称

- DESCRIPTION 镜像的描述

- OFFICIAL  是否 docker 官方发布

- STARS 类似 Github 里面的 star，表示点赞、喜欢的意思

- AUTOMATED 自动构建


```shell
docker search nginx
NAME                               DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
nginx                              Official build of Nginx.                        13865               [OK]                
jwilder/nginx-proxy                Automated Nginx reverse proxy for docker con…   1896                                    [OK]
richarvey/nginx-php-fpm            Container running Nginx + PHP-FPM capable of…   791                                     [OK]

#查看stars>=100 nginx镜像
search -f stars=100 nginx
NAME                      DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
nginx                     Official build of Nginx.                        13865               [OK]                
jwilder/nginx-proxy       Automated Nginx reverse proxy for docker con…   1896                                    [OK]
richarvey/nginx-php-fpm   Container running Nginx + PHP-FPM capable of…   791                                     [OK]
linuxserver/nginx         An Nginx container, brought to you by LinuxS…   127
```

## pull
从镜像仓库中拉取或者更新指定镜像


### 命令格式
```shell
docker pull [OPTIONS] NAME[:TAG|@DIGEST]
```

### 使用示例

```shell
docker pull hello-world
Using default tag: latest
latest: Pulling from library/hello-world
0e03bdcc26d7: Pull complete 
Digest: sha256:8c5aeeb6a5f3ba4883347d3747a7249f491766ca1caa47e5da5dfcf6b9b717c0
Status: Downloaded newer image for hello-world:latest
docker.io/library/hello-world:latest

# 下载账号仓库的镜像
docker pull hateghost/docker:latest
```

## push
将本地的镜像上传到镜像仓库,要先登陆到镜像仓库



### 使用示例

```shell
#上传本地镜像hateghost/docker:latest到镜像仓库中。
docker push hateghost/docker:latest
The push refers to repository [docker.io/hateghost/docker]
9c27e219663c: Mounted from library/hello-world 
latest: digest: sha256:90659bf80b44ce6be8234e6ff90a1ac34acbeb826903b02cfa0da11c82cbc042 size: 525
```



## images

列出本地镜像

### 命令格式

```shell
docker images [OPTIONS] [REPOSITORY[:TAG]]
```


### 使用示例

```shell
docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
webserver           v2                  8c1b66feb178        3 hours ago         131MB
```



## rmi
删除本地一个或多少镜像

### 命令格式

```shell
docker rmi [OPTIONS] IMAGE [IMAGE...]
```

### 常用参数

- **-f :**强制删除；

- **--no-prune :**不移除该镜像的过程镜像，默认移除；

### 使用示例

```shell
docker rmi hateghost/docker:latest
```



## save

将指定镜像保存成 tar 归档文件


### 常用参数

**-o :**输出到的文件

### 使用示例

```shell
docker save -o webserver-v2.tar webserver:v2
ls
Dockerfile       webserver-v2.tar webserver.tar
docker rmi webserver:v2
Untagged: webserver:v2
Deleted: sha256:8c1b66feb1786e67dc240cb83b8ec3adabd88c935187f2d95dd6d298303965e3
 Docker docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
webserver           v1                  a3038edc18d1        3 hours ago         133MB

```



## build

使用 Dockerfile 创建镜像

### 常用参数

- **--build-arg=[] :** 设置镜像创建时的变量；

- **--cpu-shares :** 设置 cpu 使用权重；

- **--cpu-period :** 限制 CPU CFS周期；

- **--cpu-quota :** 限制 CPU CFS配额；

- **--cpuset-cpus :** 指定使用的CPU id；

- **--cpuset-mems :** 指定使用的内存 id；

- **--disable-content-trust :** 忽略校验，默认开启；

- **-f :** 指定要使用的Dockerfile路径；

- **--force-rm :** 设置镜像过程中删除中间容器；

- **--isolation :** 使用容器隔离技术；

- **--label=[] :** 设置镜像使用的元数据；

- **-m :** 设置内存最大值；

- **--memory-swap :** 设置Swap的最大值为内存+swap，"-1"表示不限swap；

- **--no-cache :** 创建镜像的过程不使用缓存；

- **--pull :** 尝试去更新镜像的新版本；

- **--quiet, -q :** 安静模式，成功后只输出镜像 ID；

- **--rm :** 设置镜像成功后删除中间容器；

- **--shm-size :** 设置/dev/shm的大小，默认值是64M；

- **--ulimit :** Ulimit配置。

- **--tag, -t:** 镜像的名字及标签，通常 name:tag 或者 name 格式；可以在一次构建中为一个镜像设置多个标签。

- **--network:** 默认 default。在构建期间设置RUN指令的网络模式

### 使用示例

```bash
#创建Dockerfile文件

vi Dockerfile

FROM webserver:v1


docker build .
Sending build context to Docker daemon  2.048kB
Step 1/1 : FROM webserver:v1
 ---> a3038edc18d1
Successfully built a3038edc18d1

#指定Dockerfile文件
docker build -f /etc/Dockerfile .
#指定名称
docker build -t webserver:v2 .

##创建镜像的过程不使用缓存
docker build -t webserver:v2 --no-cache .

```



## tag

标记本地镜像，将其归入某一仓库，重命名

### 使用示例

```shell
docker tag hello-world:latest hateghost/docker:latest
docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hateghost/docker    latest              bf756fb1ae65        9 months ago        13.3kB
hello-world         latest              bf756fb1ae65        9 months ago        13.3kB
```



## history

导入使用 [docker save](https://www.runoob.com/docker/docker-save-command.html) 命令导出的镜像

### 常用参数

- **-H :** 以可读的格式打印镜像大小和日期，默认为true；

- **--no-trunc :** 显示完整的提交记录；

- **-q :** 仅列出提交记录ID

### 使用示例

```shell
docker history runoob/ubuntu:v3
IMAGE             CREATED           CREATED BY                                      SIZE      COMMENT
4e3b13c8a266      3 months ago      /bin/sh -c #(nop) CMD ["/bin/bash"]             0 B                 
<missing>         3 months ago      /bin/sh -c sed -i 's/^#\s*\(deb.*universe\)$/   1.863 kB            
<missing>         3 months ago      /bin/sh -c set -xe   && echo '#!/bin/sh' > /u   701 B               
<missing>         3 months ago      /bin/sh -c #(nop) ADD file:43cb048516c6b80f22   136.3 MB
```

## import

从归档文件中创建镜像

### 常用参数

- **-c :** 应用docker 指令创建镜像；

- **-m :** 提交时的说明文字；

### 使用示例

```shell
docker import ./webserver.tar webserver:v2
sha256:8c1b66feb1786e67dc240cb83b8ec3adabd88c935187f2d95dd6d298303965e3
docker history webserver:v2
IMAGE               CREATED             CREATED BY          SIZE                COMMENT
8c1b66feb178        15 seconds ago                          131MB               Imported from -
```





## load

导入使用 [docker save](https://www.runoob.com/docker/docker-save-command.html) 命令导出的镜像

### 使用示例

```bash
docker load -i webserver-v2.tar 
Loaded image: webserver:v2
docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
webserver           v2                  8c1b66feb178        3 hours ago         131MB
webserver           v1                  a3038edc18d1        3 hours ago         133MB
```

## create

创建一个新的容器但不启动它

### 使用示例

```bash
docker create --name webnewserver nginx
9e14a8a86838aae088775dec302f5764513b510db681e8540dfca4fe2b94624c
docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                   PORTS                  NAMES
9e14a8a86838        nginx               "/docker-entrypoint.…"   30 seconds ago      Created                                         webnewserver
531d1da7106a        nginx               "/docker-entrypoint.…"   13 hours ago        Up 3 hours               0.0.0.0:8000->80/tcp   webserver
d71dcdf7c42b        docker101tutorial   "/docker-entrypoint.…"   2 months ago        Exited (0) 6 weeks ago                          docker-tutorial

```



## update

```shell
docker update --cpus 2 webaserver
```

## login/logout

登录/退出

### 命令格式

```shell
docker login [OPTIONS] [SERVER]
docker logout [OPTIONS] [SERVER]
```


### 使用示例

```shell
#登录
docker login
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: hateghost
Password:

docker login -u 用户名 -p 密码

#登出
Docker docker logout
Removing login credentials for https://index.docker.io/v1/
```










