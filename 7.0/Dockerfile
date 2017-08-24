FROM php:7.0-fpm

RUN apt-get update && apt-get install -y \
        git \
        libmemcached-dev \
        zlib1g-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        libmemcached-dev \
        memcached \
        libxml2-dev \
        php-soap \
    && git clone --branch php7 https://github.com/php-memcached-dev/php-memcached /usr/src/php/ext/memcached/ \
    && docker-php-ext-install memcached \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install mysqli pdo pdo_mysql \
    && docker-php-ext-install -j$(nproc) soap

COPY php.ini /usr/local/etc/php/conf.d/php.ini

VOLUME /usr/local/etc/php/conf.d
VOLUME /var/www/html
