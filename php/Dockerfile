ARG PHP_VERSION=""
FROM php:${PHP_VERSION:+${PHP_VERSION}-}fpm-alpine
LABEL maintainer="Cristian Pini"

RUN apk update; \
    apk upgrade; \
    apk add freetype freetype-dev libxslt-dev libpng libjpeg libxml2-dev zlib libwebp-dev libpng-dev jpeg-dev icu-dev;

RUN docker-php-ext-configure gd --with-png-dir=/usr/include/ \
                                   --with-jpeg-dir=/usr/include/ \
                                   --with-webp-dir=/usr/include/ \
                                   --with-freetype-dir=/usr/inlcude/ \
 && docker-php-ext-install mysqli bcmath gd pdo_mysql soap xsl zip intl;