---
layout:     post
title:	    docker-compose.yml文件	      
subtitle:   架设一个易用的私有云
date:       2020-03-01
author:     tyler
header-img: img/nextcloud.jpg
catalog:         true
tags:
    - vps
    - 私有云
---

```
nextcloud:

  image: wonderfall/nextcloud

  container_name: nextcloud_web

  links:

    - nextcloud-db:nextcloud-db

  environment:

    - UID=1000

    - GID=1000

    - UPLOAD_MAX_SIZE=5G

    - APC_SHM_SIZE=128M

    - OPCACHE_MEM_SIZE=128

    - CRON_PERIOD=15m

    - TZ=Aisa/Shanghai

    - ADMIN_USER=登录账号

    - ADMIN_PASSWORD=登录密码

    - DOMAIN=localhost

    - DB_TYPE=mysql

    - DB_NAME=nextcloud

    - DB_USER=nextcloud

    - DB_PASSWORD=数据库 nextcloud 账号密码

    - DB_HOST=nextcloud-db

  volumes:

    # 文件会放在宿主机的 `/docker/nextcloud` 目录，如果不存在会自动创建

    - /docker/nextcloud/data:/data

    - /docker/nextcloud/config:/config

    - /docker/nextcloud/apps:/apps2

    - /docker/nextcloud/themes:/nextcloud/themes

  expose:

    - 8888

  ports:

    # 宿主机端口:镜像端口

    - 8888:8888/tcp

  restart: always



nextcloud-db:

  image: mariadb:10

  container_name: nextcloud_db

  volumes:

    # 数据库文件会放在宿主机的 `/docker/nextcloud/db` 目录，如果不存在会自动创建

    - /docker/nextcloud/db:/var/lib/mysql

  environment:

    - MYSQL_ROOT_PASSWORD=数据库 root 密码

    - MYSQL_DATABASE=nextcloud

    - MYSQL_USER=nextcloud

    - MYSQL_PASSWORD=数据库 nextcloud 账号密码

  restart: always
```
