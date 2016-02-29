FROM php:5.6-fpm

RUN usermod -u 1000 www-data

# install the PHP extensions we need
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev && \
    docker-php-ext-install -j$(nproc) iconv \
    									 mcrypt \
    									 pdo \
    									 pdo_mysql \
    									 mbstring \
    									 mysqli \
    									 opcache \
                                         zip \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

# set recommended PHP.ini settings
# see https://secure.php.net/manual/en/opcache.installation.php
RUN { \
		echo 'opcache.memory_consumption=128'; \
		echo 'opcache.interned_strings_buffer=8'; \
		echo 'opcache.max_accelerated_files=4000'; \
		echo 'opcache.revalidate_freq=60'; \
		echo 'opcache.fast_shutdown=1'; \
		echo 'opcache.enable_cli=1'; \
	} > /usr/local/etc/php/conf.d/opcache-recommended.ini


# Customize: Install extra packages you want here
# example: RUN apt-get install -y git


# Remove the junk files that you don't need
RUN rm -rf /var/lib/apt/lists/*