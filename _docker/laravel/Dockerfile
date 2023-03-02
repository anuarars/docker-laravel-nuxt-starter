# Start with a PHP image
FROM php:8.1-fpm

# Install required extensions
RUN docker-php-ext-install pdo_mysql

RUN apt-get update && apt-get install -y \
    zlib1g-dev \
    libzip-dev \
    unzip
RUN docker-php-ext-install zip

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php --install-dir=/bin --filename=composer && \
    php -r "unlink('composer-setup.php');"

# Set working directory
WORKDIR /var/www/laravel

# Copy project files to the working directory
COPY laravel /var/www/laravel

# Run the Artisan command
RUN composer install

# Copy the .env file to the container
COPY laravel/.env.example /var/www/laravel/.env

# Set permissions on the storage directory
RUN chmod -R 777 storage
RUN chmod -R 777 bootstrap

# Delete any existing Laravel cache files
RUN php artisan cache:clear

# Set the APP_KEY value
ENV APP_KEY=base64:eXdjcGdsMnR6cG50bnV4dnk2YXF3ZnJuNHUyZGpxazM=

RUN php artisan optimize
RUN php artisan key:generate
# RUN php artisan migrate

# Expose port 9000 for FastCGI
EXPOSE 9000
EXPOSE 8000