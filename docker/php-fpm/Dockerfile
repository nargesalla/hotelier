ARG PHP_VERSION
FROM php:${PHP_VERSION}-fpm

# Install APT packages, PHP Extensions and Nginx
RUN apt-get update && apt-get install -y \
		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libpng-dev \
		libgmp3-dev \
		libzip-dev \
		libonig-dev \
		libicu-dev \
		curl \
		zip \
		procps \
	&& docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
    && docker-php-ext-configure intl \
	&& docker-php-ext-install -j$(nproc) gd gmp \
	&& docker-php-ext-install pdo pdo_mysql mysqli mbstring zip exif pcntl intl

# Install composer
ARG COMPOSER_VERSION
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer --version=${COMPOSER_VERSION} && \
    composer global require hirak/prestissimo

#
#--------------------------------------------------------------------------
# Final Touch
#--------------------------------------------------------------------------
#

USER root

RUN usermod -u 1000 www-data

WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE 9000