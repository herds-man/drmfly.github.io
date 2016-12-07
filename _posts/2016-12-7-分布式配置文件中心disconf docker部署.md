---

layout: post

title: 基于Dokcer容器部署分布式配置文件中心disconf

categories: [Config,Docker]

description: 基于Dokcer容器部署分布式配置文件中心

keywords: disconf,docker

---

> Docker容器部署disconf

### 一、背景

随着容器技术、微服务架构的流行，互联网以及互联网转型ing企业已经逐步开始从单体架构解耦为微服务架构的同时，将传统应用/程序容器化部署。

容器化过程中，我们期望一个镜像可以运行在不同的环境（local,qa,rd..)。这意味着可配置信息要么通过系统变量供容器读取，这是最鼓励大家使用的方式，但是Java web开发历来都有繁琐的xml配置 比如spring XML config、 log4j/logback等等。通过变量传入意味着使用大量的环境变量。所以使用集中配置文件中心是解决java程序配置文件瓶颈的主要途径。

公司选择国内流行的百度disconf作为配置文件中心，本文主要讨论基于容器部署disconf。

### 二、编译disconf-web

### 三、镜像制作

### 四、Compose部署

待补充....

转载请注明出处，本文采用 [CC4.0](http://creativecommons.org/licenses/by-nc-nd/4.0/) 协议授权