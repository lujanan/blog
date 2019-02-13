## Docker-Compose 安装

[TOC]

### Compose安装

#### 二进制包安装

从 [官方 GitHub Release](https://github.com/docker/compose/releases) 处直接下载编译好的二进制文件

```shell
$ sudo curl -L https://github.com/docker/compose/releases/download/1.23.2/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
```

#### bash 补全命令

```shell
$ curl -L https://raw.githubusercontent.com/docker/compose/1.23.2/contrib/completion/bash/docker-compose > /etc/bash_completion.d/docker-compose
```



### 参考

+ [Docker — 从入门到实践](https://yeasy.gitbooks.io/docker_practice/)
+ [Install Docker Compose](https://docs.docker.com/compose/install/#upgrading)