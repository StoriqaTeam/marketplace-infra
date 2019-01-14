FROM php:7.3-apache-stretch

ARG subpath=blog

RUN openssl req \
    -x509 \
    -newkey rsa:4096 \
    -days 365 \
    -nodes \
    -subj '/CN=*' \
    -keyout /etc/ssl/private/ssl-cert-snakeoil.key \
    -out /etc/ssl/certs/ssl-cert-snakeoil.pem \
  && apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libmemcached-dev \
        zlib1g-dev \
  && docker-php-ext-install -j$(nproc) iconv \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install -j$(nproc) gd \
  && docker-php-ext-install mysqli \
  && docker-php-ext-install pdo_mysql

COPY $subpath/wordpress /var/www/html/$subpath
COPY $subpath/apache2 /etc/apache2

VOLUME /var/www/html/$subpath
