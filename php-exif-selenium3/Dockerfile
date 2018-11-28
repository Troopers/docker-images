FROM php:7.1

ENV DEBIAN_FRONTEND=noninteractive
ENV NPM_CONFIG_LOGLEVEL info

RUN apt-get update && apt-get install -y \
    libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev libpng-dev \
    zlib1g-dev libicu-dev g++ apt-transport-https netcat \
    mysql-server mysql-client mysql-common vim ruby-full git \
    xvfb chromium chromium-l10n perl pwgen zip unzip libsqlite3-dev curl libxml2-dev \
    gnupg

RUN docker-php-ext-install -j$(nproc) iconv mcrypt bcmath mbstring \
    && docker-php-ext-configure intl && docker-php-ext-install intl \
    && docker-php-ext-install zip exif \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install pdo_mysql soap \
    # Support “easter_date” function
    && docker-php-ext-install calendar && docker-php-ext-configure calendar \
    # For “app/console server:start” command
    && docker-php-ext-install pcntl

# Install APCu
RUN pecl install apcu \
    && echo "extension=apcu.so" > /usr/local/etc/php/conf.d/apcu.ini

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
    apt-get update && apt-get install -y nodejs && \
    npm install npm@latest -g

RUN apt-get install -y default-jdk

RUN apt-get clean

RUN curl http://selenium-release.storage.googleapis.com/3.141.59/selenium-server-standalone-3.141.59.jar > selenium-server-standalone-3.141.59.jar

RUN gem install sass

EXPOSE 22 80

WORKDIR "/var/www/app"
