FROM php:7.2-apache
ENV DEBIAN_FRONTEND=noninteractive
ENV COMPOSER_ALLOW_SUPERUSER=1

RUN apt-get update && apt-get install -y apt-utils

RUN apt-get install -y bash \
    libfreetype6-dev \
    libmcrypt-dev \
    zlib1g-dev \
    libicu-dev \
    g++ \
    apt-transport-https \
    zip \
    unzip \
    libxml2-dev \
    wget \
    vim \
    git \
    libmemcached-dev \
    libpq-dev \
    netcat \
    cron

RUN docker-php-ext-install -j$(nproc) iconv \
    bcmath \
    mbstring \
    pdo \
    pdo_pgsql

RUN docker-php-ext-configure intl && docker-php-ext-install intl \
    zip \
    soap \
    gd

RUN apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer global require "hirak/prestissimo:^0.3"

RUN a2enmod rewrite ssl

RUN mkdir /app
WORKDIR /app

EXPOSE 80
