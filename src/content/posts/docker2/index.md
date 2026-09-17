---
title: Docker基本命令
published: 2026-09-17
image: ./1.avif
tags: [ docker, 教程 ]
category: 技术笔记
draft: false
---

## Docker基本命令

#### **启动docker**

```bash
systemctl start docker
```

#### **关闭docker**

```bash
systemctl stop docker
```

#### **docker容器随服务启动而自启动**

```bash
systemctl enable docker
```

#### **查看docker 运行状态**

```bash
systemctl status docker
```

>

#### **查看docker版本信息**

```bash
docker version
```

```bash
docker info
```

>

#### **获取命令带参(列如pull)**

```bash
docker pull --help
```

>

## docker镜像命令

#### **查看镜像列表**

```bash
docker images
```

>

#### **搜索镜像**

```bash
docker search 镜像名  
docker search --filter=STARS=9000 mysql  # 搜索 STARS >9000的 mysql 镜像
```

>

#### **拉取镜像**

- 不加tag(版本号) 即拉取docker仓库中 该镜像的最新版本latest 加:tag 则是拉取指定版本

```bash
docker pull 镜像名:tag
```

#### **启动一个redis 镜像**

> -v 为磁盘挂载；用于容器数据与本地同步
>
>
> -p 容器6379映射到本地6888端口 设置端口映射 --name 设置别名为aa;
>
>
>
> -d 后台运行
>
>
>
> redis为镜像名称或者镜像id

```bash
docker run -d -p 6888:6379 --name aaa -v /test:/data redis
docker exec -it aaa /bin/bash
```


#### **删除镜像-**-----当前镜像没有被任何容器使用才可以删除

```bash

#删除一个  
docker rmi -f 镜像名/镜像ID

#删除多个 其镜像ID或镜像用用空格隔开即可  
docker rmi -f 镜像名/镜像ID 镜像名/镜像ID 镜像名/镜像ID

#删除全部镜像 -a 意思为显示全部, -q 意思为只显示ID  
docker rmi -f $(docker images -aq)
```
#### 强制删除镜像

```bash
docker image rm 镜像名称/镜像ID
```


#### **保存镜像**

- 将我们的镜像 保存为tar 压缩文件 这样方便镜像转移和保存 ,然后可以在任何一台安装了docker的服务器上 加载这个镜像
  
```bash
docker save 镜像名/镜像ID -o 镜像保存在哪个位置与名字
docker save tomcat -o /myimg.tar
```

#### **7.加载镜像**

- 任何装 docker 的地方加载镜像保存文件,使其恢复为一个镜像

```bash
docker load -i 镜像保存文件位置
```

#### **镜像标签**
```bash
 docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]

 docker tag 源镜像名:TAG 想要生成新的镜像名:新的TAG

 # 如果省略TAG 则会为镜像默认打上latest TAG  
 docker tag aaa bbb

  #  上方操作等于 
 docker tag aaa:latest bbb:test

  #  我们根据镜像 quay.io/minio/minio 添加一个新的镜像 名为 aaa 标签Tag设置为1.2.3  
 docker tag quay.io/minio/minio:1.2.3 aaa:1.2.3

  # 我们根据镜像 app-user:1.0.0 添加一个新的镜像 名为 app-user 标签Tag设置为alpha-1.0.0  
 docker tag app-user:1.0.0 app-user:alpha-1.0.0

```


## docker容器命令

#### **查看正在运行容器列表**
```bash
 docker ps

```
#### **查看所有容器** -----包含正在运行 和已停止的

```bash
docker ps -a
```
#### **运行一个容器**

- -it 表示 与容器进行交互式启动 -d 表示可后台运行容器 （守护式运行） --name 给要运行的容器 起的名字 /bin/bash 交互路径  
```bash
docker run -it -d --name 要取的别名 镜像名:Tag /bin/bash
```



#### **删除容器**
```bash
 #删除一个容器  
 docker rm -f 容器名/容器ID  
 #删除多个容器 空格隔开要删除的容器名或容器ID  
 docker rm -f 容器名/容器ID 容器名/容器ID 容器名/容器ID  
 #删除全部容器  
 docker rm -f $(docker ps -aq)
```



#### **容器端口与服务器端口映射**
```bash
# -p 宿主机端口:容器端口

docker run --name redis002 -p 8888:6379 redis

docker run --name redis -d -p 6399:6379 -v D:\software\Docker\dockerTest\redis:/data --network my-net redis


```

#### **进入容器方式一**
```bash
docker exec -it 容器名/容器ID /bin/bash

#进入 前面的 redis002容器  
docker exec -it redis002 /bin/bash
```


#### **进入容器方式二**  —推荐使用 exec 方式
```bash
docker attach 容器名/容器ID
```


#### **退出容器**
```bash
#-----直接退出 启动时未添加 -d(持久化运行容器) 时 执行此参数 容器会被关闭  
exit

# 优雅提出 --- 无论是否添加-d 参数 执行此命令容器都不会被关闭  
Ctrl + p + q
```


