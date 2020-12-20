FROM php:8.0-apache
COPY ./php.ini /usr/local/etc/php/
RUN apt update \
  && apt install -y libicu-dev autoconf make g++ gcc apt-utils \
  && apt install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev libonig-dev \
  && docker-php-ext-install -j$(nproc) pdo_mysql mysqli gd iconv intl opcache \
  && pecl install xdebug \
  && docker-php-ext-enable xdebug opcache \
  && apt upgrade -y \
  && apt autoremove -y \
  && apt clean -y

RUN { \
  echo 'short_open_tag = On'; \
  echo 'fastcgi.logging = 1'; \
  echo 'opcache.enable=1'; \
  echo 'opcache.optimization_level=0x7FFFBBFF' ; \
  echo 'opcache.revalidate_freq=0'; \
  echo 'opcache.validate_timestamps=1'; \
  echo 'opcache.memory_consumption=128'; \
  echo 'opcache.interned_strings_buffer=8'; \
  echo 'opcache.max_accelerated_files=4000'; \
  echo 'opcache.revalidate_freq=60'; \
  echo 'opcache.fast_shutdown=1'; \
  echo 'xdebug.remote_enable=1'; \
} > /usr/local/etc/php/conf.d/overrides.ini
