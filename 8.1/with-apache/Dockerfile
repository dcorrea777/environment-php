FROM php:8.1-apache-bookworm

LABEL maintainer="danilosilva87@gmail.com"

ENV APACHE_RUN_USER=php
ENV APACHE_RUN_GROUP=php
ENV APACHE_SERVER_NAME=localhost
ENV APACHE_DOCUMENT_ROOT=/home/php/app/public
ENV APACHE_LOG_DIR=/var/log/apache2

RUN set -x \
    && groupadd --gid 1000 php \
    && useradd --uid 1000 --gid php -m php

RUN apt-get update -y \
    && apt-get install -y --no-install-recommends \
    libpng-dev \
    libjpeg-dev \
    libssl-dev \
    libmcrypt-dev \
    lib32z1-dev \
    libxml2-dev \
    libedit-dev \
    libxslt1-dev \
    libonig-dev \
    libzip-dev

ENV EXTENSION_PHP="zip pdo pdo_mysql opcache sockets xsl pcntl phar mbstring bcmath gd xml"

RUN docker-php-ext-install ${EXTENSION_PHP} \
    && docker-php-ext-configure gd --with-jpeg=/usr/include/ \
    && rm -rf /etc/apache2/sites-*/ \
    && chown -R php:php /var/run/apache2 /var/log/apache2 /var/lock/apache2 /var/lib/apache2 \
    && apt-get purge -y --auto-remove \
    && rm -r /var/lib/apt/lists/*

COPY php.ini /usr/local/etc/php/
COPY ports.conf /etc/apache2/ports.conf
COPY sites-enabled/*.conf /etc/apache2/sites-enabled/

WORKDIR /home/php/app

RUN a2enmod rewrite ssl \
    && chown php.php -R /home/php

USER php

RUN ln -sf /dev/stdout ${APACHE_LOG_DIR}/access.log
RUN ln -sf /dev/stderr ${APACHE_LOG_DIR}/error.log

EXPOSE 8080 4433

CMD ["apache2-foreground"]
