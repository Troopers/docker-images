FROM nginx:1.14

# update the repository sources list
# and install dependencies
RUN apt-get update \
    && apt-get install -y curl gnupg bzip2 make gcc libpng-dev wget \
    && apt-get -y autoclean

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - \
    && apt-get install -y nodejs && npm i -g yarn

# Install Google Chrome
# A specific version is set in google chrome install cmd
# Google delete old version from the repository
# Change the version is it doesn't exist anymore
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
RUN apt-get update && apt-get install -y google-chrome-stable

WORKDIR /app
