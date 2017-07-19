---

layout: post

title: 基于docker 部署zookeeper集群

categories: [技术文档]

description: 基于docker host网络模式部署zookeeper集群

keywords: zookeeper,docker

---


> 部署zookeeper集群

## 集群规划

10.129.11.12   zk1
10.129.11.13   zk2
10.129.11.14   zk3

## 镜像

```bash
$ docker pull mesoscloud/zookeeper
```
## 启动容器
### zk1上启动节点1
```bash
$ docker run -d \
-v /data/svc/zookeeper/data:/data \
-v /data/svc/zookeeper/log:/datalog \
-e ZOO_MY_ID=1 \
-e "ZOO_SERVERS=server.1=10.129.11.12:2888:3888 server.2=10.129.11.13:2888:3888 server.3=10.129.11.14:2888:3888" \
--name=zookeeper --net=host --restart=always zookeeper:3.4.10
```
### zk2上启动节点2
```bash
$ docker run -d \
-v /data/svc/zookeeper/data:/data \
-v /data/svc/zookeeper/log:/datalog \
-e ZOO_MY_ID=2 \
-e "ZOO_SERVERS=server.1=10.129.11.12:2888:3888 server.2=10.129.11.13:2888:3888 server.3=10.129.11.14:2888:3888" \
--name=zookeeper --net=host --restart=always zookeeper:3.4.10
```
### zk3 上启动节点3
```bash
$ docker run -d \
-v /data/svc/zookeeper/data:/data \
-v /data/svc/zookeeper/log:/datalog \
-e ZOO_MY_ID=3 \
-e "ZOO_SERVERS=server.1=10.129.11.12:2888:3888 server.2=10.129.11.13:2888:3888 server.3=10.129.11.14:2888:3888" \
--name=zookeeper --net=host --restart=always zookeeper:3.4.10
```
