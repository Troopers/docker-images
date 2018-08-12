FROM php:7.1-fpm
ARG TIMEZONE=Europe/Paris

# “apt-transport-https”, “lsb-release”, and “build-essential” are dependencies of nodejs, they are installed by the
# “nodesource_setup.sh” script
# ruby-full is necessary to get the “gem” binary
RUN apt-get update && apt-get install -y \
    openssl \
    git \
    unzip \
    curl \
    gnupg \
    netcat \
    apt-transport-https lsb-release build-essential \
    ruby-full \
    libfreetype6-dev libjpeg62-turbo-dev libpng-dev

# Set timezone
RUN ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && echo ${TIMEZONE} > /etc/timezone
RUN printf '[PHP]\ndate.timezone = "%s"\n', ${TIMEZONE} > /usr/local/etc/php/conf.d/tzone.ini && date

# Type docker-php-ext-install to see available extensions
RUN docker-php-ext-install pdo pdo_mysql
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

# patch
RUN echo "memory_limit=384M" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

RUN echo 'alias ll="ls -lh"' >> ~/.bashrc \
    && echo 'alias sf="php app/console"' >> ~/.bashrc \
    && echo 'alias sf3="php bin/console"' >> ~/.bashrc

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

##### Front #####
# Install node
# https://github.com/maxpou/docker-symfony/issues/25#issuecomment-337843548
# This script runs sudo apt-get update
RUN curl -sL https://deb.nodesource.com/setup_8.x -o nodesource_setup.sh \
    && bash nodesource_setup.sh \
    && apt-get install -y nodejs

# Front dependencies
RUN gem install sass

RUN npm -g install \
    yarn bower less@2.7.2 gulp@3.9.1 \
    && npm install --unsafe-perm node-sass

RUN apt-get clean

WORKDIR /var/www/symfony
