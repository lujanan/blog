## Docker CE安装

[TOC]

### 准备工作

​	Docker CE 支持 64 位版本 CentOS 7，并且要求内核版本不低于 3.10。 CentOS 7 满足最低内核的要求，但由于内核版本比较低，部分功能（如 `overlay2` 存储层驱动）无法使用，并且部分功能可能不太稳定。

#### 卸载旧版本

​	旧版本的 Docker 称为 `docker` 或者 `docker-engine`，使用以下命令卸载旧版本：

```shell
$ sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine
```



### Centos Docker CE在线安装

> 警告：切勿在没有配置 Docker YUM 源的情况下直接使用 yum 命令安装 Docker.

#### 使用 yum 安装

执行以下命令安装依赖包：

```shell
$ sudo yum install -y yum-utils \
           device-mapper-persistent-data \
           lvm2
```

鉴于国内网络问题，建议使用下面的阿里源。

执行下面的命令添加 `yum` 软件源：

```shell
# 阿里源
$ sudo yum-config-manager \ 
	--add-repo \ 
	http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo

# 中科大源
# $ sudo yum-config-manager \
#     --add-repo \
#     https://mirrors.ustc.edu.cn/docker-ce/linux/centos/docker-ce.repo
    
# 官方源
# $ sudo yum-config-manager \
#     --add-repo \
#     https://download.docker.com/linux/centos/docker-ce.repo
```

查看Docker版本:

```shell
$ sudo yum list docker-ce --showduplicates
```

#### 安装 Docker CE

```shell
# 更新本地yum包缓存
$ sudo yum makecache fast
# 安装最新版docker ce
$ sudo yum install docker-ce
# 安装指定版本docker ce，加上指定版本号
# $ sudo yum install docker-ce-18.03.0.ce
```



### Centos Docker CE rpm离线安装

#### 下载rpm包

​	docker-ce-18.06.1.ce-3.el7.x86_64.rpm [下载地址1](https://download.csdn.net/download/andlu6/10955075) [下载地址2](https://download.docker.com/linux/centos/7/x86_64/stable/Packages/docker-ce-18.06.1.ce-3.el7.x86_64.rpm)

#### 安装

​	下载完上面的rpm包后进行安装，会涉及到一些软件依赖的问题，可以分情况选择以下方式进行安装：

##### 1. yum安装

​	建议使用yum方式安装，yum安装过程中会下载相应的软件依赖，可以省去很多麻烦

```shell
# 使用yum命令安装
$ sudo yum -y install docker-ce-18.06.1.ce-3.el7.x86_64.rpm
```

##### 2. 手动下载依赖rpm包安装

​	如果网络问题无法使用yum方式安装，可以手动下载软件依赖rpm包进行安装

​	经过多次试验，所需包如下：

> 1. container-selinux-2.74-1.el7.noarch.rpm [下载地址](https://mirrors.aliyun.com/centos/7.6.1810/extras/x86_64/Packages/container-selinux-2.74-1.el7.noarch.rpm)
> 2. libselinux-2.5-14.1.el7.x86_64.rpm [下载地址](http://mirrors.163.com/centos/7/os/x86_64/Packages/libselinux-2.5-14.1.el7.x86_64.rpm)
> 3. libselinux-python-2.5-14.1.el7.x86_64.rpm [下载地址](http://mirrors.163.com/centos/7/os/x86_64/Packages/libselinux-python-2.5-14.1.el7.x86_64.rpm)
> 4. libselinux-utils-2.5-14.1.el7.x86_64.rpm [下载地址](http://mirrors.163.com/centos/7/os/x86_64/Packages/libselinux-utils-2.5-14.1.el7.x86_64.rpm)
> 5. libsemanage-2.5-14.el7.x86_64.rpm [下载地址](http://mirrors.163.com/centos/7/os/x86_64/Packages/libsemanage-2.5-14.el7.x86_64.rpm)
> 6. libsemanage-python-2.5-14.el7.x86_64.rpm [下载地址](http://mirrors.163.com/centos/7/os/x86_64/Packages/libsemanage-python-2.5-14.el7.x86_64.rpm)
> 7. libsepol-2.5-10.el7.x86_64.rpm [下载地址](http://mirrors.163.com/centos/7/os/x86_64/Packages/libsepol-2.5-10.el7.x86_64.rpm)
> 8. policycoreutils-2.5-29.el7.x86_64.rpm [下载地址](http://mirrors.163.com/centos/7/os/x86_64/Packages/policycoreutils-2.5-29.el7.x86_64.rpm)
> 9. policycoreutils-python-2.5-29.el7.x86_64.rpm [下载地址](http://mirrors.163.com/centos/7/os/x86_64/Packages/policycoreutils-python-2.5-29.el7.x86_64.rpm)
> 10. selinux-policy-3.13.1-229.el7.noarch.rpm [下载地址](http://mirrors.163.com/centos/7/os/x86_64/Packages/selinux-policy-3.13.1-229.el7.noarch.rpm)
> 11. selinux-policy-targeted-3.13.1-229.el7.noarch.rpm [下载地址](http://mirrors.163.com/centos/7/os/x86_64/Packages/selinux-policy-targeted-3.13.1-229.el7.noarch.rpm)
> 12. setools-libs-3.3.8-4.el7.x86_64.rpm [下载地址](http://mirrors.163.com/centos/7/os/x86_64/Packages/setools-libs-3.3.8-4.el7.x86_64.rpm)

​	如果上面的地址无法下载，我这里有一份打包好的资源 [docker-ce-18.06 rpm软件依赖包](https://download.csdn.net/download/andlu6/10955087)

​	下载上述依赖包和docker ce的rpm包，放在同一目录下，执行安装命令：

```shell
$ sudo rpm -ivh softPath/*.rpm --nodeps --force
```



### 安装成功后设置

#### 启动Docker CE

```shell
# 设置开机启动docker ce
$ sudo systemctl enable docker
# 启动docker ce
$ sudo systemctl start docker
```

#### 建立 docker 用户组

```shell
# 建立docker组
$ sudo groupadd docker
# 讲当前用户加入docker组
$ sudo usermod -aG docker $USER
```

退出当前终端并重新登录，进行如下测试。

#### 测试 Docker 是否安装正确

```shell
# 启动hello-world容器
$ docker run hello-world

Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
d1725b59e92d: Pull complete 
Digest: sha256:b3a26e22bf55e4a5232b391281fc1673f18462b75cdc76aa103e6d3a2bce5e77
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

若能正常输出以上信息，则说明安装成功。

#### 设置镜像加速器

> 国内网络访问docker官方镜像可能会比较慢
>
> https://registry.docker-cn.com 为Docker官方提供的国内加速器，应该算是体验最后之一的加速器了
>
> https://reg-mirror.qiniu.com 七牛云加速器

在 `/etc/docker/daemon.json` 中写入如下内容（如果文件不存在请新建该文件）

```json
{
    "registry-mirrors": [
        "https://registry.docker-cn.com"
    ]
}
```

> 注意，一定要保证该文件符合 json 规范，否则 Docker 将不能启动。

```shell
# 重启docker服务
$ sudo systemctl daemon-reload
$ sudo systemctl restart docker
```

#### 检查加速器是否生效

配置加速器之后，如果拉取镜像仍然十分缓慢，请手动检查加速器配置是否生效，在命令行执行 `docker info`，如果从结果中看到了如下内容，说明配置成功。

```
Registry Mirrors:
 https://registry.docker-cn.com/
```



### 参考

+ [Docker — 从入门到实践](https://yeasy.gitbooks.io/docker_practice/)

