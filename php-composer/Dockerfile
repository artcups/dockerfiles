FROM php:7.4-apache
LABEL maintainer="Sebastian Lundh <s.lundh@gmail.com>"

# Install php extensions (see https://hub.docker.com/_/php/)
RUN apt-get update && apt-get install -y \
   libfreetype6-dev \
   libjpeg62-turbo-dev \
   libmcrypt-dev \
   libxml2-dev \
   libpng-dev \
   zlib1g-dev \
   libzip-dev \
   && pecl install redis \
   && pecl install apcu \
   && docker-php-ext-install pdo \
   && docker-php-ext-install pdo_mysql \
   && docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
   && docker-php-ext-install gd \
   && docker-php-ext-install zip \
   && docker-php-ext-enable redis \
   && docker-php-ext-enable apcu

RUN a2enmod rewrite proxy_http mime_magic headers

COPY --from=composer:1.8 /usr/bin/composer /usr/bin/composer
