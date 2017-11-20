FROM mvbortolotti/docker-library-php:php54

RUN curl https://xdebug.org/files/xdebug-2.4.0.tgz -o xdebug-2.4.0.tgz \
	&& tar xvf xdebug-2.4.0.tgz \
	&& cd xdebug-2.4.0 \
	&& /usr/local/bin/phpize \
	&& ./configure --enable-xdebug \
	&& make \
	&& make install \
	&& echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "xdebug.remote_port=9000" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "xdebug.remote_host=dbhost" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "xdebug.max_nesting_level=300" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

RUN apt-get update && apt-get install -y \
	libmcrypt-dev \
	zlib1g-dev \
	libmagickwand-dev \
	libmagickcore-dev \
	vim \
	locales

RUN sed -i -e 's/# pt_BR.UTF-8 UTF-8/pt_BR.UTF-8 UTF-8/' /etc/locale.gen \
	&& sed -i -e 's/# pt_BR ISO-8859-1/pt_BR ISO-8859-1/' /etc/locale.gen \
	&& locale-gen \
	&& locale -a

ENV LANGUAGE=pt_BR.UTF-8
ENV LANG=pt_BR.UTF-8
ENV LC_ALL=pt_BR.UTF-8

RUN dpkg-reconfigure --frontend=noninteractive locales \
	&& update-locale LANG=pt_BR.UTF-8


RUN docker-php-ext-install pdo pdo_mysql mysql mcrypt zip \
	&& pecl install imagick \
	&& docker-php-ext-enable imagick

RUN a2enmod rewrite
RUN a2enmod headers