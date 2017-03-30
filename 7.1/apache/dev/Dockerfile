FROM mvbortolotti/apache-php:php71

RUN apt-get update && apt-get install -y \
	libmcrypt-dev \
	&& docker-php-ext-install pdo pdo_mysql mcrypt \
	&& pecl install xdebug-2.5.0 \
	&& docker-php-ext-enable pdo pdo_mysql mcrypt xdebug

RUN a2enmod rewrite