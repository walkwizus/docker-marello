FROM php:8.1.3RC1-fpm-buster
MAINTAINER Jimmy Carricart <jimmy@walkwizus.fr>

ARG APP_ID=1000

RUN apt-get update && apt-get install -y \
	cron \
	default-mysql-client \
    git \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libxml2-dev \
    libxslt1-dev \
    libicu-dev \
    xmlstarlet \
    libcurl4-openssl-dev \
    pkg-config \
    libssl-dev \
    libonig-dev \
    libzip-dev \
    zip \
    libldap2-dev \
    unzip \
    gnupg2 \
    curl \
    software-properties-common \
    msmtp \
    mailutils

RUN docker-php-ext-configure gd --with-freetype --with-jpeg

RUN pecl channel-update pecl.php.net \
  	&& pecl install xdebug \
  	&& docker-php-ext-enable xdebug

RUN apt-get install -y libmagickwand-dev \
  	&& pecl install imagick  \
  	&& docker-php-ext-enable imagick

RUN docker-php-ext-install -j$(nproc) \
	bcmath \
	gd \
    iconv \
    mbstring \
    pcntl \
    soap \
    xsl \
    zip \
    intl \
    pdo \
    pdo_mysql \
    sysvsem \
    ldap \
    sockets

RUN pecl install redis && docker-php-ext-enable redis

RUN groupadd -g "$APP_ID" app && useradd -g "$APP_ID" -u "$APP_ID" -d /var/www -s /bin/bash app

RUN curl -sL https://deb.nodesource.com/setup_14.x | bash - && apt-get update && apt-get install -y nodejs

RUN php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer --version=1.10.22
RUN composer global require hirak/prestissimo

COPY conf/msmtprc /etc/msmtprc
COPY conf/www.conf /usr/local/etc/php-fpm.d/
COPY conf/php.ini /usr/local/etc/php/
COPY conf/php-fpm.conf /usr/local/etc/

RUN mkdir -p /etc/nginx/html /var/www/html /sock \
	&& chown -R app:app /etc/nginx /var/www /usr/local/etc/php/conf.d /sock

USER app:app

VOLUME /var/www

WORKDIR /var/www/html