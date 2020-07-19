FROM php:7.4-apache

RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    iproute2 \
    && docker-php-ext-configure gd \
    && docker-php-ext-install -j$(nproc) mysqli \
    && docker-php-ext-install -j$(nproc) gd

RUN pecl channel-update pecl.php.net && pecl -q install xdebug && docker-php-ext-enable xdebug

COPY php.ini $PHP_INI_DIR/php.ini
COPY xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

RUN echo "xdebug.remote_host="`/sbin/ip route|awk '/default/ { print $3 }'` >> /usr/local/etc/php/conf.d/xdebug.ini

