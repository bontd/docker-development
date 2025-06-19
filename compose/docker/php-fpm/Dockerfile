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
    gnupg \
    apt-transport-https \
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

# Cài Node.js 18 và npm đi kèm (đã ổn định)
RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash - && \
    apt-get install -y nodejs

# (Tùy chọn) Hạ npm nếu cần, nhưng Node 18 mặc định đã kèm npm 10.x
# RUN npm install -g npm@9

# Thiết lập thư mục làm việc
WORKDIR /var/www

# Thêm node_modules vào PATH nếu muốn gọi npm từ các script khác
ENV PATH="/var/www/node_modules/.bin:$PATH"
