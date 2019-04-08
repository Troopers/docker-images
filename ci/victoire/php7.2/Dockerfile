FROM php:7.2

ENV DEBIAN_FRONTEND=noninteractive
ENV NPM_CONFIG_LOGLEVEL info
ENV COMPOSER_ALLOW_SUPERUSER=1

RUN apt-get update && apt-get install -y gnupg

RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
  echo "deb http://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

RUN apt-get update && apt-get install -yq \
        libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev libpng-dev \
        zlib1g-dev libicu-dev g++ apt-transport-https \
        mysql-client mysql-common ruby-dev git \
        xvfb firefox-esr libsqlite3-dev curl libxml2-dev \
        libmemcached-dev yarn
RUN apt-get install libmcrypt-dev \
    && pecl install mcrypt-1.0.1
RUN docker-php-ext-install -j$(nproc) bcmath \
    && docker-php-ext-configure intl \ 
    && docker-php-ext-install intl zip \
    && docker-php-ext-configure mbstring \ 
    && docker-php-ext-install mbstring \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install pdo_mysql

# Imagick
RUN apt-get install -yq libmagickwand-6.q16-dev --no-install-recommends \
   && ln -s /usr/lib/x86_64-linux-gnu/ImageMagick-6.8.9/bin-Q16/MagickWand-config /usr/bin \
   && pecl install imagick \
   && echo "extension=imagick.so" > /usr/local/etc/php/conf.d/ext-imagick.ini

# Memcached
RUN git clone https://github.com/php-memcached-dev/php-memcached /usr/src/php/ext/memcached \
  && cd /usr/src/php/ext/memcached && git checkout -b php7 origin/php7 \
  && docker-php-ext-configure memcached \
  && docker-php-ext-install memcached

# Front dependencies
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
    apt-get update && apt-get install -y nodejs && \
    npm install npm@latest -g

RUN npm install -g bower less@2.7.2 gulp grunt

RUN gem install sass

RUN apt-get install -yq default-jdk

# Clean up
RUN apt-get clean

RUN curl http://selenium-release.storage.googleapis.com/2.53/selenium-server-standalone-2.53.0.jar > /selenium-server-standalone-2.53.0.jar

RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer global require "hirak/prestissimo:^0.3"

EXPOSE 80

WORKDIR "/var/www/app"
