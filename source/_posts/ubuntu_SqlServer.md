---
title: Ubuntu（22.04）下安装SQL Server
date: 2024-05-07
description: Ubuntu下安装SQL Server
keywords: Ubuntu下安装SQL Server
tags:
  - SQl Server
categories:
  - SQl Server
top_img: false
cover: false
---

在Ubuntu下安装SQL Server[^参考]



## 安装 SQL Server

### 导入公共存储库 GPG 密钥

```sh
sudo apt-get install curl
curl -fsSL https://packages.microsoft.com/keys/microsoft.asc | sudo gpg --dearmor -o /usr/share/keyrings/microsoft-prod.gpg
sudo cp /usr/share/keyrings/microsoft-prod.gpg /etc/apt/trusted.gpg.d/
```

 ### 注册 SQL Server Ubuntu 存储库

```sh
curl -fsSL https://packages.microsoft.com/config/ubuntu/22.04/mssql-server-2022.list | sudo tee /etc/apt/sources.list.d/mssql-server-2022.list
```

 ### 运行以下命令以安装 SQL Server

```sh
sudo apt-get update
sudo apt-get install -y mssql-server
```

 

### 设置 SA 密码

```sh
sudo ACCEPT_EULA='Y' MSSQL_PID='Developer' MSSQL_SA_PASSWORD='1q2w3e4rQWE!' MSSQL_TCP_PORT=1433 /opt/mssql/bin/mssql-conf setup
```

 

 ### 完成配置后，验证服务是否正在运行

```sh
systemctl status mssql-server --no-pager
```



## 安装 SQL Server 命令行工具

### 注册 Microsoft Ubuntu 存储库

```sh
curl https://packages.microsoft.com/config/ubuntu/22.04/prod.list | sudo tee /etc/apt/sources.list.d/ms-prod.list
```

 

 ### 更新源列表，并使用 unixODBC 开发人员包运行安装命令

```sh
sudo apt-get update
sudo apt-get install -y mssql-tools18 unixodbc-dev
```

## 启动服务

```sh
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
sudo systemctl restart mssql-server
```

[^参考]: https://learn.microsoft.com/zh-cn/sql/linux/quickstart-install-connect-ubuntu?view=sql-server-ver16&tabs=ubuntu2004