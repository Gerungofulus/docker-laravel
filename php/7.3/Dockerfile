FROM php:7.3-fpm-alpine

MAINTAINER JG <julien@mangue.eu>

RUN apk add --no-cache --virtual .build-deps \
        $PHPIZE_DEPS \
        curl-dev \
        imagemagick-dev \
        libtool \
        libxml2-dev \
        postgresql-dev \
        sqlite-dev \
    && apk add --no-cache \
        curl \
        git \
        imagemagick \
        mysql-client \
        postgresql-libs \
        libintl \
        icu \
        icu-dev \
        libzip-dev \
        chromium \
        nss \
        freetype \
        freetype-dev \
        libpng \
        libjpeg-turbo \
        libpng-dev \
        libjpeg-turbo-dev \
        harfbuzz \ca-certificates \
        ttf-freefont \
        nodejs \
        yarn \
        npm \
        bash \
        openssh \
    && pecl install imagick \
    && docker-php-ext-enable imagick \
    && docker-php-ext-install \
        bcmath \
        curl \
        iconv \
        mbstring \
        pdo \
        pdo_mysql \
        pdo_pgsql \
        pdo_sqlite \
        pcntl \
        tokenizer \
        xml \
        zip \
        intl \
    && docker-php-ext-configure gd \
    --with-gd \
    --with-freetype-dir=/usr/include/ \
    --with-png-dir=/usr/include/ \
    --with-jpeg-dir=/usr/include/ && \
      NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) && \
      docker-php-ext-install -j${NPROC} gd && \
      apk del --no-cache freetype-dev libpng-dev libjpeg-turbo-dev \
    && curl -s https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer \
    && composer global require laravel/envoy \
    && npm install backstopjs -g --unsafe-perm=true \
    && apk del -f .build-deps

WORKDIR /var/www
