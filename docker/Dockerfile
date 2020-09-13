FROM php:7.4.10-apache

RUN apt-get update && apt-get install -y libicu-dev
RUN docker-php-ext-install intl

RUN apt-get install -y libzip-dev unzip
RUN docker-php-ext-install zip

RUN a2enmod rewrite

VOLUME /var/www/html/var
VOLUME /var/www/html/vendor

RUN chown -R www-data:www-data /var/www/html/var
RUN chown -R www-data:www-data /var/www/html/vendor

WORKDIR /opt

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && ln -s /opt/composer.phar /usr/bin/composer

WORKDIR /var/www/html
#RUN composer install

COPY php.ini /usr/local/etc/php/php.ini
COPY vhost.conf /etc/apache2/sites-enabled/010-symfony-01.conf
