FROM php:5.6-fpm

RUN apt-get update && apt-get install -y \
        git \
        libmemcached-dev \
        libmemcached11 \
        zlib1g-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        libmemcached-dev \
        php5-memcached \
        memcached \
        libxml2-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt bcmath \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install mysql mysqli pdo pdo_mysql \
    && docker-php-ext-install soap \
    && yes '' | pecl install memcached-2.2.0 \
    && docker-php-ext-enable memcached \
    && yes '' | pecl install memcache \
    && docker-php-ext-enable memcache

RUN apt-get update && apt-get install -y libssl-dev && rm -rf /var/lib/apt/lists/*

RUN pecl install mongo-1.6.14 \
    && docker-php-ext-enable mongo

COPY php.ini /usr/local/etc/php/conf.d/php.ini

VOLUME /usr/local/etc/php/conf.d
VOLUME /var/www/html
