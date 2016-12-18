FROM php:7.0-fpm

MAINTAINER Matthew Cooper <matthew@debugthat.com>

RUN echo 'deb http://security.debian.org/debian-security jessie/updates main' >> /etc/apt/sources.list && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
        curl \
        libmemcached-dev \
        libz-dev \
        libpq-dev \
        libjpeg-dev \
        libpng12-dev \
        libfreetype6-dev \
        libssl-dev \
        libmcrypt-dev \
        libcurl4-openssl-dev \
        libbz2-dev \
        libicu-dev \
        libxml2-dev \
        libxslt1-dev

# Install the PHP gd library
RUN docker-php-ext-configure gd \
        --enable-gd-native-ttf \
        --with-jpeg-dir=/usr/lib \
        --with-freetype-dir=/usr/include/freetype2

RUN docker-php-ext-install \
    mcrypt \
    pdo_mysql \
    bcmath \
    gd \
    intl \
    mbstring \
    xsl \
    iconv \
    curl \
    bz2 \
    mysqli \
    soap

RUN pecl install xdebug && \
    docker-php-ext-enable xdebug
COPY ./xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

RUN pecl install zip && \
    docker-php-ext-enable zip

ADD ./pool.conf /usr/local/etc/php-fpm.d/

RUN rm -r /var/lib/apt/lists/*

RUN usermod -u 1000 www-data

WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE 9000ed