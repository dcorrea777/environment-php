FROM nginx:1.19-alpine

RUN set -x \
    && addgroup -g 1000 php \
    && adduser -u 1000 -D -G php php

WORKDIR /home/php/app

RUN rm -rf /etc/nginx/conf.d/*.conf

COPY localhost.conf /etc/nginx/conf.d/localhost.conf
COPY nginx.conf /etc/nginx/nginx.conf

RUN touch /var/run/nginx.pid \
    && chown -R php:php /var/run/nginx.pid \
    && chown -R php:php /var/cache/nginx/ \
    && chown -R php:php /var/log/nginx/

USER php

EXPOSE 8080
