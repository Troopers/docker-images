FROM ruby:2.3-slim

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y ruby-dev libxml++2.6-dev \
    # includes gcc and make
    build-essential

RUN apt-get clean

RUN gem install bundler

ADD Gemfile /install/Gemfile

RUN cd /install && bundle install
