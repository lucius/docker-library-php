FROM php:7.0-apache

RUN apt-get update && apt-get install -y \
	libmcrypt-dev \
	zlib1g-dev \
	vim \
	libmagickwand-dev \
	libmagickcore-dev \
	&& docker-php-ext-install pdo pdo_mysql mysql mcrypt zip \
	&& pecl install xdebug-2.5.0 \
	&& echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "xdebug.remote_port=9000" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "xdebug.remote_host=dbhost" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "xdebug.max_nesting_level=300" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& docker-php-ext-enable pdo pdo_mysql mysql mcrypt xdebug zip \
	&& pecl install imagick \
	&& docker-php-ext-enable imagick

RUN a2enmod rewrite
RUN a2enmod headers