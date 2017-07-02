FROM php:5.4-apache
MAINTAINER Spencer Williams <spencer@aninternetpresence.net>

RUN a2enmod rewrite && apt-get update && apt-get install --yes \ 
  ca-certificates git vim mariadb-client libpng12-dev libmcrypt-dev libmagic-dev libcurl4-openssl-dev && \
  docker-php-ext-install mysql mysqli pdo_mysql gd mcrypt mbstring && \
  yes | pecl install pecl_http-1.7.6 && \
  echo 'extension=http.so' >> /usr/local/etc/php/conf.d/pecl_http.ini
  
COPY env_conf/* 000-kohana.conf /etc/apache2/sites-available/

RUN a2ensite 000-kohana

# Install composer
RUN php -r "copy('https://getcomposer.org/installer', '/tmp/composer-setup.php');" && \
	php -r "if (hash_file('SHA384', '/tmp/composer-setup.php') === '669656bab3166a7aff8a7506b8cb2d1c292f042046c5a994c43155c0be6190fa0355160742ab2e1c88d40d5be660b410') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('/tmp/composer-setup.php'); } echo PHP_EOL;" && \
php /tmp/composer-setup.php --install-dir=/usr/bin --filename=composer && \
php -r "unlink('/tmp/composer-setup.php');"