FROM php:7.3-apache-stretch

RUN a2enmod rewrite && service apache2 restart

RUN apt-get update \
    && apt-get install -y \
        libwebp-dev \
        libxpm-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libzip-dev \
        libxml2-dev \
    && docker-php-ext-install -j$(nproc) iconv mysqli session zip xml pdo pdo_mysql \
    && docker-php-ext-configure gd --with-gd --with-webp-dir --with-jpeg-dir \
        --with-png-dir --with-zlib-dir --with-xpm-dir --with-freetype-dir \
        --enable-gd-native-ttf \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-configure opcache --enable-opcache \
    && docker-php-ext-install opcache

RUN pecl install xdebug-2.7.2 \
    && docker-php-ext-enable xdebug

# add configs
ADD ./xdebug.ini /usr/local/etc/php/conf.d/201-xdebug.ini
ADD ./php.ini /usr/local/etc/php/conf.d/php.ini
