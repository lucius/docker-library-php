FROM php:7.0-dev

RUN apt-get update && apt-get install -y \
	libmcrypt-dev \
	&& docker-php-ext-install pdo pdo_mysql mcrypt \
	&& pecl install xdebug-2.5.0 \
	&& echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "xdebug.remote_port=9000" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "xdebug.remote_host=dbhost" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "xdebug.max_nesting_level=300" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& docker-php-ext-enable pdo pdo_mysql mcrypt xdebug

RUN a2enmod rewrite