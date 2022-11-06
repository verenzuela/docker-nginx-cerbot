FROM node:alpine AS node

FROM php:7.3.15-fpm-alpine

COPY --from=node /usr/lib /usr/lib
COPY --from=node /usr/local/share /usr/local/share
COPY --from=node /usr/local/lib /usr/local/lib
COPY --from=node /usr/local/include /usr/local/include
COPY --from=node /usr/local/bin /usr/local/bin

RUN apk add --no-cache freetype libpng libjpeg-turbo freetype-dev libpng-dev libjpeg-turbo-dev && \
  docker-php-ext-configure gd \
    --with-gd \
    --with-freetype-dir=/usr/include/ \
    --with-png-dir=/usr/include/ \
    --with-jpeg-dir=/usr/include/ && \
  NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) && \
  docker-php-ext-install -j${NPROC} gd && \
  apk del --no-cache freetype-dev libpng-dev libjpeg-turbo-dev

RUN apk --update add wget \  
  libzip-dev \
  zip \
  curl \
  git \
  grep \
  build-base \
  libmemcached-dev \
  libmcrypt-dev \
  libxml2-dev \
  imagemagick-dev \
  pcre-dev \
  libtool \
  make \
  autoconf \
  g++ \
  cyrus-sasl-dev \
  libgsasl-dev \
  supervisor

RUN docker-php-ext-install zip mysqli mbstring pdo pdo_mysql tokenizer xml && \
  pecl channel-update pecl.php.net \
  && pecl install memcached \
  && pecl install imagick \
  && pecl install mcrypt-1.0.2 \
  && docker-php-ext-enable memcached \
  && docker-php-ext-enable imagick \
  && docker-php-ext-enable mcrypt

RUN rm /var/cache/apk/* && \
    mkdir -p /var/www

#ADD php/uploads.ini /usr/local/etc/php/conf.d/uploads.ini
