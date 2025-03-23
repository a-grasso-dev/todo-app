FROM php:8.2-apache

# Installer les extensions PHP requises
RUN apt-get update && apt-get install -y \
    unzip zip git curl libzip-dev \
    && docker-php-ext-install pdo pdo_mysql

# Activer les modules Apache nécessaires
RUN a2enmod rewrite proxy proxy_http

# Copier le code Symfony
COPY . /var/www/html
WORKDIR /var/www/html

# Copier la conf Apache personnalisée
COPY docker/apache.conf /etc/apache2/sites-available/000-default.conf

# Fixer les droits
RUN chown -R www-data:www-data /var/www/html
