---
title: Mongodb 集群部署
published: 2022-05-17 15:29:35
image: ./77.avif
tags: [MongoDB, 集群部署, 踩坑]
category: 技术笔记
draft: false
---

# Mongodb 集群部署

**Mongodb 版本>=4.2windows不以服务式安装**

#### 一、安装完成后设置目录下data里面间分区

1.建立mongodb1文件夹

2.在mongodb1下建立 conf与log文件夹

3.在conf文件夹下建立 mongodb.conf

内容为：

```xml
dbpath=D:\BtSoft\mongodb\data\mongodb1 #修改路径
logpath=D:\BtSoft\mongodb\data\mongodb1\log\mongodb.log #修改路径
logappend=true
bind_ip=0.0.0.0
port=27011 #修改端口
shardsvr=true
journal=true
replSet=skeqi
```

3.复制mongodb1为 mongodb2 mongodb3 并分别修改 mongodb.conf 里的路径与端口（同样操作）

#### 二、准备启动

电脑搜索PowerShell，进入到mongod\bin，输入下面（路径按自己实际位置来）

```
mongod --config D:\BtSoft\mongodb\data\mongodb1\conf\mongodb.conf --install --serviceName "MongoDB1"
mongod --config D:\BtSoft\mongodb\data\mongodb2\conf\mongodb.conf --install --serviceName "MongoDB2"
mongod --config D:\BtSoft\mongodb\data\mongodb3\conf\mongodb.conf --install --serviceName "MongoDB3"
```

然后电脑搜索服务，打开找到对应的3个MongoDB服务，启动并设置自动

然后重新打开一个cmd（mongod\bin目录下）输入 mongo –port 27011，然后再输入：

```xml
use admin;
cfg = {_id: "skeqi",members:[{_id: 0,host: '127.0.0.1:27011',priority: 2},{_id: 1,host: '127.0.0.1:27012',priority: 1},{_id: 3,host: '127.0.0.1:27013',arbiterOnly: true}]};
rs.initiate(cfg)
rs.status()
```

中间无任何报错即成功了。