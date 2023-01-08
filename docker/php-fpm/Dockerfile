FROM phpdockerio/php:7.4-fpm

RUN apt update \
    && apt -y --no-install-recommends install \
    curl \
    wget \
    git \
    unzip \
    rsync \
    php7.4-memcached \
    php7.4-memcache \
    php7.4-mbstring \
    php7.4-mysql \
    php7.4-intl \
    php7.4-xdebug \
    php7.4-soap \
    php7.4-gd \
    php7.4-imagick \
    php7.4-opcache \
    php7.4-zip \
    php7.4-mcrypt \
    php7.4-vips \
    php7.4-curl \
    php7.4-xml \
    && apt clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# DO NOT install php7.4-xdebug package for site running in production! It will slow it down significantly.

COPY php.ini /etc/php/7.4/fpm/conf.d/90-php.ini
COPY php.ini /etc/php/7.4/cli/conf.d/90-php.ini

# Sendmail
RUN apt install --no-install-recommends --assume-yes --quiet ca-certificates \
    && rm -rf /var/lib/apt/lists/* \
    && curl -Lsf 'https://storage.googleapis.com/golang/go1.8.3.linux-amd64.tar.gz' | tar -C '/usr/local' -xvzf -
ENV PATH /usr/local/go/bin:$PATH
RUN go get github.com/mailhog/mhsendmail \
    && cp /root/go/bin/mhsendmail /usr/bin/mhsendmail

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN usermod -u 1000 www-data

RUN chmod 777 -R /tmp && chmod o+t -R /tmp

WORKDIR "/var/www/test.loc"

EXPOSE 9000
