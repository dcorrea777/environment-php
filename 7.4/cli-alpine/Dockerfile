FROM php:7.4-cli-alpine

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

ENV EXTENSION_PHP \
    zip \
    pdo \
    pdo_mysql \
    xml \
    json \
    opcache \
    readline \
    sockets \
    tokenizer \
    xsl \
    gd \
    mbstring \
    pcntl \
    phar \
    bcmath


RUN docker-php-ext-install ${EXTENSION_PHP} \
    && docker-php-ext-configure gd \
        --with-jpeg=/usr/include/ \
        --with-freetype=/usr/include/

USER php

CMD ["php", "-v"]
