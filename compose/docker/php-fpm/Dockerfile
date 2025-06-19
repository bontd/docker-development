FROM php:7.4-fpm

# Cài các gói cần thiết
RUN apt-get update && apt-get install -y \
    libzip-dev \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libwebp-dev \
    libxpm-dev \
    libonig-dev \
    libxml2-dev \
    libicu-dev \
    libxslt1-dev \
    libmpdec-dev \
    libpq-dev \
    unzip \
    zip \
    git \
    curl \
    pkg-config \
    && docker-php-ext-configure gd \
        --with-freetype \
        --with-jpeg \
        --with-webp \
        --with-xpm \
    && docker-php-ext-install \
        pdo \
        pdo_mysql \
        pdo_pgsql \
        zip \
        gd \
        exif \
    && pecl install decimal \
    && docker-php-ext-enable decimal

# Cài Composer
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer

# Thiết lập working directory
WORKDIR /var/www
