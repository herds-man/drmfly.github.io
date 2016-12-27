---

layout: post

title: 在AWS上使用kubeadm部署Kubernetes集群

categories: [Kubernetes,Docker]

description: 在AWS上部署Kubernetes集群

keywords: kubernetes

---

> 在AWS上部署Kubernetes集群。

#### 背景
Kubeadm大大降低了kubernetes的安装难度，但仍然处于alpha 并未release，官方不推荐在正式环境使用。
kubernetes官网有基于kops安装集群的教程，但个人还是喜欢使用centos,然而AWS并未提供centos的官方镜像。
使用Redhat 7.2代替Centos7.

#### Redhat 7 使用Centos yum
- ##### 安装wget 
浏览器打开链接http://mirrors.aliyun.com/centos/7/os/x86_64/Packages/ 找到wget
下载wget-{version}.el7.x86_64.rpm 下载,scp 或者 通过 sftp上传到redhat主机.

```shell
# 注意替换{version}为实际对应版本号（版本升级，不固定，所以以变量代替）
wget http://mirrors.aliyun.com/centos/7/os/x86_64/Packages/wget-{version}.el7.x86_64.rpm
```
- ##### 下载yum依赖包

```shell
wget http://mirrors.aliyun.com/centos/7/os/x86_64/Packages/python-iniparse-{version}.el7.noarch.rpm
wget http://mirrors.aliyun.com/centos/7/os/x86_64/Packages/yum-{version}.el7.centos.noarch.rpm
wget http://mirrors.aliyun.com/centos/7/os/x86_64/Packages/yum-metadata-parser-{version}.el7.x86_64.rpm
wget http://mirrors.aliyun.com/centos/7/os/x86_64/Packages/yum-plugin-fastestmirror-{version}.el7.noarch.rpm

```
- ##### 安装依赖包
注意按顺序安装

```shell
rpm -ivh python-iniparse-{version}.el7.noarch.rpm
rpm -ivh yum-metadata-parser-{version}.el7.x86_64.rpm
rpm -ivh yum-{version}.el7.centos.noarch.rpm yum-plugin-fastestmirror-{version}.el7.noarch.rpm

```

如果在安装过程中提示包冲突，请先在http://mirrors.aliyun.com/centos/7/os/x86_64/Packages/ 下载对应依赖包 rpm -Uvh xxx.rpm 升级对应依赖包。

- ##### 更新repo
  - 删除/etc/yum.repo.d/ 下的文件，当然以防万一，先备份是个好习惯。
  - 使用阿里yum源
  
  ```
  wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
  ```
  
  修改CentOS-Base.repo，全量替换$releasever为7
  - 更新缓存
  
  ```
  yum clean all 
  yum makecache
  ```

#### 集群规划



参考：
http://wangn6806.blog.51cto.com/10410653/1711306
处于 设计阶段 持续更新.....

转载请注明出处，本文采用 [CC4.0](http://creativecommons.org/licenses/by-nc-nd/4.0/) 协议授权