FROM php:7.0-fpm

MAINTAINER Alan Boglioli <alan.boglioli@gmail.com>

RUN apt-get update && apt-get install -y \
    libpq-dev \
    libmemcached-dev \
    cron \
    libfreetype6-dev \
    libicu-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng12-dev \
    libxslt1-dev \
    sendmail-bin \
    sendmail \
    curl

# Configure the gd library
RUN docker-php-ext-configure \
  gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

# Install required PHP extensions
RUN docker-php-ext-install \
  gd \
  intl \
  mbstring \
  mcrypt \
  pdo_mysql \
  xsl \
  zip \
  soap
  #pdo_pgsql

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
