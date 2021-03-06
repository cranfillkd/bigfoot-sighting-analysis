FROM php:7.3-apache-stretch

RUN apt-get -y update --fix-missing
RUN apt-get upgrade -y

# Change Root Directory
ENV APACHE_DOCUMENT_ROOT=/var/www/html/bigfoot-sighting-analysis
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf


# Install useful tools
RUN apt-get -y install apt-utils nano wget dialog
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash  &&  apt-get install -y nodejs

# Install important libraries
RUN apt-get -y install --fix-missing apt-utils build-essential git curl libcurl3 libcurl3-dev zip openssl

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install xdebug
RUN pecl install xdebug-2.7.2
RUN docker-php-ext-enable xdebug

# Install redis
#RUN pecl install redis-4.0.1
#RUN docker-php-ext-enable redis

# Other PHP7 Extensions

RUN apt-get -y install libsqlite3-dev libsqlite3-0 mysql-client
# RUN docker-php-ext-install pdo_mysql 
# RUN docker-php-ext-install pdo_sqlite
RUN docker-php-ext-install mysqli

RUN docker-php-ext-install curl
# RUN docker-php-ext-install tokenizer
RUN docker-php-ext-install json

# Compression
# RUN apt-get -y install zlib1g-dev libzip-dev
# RUN docker-php-ext-install zip

# Unicode
# RUN apt-get -y install libicu-dev
# RUN docker-php-ext-install -j$(nproc) intl

# PHP Text Manulipation
# RUN docker-php-ext-install mbstring
# RUN docker-php-ext-install gettext

# PHP Sprites
RUN apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ 
RUN docker-php-ext-install -j$(nproc) gd

# Enable apache modules
RUN a2enmod rewrite headers

WORKDIR /var/www/html

RUN git clone https://github.com/kita85/bigfoot-sighting-analysis.git

WORKDIR /var/www/html/bigfoot-sighting-analysis

RUN npm install
