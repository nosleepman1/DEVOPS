FROM php:8.3-cli-alpine

WORKDIR /var/www

RUN apk add --no-cache \
    libxml2-dev \
    oniguruma-dev \
    libzip-dev \
    zip \
    unzip

RUN docker-php-ext-install pdo pdo_mysql mbstring xml

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

COPY composer.lock composer.json ./

RUN composer install --no-scripts --no-autoloader

COPY . .

RUN composer dump-autoload --optimize

RUN php artisan key:generate --ansi

EXPOSE 8000

CMD [ "php", "artisan", "serve", "--host=0.0.0.0", "--port=8000" ]
