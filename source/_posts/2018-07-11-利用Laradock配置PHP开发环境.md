---
title: 利用Laradock配置PHP开发环境
tags:
  - PHP
  - docker
  - laradock
categories:
  - 工具库
  - 开发环境
abbrlink: e047a409
date: 2018-07-11 17:05:42
keywords: php laradock PHPstorm
description:
---


## 需要一个简易的开发环境

传统的开发环境, 需要自己下 PHP, Nginx, MySQL... 等一大堆东西, 但是 docker 给我们带来了便利, 从此就告别了, 本地环境跑的好好的东西,
为啥服务器就是不给力, 各种未知的bug. 

## 准备工作
-------------------

### docker 环境

<!--more-->

不管你是 Mac, windows 或者 linux 等, 先去官网搞定这个基础环境. [传送门](https://docs.docker.com/install/)

### Git

你需要 clone 源码.

## 开始你的表演
---------------------

### 拉取源码

进入你的开发代码目录

`git clone https://github.com/laradock/laradock.git`

### 修改配置

```bash
cp env-example .env
```

接下就可以修改 `.env` 里面的配置了.

```bash
# 修改composer 为中国镜像 提速
WORKSPACE_COMPOSER_REPO_PACKAGIST=https://packagist.phpcomposer.com

```


```bash
# 接下来运行 Nginx 以及 mysql redis...
docker-compose up -d nginx mysql

# 因为是首次拉取, 所以会比较慢
```

> 当然你可以使用加速器来加速docker
> 
> 需要注册登录, 并且是免费的
> 
> https://www.daocloud.io/mirror#accelerator-doc

```bash
# 这样你就可以进入工作台了
docker-compose exec --user=laradock workspace bash
```

### phpstorm xdebug

在这儿用 Windows 做例子, 毕竟用 Windows 开发是坑最多了.

#### 开启 xdebug

```bash
#  laradock/.env 文件
# 修改

### WORKSPACE #############################################
WORKSPACE_INSTALL_XDEBUG=true
WORKSPACE_INSTALL_WORKSPACE_SSH=true

### PHP_FPM ###############################################
PHP_FPM_INSTALL_XDEBUG=true
```

#### 修改 .ini 配置

```ini
; laradock/workspace/xdebug.ini
; laradock/php-fpm/xdebug.ini

; 修改两个文件

; remote_host 的 "dockerhost" 是 laradock/.env 文件下的 DOCKER_HOST_IP 的值, 需要在 系统的 hosts 文件添加这么一条记录  10.0.75.1  dockerhost
xdebug.remote_host=dockerhost 
xdebug.remote_connect_back=0
xdebug.remote_port=9000
xdebug.idekey=PHPSTORM

xdebug.remote_autostart=1
xdebug.remote_enable=1
xdebug.cli_color=1
```

#### 修改 hosts 文件

此处需要 管理员权限


#### 配置 phpstorm

- 配置 deployment 
- 配置 server
  - PHP_IDE_CONFIG=serverName=laradock 
- 配置 debug (非必填)
- 配置 test Framework
- Edit Run/Debug configuration



