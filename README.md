# env
php:5.6.31-apache

### One

```
FROM php:5.6.31-apache
COPY docker/php.ini /usr/local/etc/php/
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd
RUN pecl install redis-3.1.0 \
    && pecl install xdebug-2.5.0 \
    && docker-php-ext-enable redis xdebug
RUN docker-php-ext-install mysql
```

### Two
通过dockerfile重建你需要的环境镜像
```
docker build -t php_apache:v1 .
```

### Three
创建容器
```
docker run -itv /blog1:/usr/share/nginx/html --add-host sfc5.com:192.168.99.100 -p 9999:80 -p 3306:3306 --privileged --name php_nginx_5 [镜像id]
```

进入容器
```
docker exec -it [容器id] bash
```
