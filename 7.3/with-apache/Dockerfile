FROM php:7.3-apache-stretch

LABEL maintainer="danilosilva87@gmail.com"

ENV APACHE_RUN_USER php
ENV APACHE_RUN_GROUP php
ENV APPLICATION \
    git \
    wget \
    curl \
    unzip

ENV PHP_DEPS \
    libpng-dev \
    libjpeg-dev \
    libssl-dev \
    libmcrypt-dev \
    lib32z1-dev \
    libxml2-dev \
    libedit-dev \
    libxslt1-dev \
    libzip-dev

ENV EXTENSION \
    zip \
    pdo \
    pdo_mysql \
    xml \
    json \
    opcache \
    phar \
    readline \
    sockets \
    tokenizer \
    xsl \
    gd \
    mbstring \
    pcntl

RUN groupadd --gid 1000 php \
    && useradd --uid 1000 --gid php -m php

RUN apt-get update \
    && apt-get install -y --no-install-recommends ${PHP_DEPS} ${APPLICATION} \
    && docker-php-ext-install ${EXTENSION} \
    && docker-php-ext-configure gd \
        --with-gd \
        --with-jpeg-dir \
        --with-png-dir \
        --with-zlib-dir \
    && rm -rf /etc/apache2/sites-*/ \
    && chown -R php:php /var/run/apache2 /var/log/apache2 /var/lock/apache2 /var/lib/apache2 \
    && apt-get purge -y --auto-remove \
    && rm -r /var/lib/apt/lists/*

COPY php.ini /usr/local/etc/php/
COPY ports.conf /etc/apache2/ports.conf
COPY sites-enabled/*.conf /etc/apache2/sites-enabled/

RUN ln -sf /dev/stdout /var/log/apache2/access.log
RUN ln -sf /dev/stderr /var/log/apache2/error.log

WORKDIR /home/php/app

RUN a2enmod rewrite ssl \
    && chown php.php -R /home/php

USER php

EXPOSE 8080 4433

CMD ["apache2-foreground"]