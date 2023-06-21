# указываем образ от которого будем наследоваться
FROM php:8.2-fpm

# набор Linux команд, которые будут выполняться при развертывании контейнера
RUN apt-get update && apt-get install -y \
      apt-utils \
      libpq-dev \
      libpng-dev \
      libzip-dev \
      zip unzip \
      git && \
      docker-php-ext-install pdo_mysql && \
      docker-php-ext-install bcmath && \
      docker-php-ext-install gd && \
      docker-php-ext-install zip && \
      apt-get clean && \
      rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# заменяем дефолтный php.ini на свой
COPY ./app/php.ini /usr/local/etc/php/conf.d/php.ini

# задаем переменную среды, чтобы композер ходил под рутом
ENV COMPOSER_ALLOW_SUPERUSER=1
# Установка композера
RUN curl -sS https://getcomposer.org/installer | php -- \
    --filename=composer \
    --install-dir=/usr/local/bin

# рабочий каталог контейнера
WORKDIR /var/www
