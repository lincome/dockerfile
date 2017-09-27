# env
php:7.1.9-apache

### One

```
FROM php:7.1.9-apache
ENV APACHE_DOCUMENT_ROOT /var/www/html/public
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf
COPY docker/apache2.conf /etc/
RUN docker-php-ext-install pdo_mysql
```

### Two
通过dockerfile重建你需要的环境镜像
```
docker build -t php_apache:laravel .
```

### Three
创建容器
```
docker run -itv /blog1:/usr/share/nginx/html --add-host sfc5.com:192.168.99.100 -P --privileged --name php_nginx_5 [镜像id]
```

进入容器
```
docker exec -it [容器id] bash
```
