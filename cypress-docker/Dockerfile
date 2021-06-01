FROM cypress/browsers:node12.19.0-chrome86-ff82

RUN apt-get update \
    && apt-get install -y docker.io \
    && apt-get clean ; \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

RUN mkdir /app
WORKDIR /app
