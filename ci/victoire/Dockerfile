FROM php:7.1

ENV DEBIAN_FRONTEND=noninteractive
ENV NPM_CONFIG_LOGLEVEL info
ENV NODE_VERSION 4.1.1

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt bcmath \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

RUN apt-get update && apt-get install mysql-server mysql-client libmysqlclient18 mysql-common nodejs npm nodejs-legacy vim ruby-full git \
    xvfb iceweasel default-jdk elasticsearch redis-server perl pwgen zip unzip libsqlite3-dev curl rabbitmq-server -yqq && \
    apt-get clean

RUN curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz" \
  && tar -xzf "node-v$NODE_VERSION-linux-x64.tar.gz" -C /usr/local --strip-components=1 \
  && rm "node-v$NODE_VERSION-linux-x64.tar.gz"

RUN npm install -g bower less gulp grunt
# runs node.js as a background service
RUN npm i nohup
RUN gem install sass mailcatcher capistrano capistrano-symfony capistrano-composer capistrano-file-permissions

RUN docker-php-ext-install pdo_mysql soap
RUN curl http://selenium-release.storage.googleapis.com/2.53/selenium-server-standalone-2.53.0.jar > selenium-server-standalone-2.53.0.jar
EXPOSE 22 80
RUN curl -L -O https://download.elastic.co/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/2.3.4/elasticsearch-2.3.4.tar.gz
RUN tar -xvf elasticsearch-2.3.4.tar.gz
RUN curl -o- -L https://yarnpkg.com/install.sh | bash

WORKDIR "/var/www/app"
