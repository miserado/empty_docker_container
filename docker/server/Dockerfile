FROM php:7.4-apache

RUN a2enmod rewrite

RUN apt-get update && apt-get install -y git unzip zip

WORKDIR /var/www/html

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/
RUN install-php-extensions gd pdo_mysql mysqli bcmath zip bz2 intl opcache imagick

RUN curl -sS https://getcomposer.org/installer -o composer-setup.php
RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN rm composer-setup.php

ARG GIT_USER
ARG GIT_EMAIL

RUN git config --global user.name ${GIT_USER}
RUN git config --global user.email ${GIT_EMAIL}

RUN chown -R $USER:www-data /var/www/html
RUN chmod -R 775 /var/www/html