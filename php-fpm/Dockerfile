FROM laradock/php-fpm:7.0--1.2

MAINTAINER Matthew Cooper <matthew@debugthat.com>

RUN echo 'deb http://security.debian.org/debian-security jessie/updates main' >> /etc/apt/sources.list
RUN apt-get update
RUN apt-get -y install curl libcurl4-openssl-dev libbz2-dev libicu-dev libxml2-dev libxslt1-dev

RUN docker-php-ext-install \
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

# Copy xdebug configration for remote debugging
COPY ./xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

RUN pecl install zip && \
    docker-php-ext-enable zip

ADD ./pool.conf /usr/local/etc/php-fpm.d/

RUN rm -r /var/lib/apt/lists/*

RUN usermod -u 1000 www-data

WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE 9000ed