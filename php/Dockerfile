ARG PHP_VERSION=""
FROM php:${PHP_VERSION:+${PHP_VERSION}-}fpm-alpine
LABEL maintainer="Cristian Pini"
ENV TZ=Europe/London
RUN apk update; \
    apk upgrade; \
    apk add --no-cache tzdata freetype freetype-dev libxslt-dev libpng libjpeg libxml2-dev zlib libwebp-dev libpng-dev jpeg-dev icu-dev zlib-dev libzip-dev; \
    apk add --no-cache $PHPIZE_DEPS && pecl install xdebug-2.7.2; 

RUN docker-php-ext-configure gd --with-png-dir=/usr/include/ \
                                   --with-jpeg-dir=/usr/include/ \
                                   --with-webp-dir=/usr/include/ \
                                   --with-freetype-dir=/usr/inlcude/ \
 && docker-php-ext-configure zip --with-libzip \
 && docker-php-ext-install mysqli bcmath gd pdo_mysql soap xsl zip intl opcache \
 && docker-php-ext-enable xdebug;
COPY xdebug.ini /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
COPY memory-limit-php.ini /usr/local/etc/php/conf.d/memory-limit-php.ini
COPY max-input-vars-php.ini /usr/local/etc/php/conf.d/max-input-vars-php.ini
RUN chown -hR www-data:www-data /var/www/html 
USER www-data