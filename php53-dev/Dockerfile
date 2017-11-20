FROM ubuntu:12.04
MAINTAINER Alexander Schenkel <alex@alexi.ch>

RUN apt-get update && \
    apt-get install -y \
      apache2 \
      php5 \
      php5-cli \
      libapache2-mod-php5 \
      php5-gd \
      php5-ldap \
      php5-mysql \
      php5-pgsql \
      php5-dev \
      vim \
      curl \
      php5-xdebug \
      php5-curl \
      mysql-client \
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

RUN set -e && \
    PHP_ERROR_REPORTING=${PHP_ERROR_REPORTING:-"E_ALL & ~E_DEPRECATED & ~E_NOTICE"} && \
    sed -ri 's/^display_errors\s*=\s*Off/display_errors = On/g' /etc/php5/apache2/php.ini && \
    sed -ri 's/^display_errors\s*=\s*Off/display_errors = On/g' /etc/php5/cli/php.ini && \
    sed -ri "s/^error_reporting\s*=.*$//g" /etc/php5/apache2/php.ini && \
    sed -ri "s/^error_reporting\s*=.*$//g" /etc/php5/cli/php.ini && \
    sed -ri 's/AllowOverride\sNone/AllowOverride All/g' /etc/apache2/sites-enabled/000-default && \
    echo "error_reporting = $PHP_ERROR_REPORTING" >> /etc/php5/apache2/php.ini && \
    echo "error_reporting = $PHP_ERROR_REPORTING" >> /etc/php5/cli/php.ini && \
    echo "xdebug.remote_port=9000" >> /etc/php5/conf.d/xdebug.ini && \
    echo "xdebug.remote_host=dbhost" >> /etc/php5/conf.d/xdebug.ini && \
    echo "xdebug.remote_enable=1" >> /etc/php5/conf.d/xdebug.ini && \
    echo "xdebug.max_nesting_level=300" >> /etc/php5/conf.d/xdebug.ini

RUN a2enmod rewrite
RUN a2enmod headers
RUN service apache2 restart

VOLUME ["/var/www"]

EXPOSE 80

CMD /usr/sbin/apache2ctl -D FOREGROUND