#### **停止容器**
```bash
 docker stop 容器ID/容器名
```

### **重启容器**
```bash
docker restart 容器ID/容器名
```

#### **启动容器**
```bash
docker start 容器ID/容器名(docker run每次会新创建一个容器，start用来启动已经创建的容器)
```


#### **kill 容器**
```bash
docker kill 容器ID/容器名
```


#### **容器文件拷贝** —无论容器是否开启 都可以进行拷贝
```bash
#docker cp 容器ID/名称:文件路径 要拷贝到外部的路径 | 要拷贝到外部的路径 容器ID/名称:文件路径  
#从容器内 拷出  
docker cp 容器ID/名称: 容器内路径 容器外路径  
#从外部 拷贝文件到容器内  
docker cp 容器外路径 容器ID/名称: 容器内路径
```



#### **查看容器日志**
```bash
docker logs -f --tail=要查看末尾多少行 默认all 容器ID

```


#### **容器随docker服务启动而自启动**
```bash
docker run -itd --name redis001 -p 8888:6379 --restart=always redis:5.0.5 /bin/bash

```


#### **不想删容器，又想让这个容器设置开机自启动，那么我们修改其启动配置即可！**
```bash
docker update --restart=always 容器Id 或者 容器名
或
docker container update --restart=always 容器Id 或者 容器名
```



#### **更换容器名**
```bash
docker rename 容器ID/容器名 新容器名
```


#### **mysql容器启动命令**
```bash
 docker run 
 --name mysql8 
 -d 
 -p 3309:3306 
 -v D:\software\Docker\dockerTest\mysql\conf:/etc/mysql/conf.d 
 -v D:\software\Docker\dockerTest\mysql\data:/var/lib/mysql 
 -e MYSQL_ROOT_PASSWORD=123456 镜像id/镜像名称
```
- *这条命令解释：启动mysql8.0.17的镜像容器*
- *并命名容器为mysql8 并后台启动*
- *并磁盘挂载同步容器中的/etc/mysql/conf.d配置文件和数据库存储文件var/lib/mysql*
- *并指定mysql密码 ，并启动对应的镜像id或者镜像名称：tag（声明版本，不然会下载最新版本）*
- *这样保证了，即使容器被删除，本地还是能保存数据库文件夹，还能再次被挂载使用*
- *容器内新建删除修改文件：宿主机外部挂载的目录 同步！！！！要是真有人搞事删除了容器内部中挂载目录下的数据那真的是要删库跑路了*
- *容器整个删除:宿主机外部挂载的目录不会同步！！！！*


## 自己提交镜像

- 我们运行的容器可能在镜像的基础上做了一些修改，有时候我们希望保存起来，封装成一个更新的镜像，这时候我们就需要使用 commit
  命令来构建一个新的镜像
```bash
docker commit -m="提交信息" -a="作者信息" 容器名/容器ID 提交后的镜像名:Tag
```

#### **nginx配置命令：**

- 先启动一个默认nginx容器，然后把对应目录拷到本地，然后删掉这个容器，重新启动一个新的
```bash
 docker cp nginx:/etc/nginx/nginx.conf D:\software\Docker\dockerTest\nginx # 配置文件(可以修改优先级使用)
 docker cp nginx:/etc/nginx/conf.d D:\software\Docker\dockerTest\nginx\conf #默认配置文件
 docker cp nginx:/usr/share/nginx/html D:\software\Docker\dockerTest\nginx\www #静态文件目录
 nginx:/var/log/nginx D:\software\Docker\dockerTest\nginx\logs #静态文件目录
 
#启动命令并挂载对应目录(一定要文件相对应，nginx.conf对应本地的nginx.conf)
docker run --name nginx 
-p 90:80 
-v D:\software\Docker\dockerTest\nginx\nginx.conf:/etc/nginx/nginx.conf 
-v D:\software\Docker\dockerTest\nginx\conf\conf.d:/etc/nginx/conf.d 
-v D:\software\Docker\dockerTest\nginx\www:/usr/share/nginx 
-v D:\software\Docker\dockerTest\nginx\logs:/var/log 
-d nginx:1.20.1
```


#### **容器内下载ping工具**
```bash
apt-get update && apt-get install iputils-ping
```

#### **容器之间互相通信**

##### **1.创建一个自定义网络**
```bash
#bridge网络，网络名字:hsjnet，B类网络192.168.0.0/16
docker network create --driver bridge --subnet 192.168.0.0/16 --gateway 192.168.0.1 hsjnet
```

##### **2.启动两个容器时添加--network hsjnet**

```bash
docker run -d -P --name tomcat-hsjnet-001 --network hsjnet tomcat
```

##### **3.查看使用hsjnet网络的容器IP**

```bash
docker network inspect hsjnet
```

#### **其他：**

- 安装docker时需要安装wsl2：[https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

