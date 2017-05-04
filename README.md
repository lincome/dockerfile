# dockerfile_php_nginx_mysql
docker环境php7、nginx1、mysql5.5

### 第一步
从阿里云拉取镜像
```
docker pull registry.cn-hangzhou.aliyuncs.com/linqr/php_nginx_mysql:v5
```

### 第二步
通过dockerfile重建你需要的环境镜像
```
docker build -t nginx_php_mysql:v3 .
```

### 第三步
创建容器
```
docker run -itv /blog1:/usr/share/nginx/html --add-host sfc5.com:192.168.99.100 -p 9999:80 -p 3306:3306 --privileged --name php_nginx_5 [镜像id]
```
系统自动用supervisor进程管理，启动nginx、php-fpm、mysql

进入容器
```
docker exec -it [容器id] bash
```
mysql默认账号root、密码root

### 第四步
访问站点
sfc5.com/192.168.99.100:9999
