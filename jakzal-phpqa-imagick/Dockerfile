FROM jakzal/phpqa:php7.1-alpine

# Install Imagick
# source: https://gist.github.com/johndatserakis/825a16a7f3cef4e8b4dbfbb1e80b9f9c
RUN apk add --no-cache --virtual .phpize-deps $PHPIZE_DEPS imagemagick-dev libtool \
    && export CFLAGS="$PHP_CFLAGS" CPPFLAGS="$PHP_CPPFLAGS" LDFLAGS="$PHP_LDFLAGS" \
    && pecl install imagick-3.4.3 \
    && docker-php-ext-enable imagick \
    && apk add --no-cache --virtual .imagick-runtime-deps imagemagick \
    && apk del .phpize-deps
