FROM ruby:2.3

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y ruby-full

RUN apt-get clean

RUN gem install bundler

ADD Gemfile /install/Gemfile

RUN cd /install && bundle install
