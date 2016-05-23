FROM php:7.0-fpm

MAINTAINER Alan Boglioli <alan.boglioli@gmail.com>

RUN apt-get update && apt-get install -y \
    libpq-dev \
    libmemcached-dev \
    curl

# Install extensions using the helper script provided by the base image
RUN docker-php-ext-install pdo_mysql #pdo_pgsql (for PostgreSQL)

RUN docker-php-ext-install mysqli \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install zip

# Install Memcached for php 7
RUN curl -L -o /tmp/memcached.tar.gz "https://github.com/php-memcached-dev/php-memcached/archive/php7.tar.gz" \
    && mkdir -p /usr/src/php/ext/memcached \
    && tar -C /usr/src/php/ext/memcached -zxvf /tmp/memcached.tar.gz --strip 1 \
    && docker-php-ext-configure memcached \
    && docker-php-ext-install memcached \
    && rm /tmp/memcached.tar.gz

RUN usermod -u 1000 www-data

WORKDIR /var/www/public

CMD ["php-fpm"]

EXPOSE 9000
