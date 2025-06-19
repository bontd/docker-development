FROM php:7.4-fpm

# Cài các gói cần thiết cho PHP và build
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
    gnupg \
    pkg-config \
    software-properties-common \
    build-essential \
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

# Cài Node.js & npm (phiên bản 18 LTS)
RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash - && \
    apt-get install -y nodejs && \
    npm install -g npm@latest

# Dọn dẹp cache để giảm kích thước image
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Thiết lập thư mục làm việc
WORKDIR /var/www
