FROM php:7.4-fpm

RUN apt update && apt install -y \
        curl \
        wget \
        git \
        unzip \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libonig-dev \
        libzip-dev \
        libmcrypt-dev \
        libmemcached-dev \
        zlib1g-dev \
        libvips-dev \
        libcurl4-openssl-dev \
        libcurl4 \
    && pecl install mcrypt-1.0.5 \
    && pecl install xdebug-3.1.6 \
    && pecl install memcached-3.2.0 \
    && pecl install memcache-4.0.5.2 \
    && pecl install vips-1.0.13 \
    && pecl install imagick-3.7.0 \
	&& docker-php-ext-enable mcrypt xdebug memcached memcache vips imagick \
    && docker-php-ext-install -j$(nproc) iconv mbstring mysqli pdo_mysql zip intl soap opcache xml curl \
	&& docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

ADD php.ini /usr/local/etc/php/conf.d/40-custom.ini

RUN usermod -u 1000 www-data

WORKDIR '/var/www'

EXPOSE 9000