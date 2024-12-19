#
# Build the app
# the official PHP image with Apache as the web server.
FROM php:7.4-apache

#Installs essential packages (unzip, libzip-dev) and 
#PHP extensions (pdo_mysql, opcache, zip) necessary 
#for the application to run, particularly for working with databases and optimizing PHP performance.
RUN apt-get update && apt-get install -yqq unzip libzip-dev \
    && docker-php-ext-install pdo_mysql opcache zip

# creates a configuration file in the PHP configuration directory to enable this feature.
RUN echo "instana.enable_auto_profile=1" > "/usr/local/etc/php/conf.d/zzz-instana-extras.ini"

# Copies a custom Apache status configuration file into the container.
COPY status.conf /etc/apache2/mods-available/status.conf

# Enables Apache modules mod_rewrite and mod_status
RUN a2enmod rewrite && a2enmod status

#working directory is set to /var/www/html
WORKDIR /var/www/html

#The html/ directory is copied into the container.
COPY html/ /var/www/html

#Installs composer and runs composer install to 
#install PHP dependencies as defined in the composer.json file.
COPY --from=composer /usr/bin/composer /usr/bin/composer
RUN composer install

# This is important. Symfony needs write permissions and we
# dont know the context in which the container will run, i.e.
# which user will be forced from the outside so better play
# safe for this simple demo.
RUN rm -Rf /var/www/var/*
RUN chown -R www-data /var/www
RUN chmod -R 777 /var/www

