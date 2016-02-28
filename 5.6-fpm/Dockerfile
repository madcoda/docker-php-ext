FROM php:5.6-fpm

RUN usermod -u 1000 www-data

# install the PHP extensions we need
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt pdo pdo_mysql mbstring \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

# Customize: Install extra packages you want here
# example: RUN apt-get install -y git


# Remove the junk files that you don't need
RUN rm -rf /var/lib/apt/lists/*