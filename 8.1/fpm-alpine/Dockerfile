FROM php:8.1-fpm-alpine

RUN set -x \
    && addgroup -g 1000 php \
    && adduser -u 1000 -D -G php php

WORKDIR /home/php/app

RUN apk add --no-cache \
    zip \
    libzip-dev \
    libxml2-dev \
    libedit-dev \
    libxslt-dev \
    libpng-dev \
    freetype-dev \
    libjpeg-turbo-dev \
    libressl-dev \
    oniguruma-dev

ENV EXTENSION_PHP="zip pdo pdo_mysql opcache sockets xsl pcntl phar mbstring bcmath gd"

RUN docker-php-ext-install ${EXTENSION_PHP} \
    && docker-php-ext-configure gd \
        --with-jpeg=/usr/include/ \
        --with-freetype=/usr/include/

COPY www.conf /usr/local/etc/php-fpm.d/www.conf

USER php
