FROM php:7.0

ENV DEBIAN_FRONTEND=noninteractive
ENV NPM_CONFIG_LOGLEVEL info
ENV NODE_VERSION 4.1.1

RUN apt-get clean && apt-get update
RUN apt-get install software-properties-common -yqq && add-apt-repository ppa:ondrej/php -y && apt-get update
RUN apt-get install mysql-server mysql-client libmysqlclient18 mysql-common nodejs npm nodejs-legacy vim ruby-full git \
    xvfb iceweasel default-jdk elasticsearch redis-server perl pwgen zip unzip libsqlite3-dev curl php7.0-gd -yqq && \
    apt-get clean

RUN curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz" \
  && tar -xzf "node-v$NODE_VERSION-linux-x64.tar.gz" -C /usr/local --strip-components=1 \
  && rm "node-v$NODE_VERSION-linux-x64.tar.gz"

RUN npm install -g bower less gulp
# runs node.js as a background service
RUN npm i nohup
RUN gem install sass mailcatcher capistrano capistrano-symfony capistrano-composer capistrano-file-permissions

RUN docker-php-ext-install pdo_mysql
RUN curl http://selenium-release.storage.googleapis.com/2.53/selenium-server-standalone-2.53.0.jar > selenium-server-standalone-2.53.0.jar
EXPOSE 22 80
RUN curl -L -O https://download.elastic.co/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/2.3.4/elasticsearch-2.3.4.tar.gz
RUN tar -xvf elasticsearch-2.3.4.tar.gz

WORKDIR "/var/www/app"
