# docker-typecho
项目包含php、nginx，未包含redis和mysql，因为笔者本地有这俩服务

如果本地这俩服务没有，参考最后的文档来修改docker-compose.yml文件

使用方法：

1. 安装docker，拉取本项目

   ```git
   git clone https://github.com/Anantree/docker-typecho.git
   ```

2. 按照自己的需求修改docker-compose.yml文件

3. 拉取最新的typecho代码

   ```git
   cd docker-typecho
   git clone https://github.com/typecho/typecho web
   ```

   - 这一步可省略，web中有typecho的1.2.2版本。如需最新版本将web文件夹全部删除，执行上面的语句

4. 启动服务

   ```git
   docker-compose up -d
   ```

5. 启动好后，会发现选择数据库的下拉框没有mysql的选项。这是因为typecho需要mysql pdo，需要安装php扩展

   - 进入php-fpm的容器，执行下面的语句

   - ```shell
     docker-php-ext-install pdo_mysql
     ```

   - 安装完后重启服务即可





## 附：完整docker-compose.yaml文件

```yaml
services:
 mysql:
   image: mysql:5.7
   privileged: false
   restart: always
   volumes:
   - ./mysql:/var/lib/mysql
   environment:
     - MYSQL_ROOT_PASSWORD=root
     - MYSQL_DATABASE=typecho
     - MYSQL_USER=typecho
     - MYSQL_PASSWORD=123456
 redis:
   image: redis
   privileged: false
   restart: always
   environment:
   - REDIS_PASS=**None**
 php:
   image: php:7.2-fpm
   volumes:
     - ./web:/www
     #- ./php.ini:/usr/local/etc/php/php.ini
   links:
     - mysql
     - redis
 nginx:
   image: nginx:1.20.1
   volumes:
     - ./nginx/default.conf:/etc/nginx/conf.d/default.conf
     - ./nginx/fastcgi_params:/etc/nginx/fastcgi_params.modified
     - ./nginx/ssl:/etc/nginx/ssl
   volumes_from:
     - php
   ports:
     - 80:80
     #- 443:443
   links:
     - php

```











