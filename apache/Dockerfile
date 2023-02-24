FROM php:8.0-apache

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN set -ex \
        && docker-php-ext-install pdo pdo_mysql mysqli

RUN apt-get update \
    # Library for reading, creating, and modifying zip archives
    && apt-get install -y libzip-dev \
    # Adding additional features to the previous package
    && apt-get install -y zlib1g-dev \
    # The directory which is used for storing information for each package resource specified in your system's sources
    && rm -rf /var/lib/apt/lists/* \
    # Another library for reading, creating, and modifying zip archives
    && docker-php-ext-install zip

#Adding the SSL files
COPY ../ssl.crt /etc/apache2/ssl/ssl.crt
COPY ../ssl.key /etc/apache2/ssl/ssl.key
RUN mkdir -p /var/run/apache2/ # The -p option if for creating the parent directories if needed.

#Enabling SSL for apache.
RUN ln -s /etc/apache2/mods-available/ssl.load  /etc/apache2/mods-enabled/ssl.load
# creating a symlink for the rewrite.load module
# This is needed to use the .htaccess file
RUN ln -s /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled/rewrite.load
RUN ln -s /etc/apache2/mods-available/headers.load /etc/apache2/mods-enabled/headers.load