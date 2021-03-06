FROM php:7.3-fpm

RUN apt-get update \
    && apt-get install -y git curl wget grep \
    libmemcached-dev zlib1g-dev libfreetype6-dev libcurl4-openssl-dev libssl-dev libpq-dev \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && pecl install -of xdebug && docker-php-ext-enable xdebug \
    && pecl install -of redis && docker-php-ext-enable redis \
    && pecl install -of memcached && docker-php-ext-enable memcached \
    && docker-php-ext-install pdo pdo_pgsql \
    && docker-php-ext-install sockets \
    && pecl install -of raphf && docker-php-ext-enable raphf \
    && pecl install -of propro && docker-php-ext-enable propro \
    && pecl install -of pecl_http && echo "extension=http.so" >> /usr/local/etc/php/conf.d/docker-php-ext-zhttp.ini
RUN groupadd -g 3000  nginx \
    && useradd -u 3000 -g nginx nginx \
    && chmod -R 777 /var/run

WORKDIR /var/www/html

CMD ["php-fpm"]