FROM php:7-apache

RUN apt-get update && \
 apt-get install -y libpng-dev

RUN apt-get update && \
    apt-get install -y \
        zlib1g-dev libzip-dev

RUN docker-php-ext-install zip
RUN docker-php-ext-install gd
RUN docker-php-ext-install mysqli pdo pdo_mysql

RUN  ln -s /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled/

RUN  a2enmod rewrite

ENV APACHE_DOCUMENT_ROOT /var/www/html/public

# seta o document root configurado anteriormente nas variáveis de ambiente
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

RUN service apache2 restart