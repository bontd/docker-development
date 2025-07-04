FROM php:8.2-fpm-bookworm
LABEL maintainer="xavia Technologies <opensource@xavia.com>"

ARG APP_ID=1000
RUN groupadd -g "$APP_ID" app \
  && useradd -g "$APP_ID" -u "$APP_ID" -d /var/www -s /bin/bash app

RUN mkdir -p /etc/nginx/html /var/www /sock \
  && chown -R app:app /etc/nginx /var/www /usr/local/etc/php/conf.d /sock

RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash -

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
    libsodium-dev \
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
    redis-6.0.2 \
    ssh2-1.3.1 \
    swoole-5.1.1 \
    xdebug-3.2.2 \
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
    sodium \
    sysvmsg \
    sysvsem \
    sysvshm \
    xsl \
    zip \
  && docker-php-ext-enable \
    imagick \
    redis \
    ssh2 \
    xdebug

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
