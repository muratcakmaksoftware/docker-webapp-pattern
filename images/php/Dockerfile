FROM php:8.1.6-fpm-alpine3.14

#intl için icu-dev gereklidir
#libzip-dev zip/unzip için gerekli C kütüphaneleridir.
#opcache önceden derlenmiş olan php betiğini cacheleyip tekrar çağrıldığında hızlı cevap vermesini sağlayan teknolojidir.

# MYSQL için gerekli bağımlıklar ve eklentiler Not: mysqli gerekli olmayabilir.
#mysqli \
#pdo \
#pdo_mysql \
#&& docker-php-ext-enable \
#pdo_mysql

# Postgresql için bağımlıklar ve eklentiler
#apk add postgresql-libs postgresql-dev \
#&& docker-php-ext-install pgsql pdo_pgsql \
#&& apk del postgresql-dev

#Composer Yüklemek için
#ÖNERİLEN:
#COPY --from=composer /usr/bin/composer /usr/bin/composer4
#VEYA ayrı bir RUN olarak çalışması gerekmektedir.
#RUN curl -s https://getcomposer.org/installer | php

#docker-compose.yml tarafından tetiklenir ve her container çalıştığında bootstrap.sh çalışacaktır.
COPY bootstrap.sh /startup/

RUN apk update \
    && apk add --no-cache \
    bash \
    libzip-dev \
    zip \
    unzip \
    icu-dev \
    postgresql-libs \
    postgresql-dev \
    && docker-php-ext-configure \
    intl \
    && docker-php-ext-install \
    intl \
    opcache \
    pgsql \
    pdo_pgsql \
    && apk del  \
    postgresql-dev \
    && chmod -R 777 /startup/bootstrap.sh

