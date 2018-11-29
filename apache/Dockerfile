FROM php:7.1-apache

#ADD nginx.conf /etc/nginx/
#ADD local.conf /etc/nginx/conf.d/local.conf

RUN apt-get update \
    && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    && docker-php-ext-install -j$(nproc) iconv mysqli session gd \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

RUN pecl install xdebug-2.6.0 \
    && docker-php-ext-enable xdebug

# add configs
ADD ./xdebug.ini /usr/local/etc/php/conf.d/201-xdebug.ini
ADD ./php.ini /usr/local/etc/php/conf.d/php.ini