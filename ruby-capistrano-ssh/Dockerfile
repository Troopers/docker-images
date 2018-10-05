FROM ruby:2.3-alpine

RUN apk add --no-cache --update openssh

RUN gem install bundler

ADD Gemfile .

RUN bundle install

RUN cap --help
