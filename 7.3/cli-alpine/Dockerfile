FROM php:7.3-cli-alpine

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
    libressl-dev

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
    && docker-php-ext-configure zip --with-libzip=/usr/include \
    && docker-php-ext-configure gd \
        --with-gd \
        --with-jpeg-dir \
        --with-png-dir \
        --with-zlib-dir

USER php

CMD ["php", "-v"]
