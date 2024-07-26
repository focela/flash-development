FROM php:7.1-fpm-buster
LABEL maintainer="Focela Technologies <opensource@focela.com>"

ARG APP_ID=1000
RUN groupadd -g "$APP_ID" app \
  && useradd -g "$APP_ID" -u "$APP_ID" -d /var/www -s /bin/bash app

RUN mkdir -p /etc/nginx/html /var/www /sock \
  && chown -R app:app /etc/nginx /var/www /usr/local/etc/php/conf.d /sock

RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash -

RUN apt-get update && apt-get install -y \
    cron \
    default-mysql-client \
    git \
    gnupg \
    gzip \
    libbz2-dev \
    libfreetype6-dev \
    libicu-dev \
    libjpeg62-turbo-dev \
    libmagickwand-dev \
    libmcrypt-dev \
    libonig-dev \
    libpng-dev \
    libpq-dev \
    libssh2-1-dev \
    libwebp-dev \
    libxslt1-dev \
    libzip-dev \
    lsof \
    mailutils \
    msmtp \
    nodejs \
    procps \
    strace \
    vim \
    zip \
    zlib1g-dev \
  && rm -rf /var/lib/apt/lists/*

RUN pecl channel-update pecl.php.net && pecl install \
    imagick-3.7.0 \
    redis-4.3.0 \
    ssh2-1.3.1 \
    swoole-5.1.1 \
    xdebug-2.9.8 \
  && pecl clear-cache \
  && rm -rf /tmp/pear

RUN docker-php-ext-configure \
    gd --with-freetype --with-jpeg --with-webp \
  && docker-php-ext-install \
    bcmath \
    bz2 \
    calendar \
    exif \
    gd \
    gettext \
    intl \
    mbstring \
    mysqli \
    opcache \
    pcntl \
    pdo \
    pdo_mysql \
    pdo_pgsql \
    soap \
    sockets \
    sysvmsg \
    sysvsem \
    sysvshm \
    xsl \
    zip

# Install libsodium from source for PHP 7.1
RUN curl -fsSL https://download.libsodium.org/libsodium/releases/libsodium-1.0.18.tar.gz -o libsodium.tar.gz \
  && mkdir -p libsodium \
  && tar -xzf libsodium.tar.gz -C libsodium --strip-components=1 \
  && cd libsodium \
  && ./configure \
  && make && make install \
  && cd .. \
  && rm -rf libsodium libsodium.tar.gz

RUN version=$(php -r "echo PHP_MAJOR_VERSION.PHP_MINOR_VERSION;") \
    && architecture=$(uname -m) \
    && curl -A "Docker" -o /tmp/blackfire-probe.tar.gz -D - -L -s https://blackfire.io/api/v1/releases/probe/php/linux/$architecture/$version \
    && mkdir -p /tmp/blackfire \
    && tar zxpf /tmp/blackfire-probe.tar.gz -C /tmp/blackfire \
    && mv /tmp/blackfire/blackfire-*.so $(php -r "echo ini_get ('extension_dir');")/blackfire.so \
    && rm -rf /tmp/blackfire /tmp/blackfire-probe.tar.gz

RUN git clone --branch v0.4.15 --depth=1 https://github.com/NoiseByNorthwest/php-spx.git /usr/lib/php-spx \
    && cd /usr/lib/php-spx \
    && phpize \
    && ./configure \
    && make \
    && make install

RUN curl -sS https://getcomposer.org/installer | \
  php -- --version=2.2.18 --install-dir=/usr/local/bin --filename=composer

COPY ./conf/blackfire.ini $PHP_INI_DIR/conf.d/blackfire.ini
COPY ./conf/msmtprc /etc/msmtprc
COPY ./conf/php-fpm.conf /usr/local/etc/
COPY ./conf/php.ini $PHP_INI_DIR
COPY ./conf/spx.ini $PHP_INI_DIR/conf.d/spx.ini
COPY ./conf/www.conf /usr/local/etc/php-fpm.d/

USER app:app

VOLUME /var/www
WORKDIR /var/www
