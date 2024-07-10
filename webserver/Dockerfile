ARG PHP_VERSION=""
FROM php:${PHP_VERSION:+${PHP_VERSION}-}apache

RUN apt-get -y update --fix-missing
RUN apt-get upgrade -y

# Install useful tools
RUN apt-get -y install apt-utils nano wget dialog

# Install important libraries
RUN apt-get -y install --fix-missing apt-utils build-essential git curl libcurl4 zip

# Install PDO MySQL
RUN docker-php-ext-install pdo pdo_mysql

# Install Composer
RUN curl --silent --show-error https://getcomposer.org/installer | php

# Use the default configuration
RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

RUN a2enmod rewrite
RUN a2enmod ssl
RUN service apache2 restart

COPY dev.conf /etc/apache2/sites-enabled/dev.conf
RUN mkdir /etc/apache2/ssl
COPY localhost.crt /etc/apache2/ssl/server.crt
COPY localhost_no-pw.key /etc/apache2/ssl/server.key

# RUN echo "Include /usr/local/apache2/conf/demo.apache.conf" \
#     >> /usr/local/apache2/conf/httpd.conf

EXPOSE 80
EXPOSE 443