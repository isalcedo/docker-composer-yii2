FROM php:apache
MAINTAINER Ignacio Salcedo <ignacio@isalcedo.com> (@pawrubble)

# Enable Apache Rewrite Module
RUN a2enmod rewrite

RUN service apache2 restart

# Install PHP extensions
RUN apt-get update && apt-get install -y libfreetype6-dev libpng12-dev libjpeg-dev zip unzip libicu-dev libicu52 libicu52-dbg && rm -rf /var/lib/apt/lists/* \
	&& docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr --with-freetype-dir=/usr \
	&& docker-php-ext-install gd
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install intl
RUN docker-php-ext-install pdo pdo_mysql

# Copy init scripts and custom .htaccess
COPY php.ini /usr/local/etc/php

RUN service apache2 restart

EXPOSE 80
CMD ["apache2-foreground"]
