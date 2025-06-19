FROM php:7.4-fpm

# Cài các thư viện hệ thống cần thiết
RUN apt-get update && apt-get install -y \
    libpq-dev \
    libzip-dev \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    unzip \
    zip \
    git \
    curl \
    libonig-dev \
    libxml2-dev \
    libicu-dev \
    libxslt1-dev \
    libgmp-dev \
    libwebp-dev \
    libxpm-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp \
    && docker-php-ext-install \
        pdo \
        pdo_mysql \
        pdo_pgsql \
        zip \
        gd

# Cài PHP extension decimal qua PECL
RUN pecl install decimal \
    && docker-php-ext-enable decimal

# Cài Composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer
