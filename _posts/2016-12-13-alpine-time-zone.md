---

layout: post

title: alpine 修改时区

categories: [automation,test,titer]

description: 构建docker镜像时依赖的官方镜像大多时区不是国内东八区,需要在build镜像时重新设置时区

keywords: titer,automation,test,API

---

> 构建docker镜像时依赖的官方镜像大多时区不是国内东八区,需要在build镜像时重新设置时区。

#### 修改镜像源为阿里
```
echo -e  "http://mirrors.aliyun.com/alpine/v3.4/main\nhttp://mirrors.aliyun.com/alpine/v3.4/community" \
 >  /etc/apk/repositories && apk update
```

#### 安装tzdata

```
apk add tzdata
```
#### 拷贝对应时区止localtime
```
cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```
#### 指定时区
```
echo "Shanghai/Asia" > /etc/timezone
```
#### Dockerfile 写法
```
FROM tomcat:alpine
RUN echo -e  "http://mirrors.aliyun.com/alpine/v3.4/main\nhttp://mirrors.aliyun.com/alpine/v3.4/community" >  /etc/apk/repositories \
&& apk update && apk add tzdata \
&& cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
&& echo "Shanghai/Asia" > /etc/timezone
```


转载请注明出处，本文采用 [CC4.0](http://creativecommons.org/licenses/by-nc-nd/4.0/) 协议授权










