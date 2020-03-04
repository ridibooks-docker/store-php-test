FROM php:7.1

RUN apt-get update && apt-get install -yqq \
    git \
    libmcrypt-dev \
    libpng-dev \
    python3 \
    python3-pip \
    unzip \
    zlib1g-dev \ 
    wget

RUN wget https://raw.githubusercontent.com/composer/getcomposer.org/da7be05fa1c9f68b9609726451d1aaac7dd832cb/web/installer -O - -q | php -- --install-dir=/usr/bin/
RUN mv /usr/bin/composer.phar /usr/bin/composer

RUN docker-php-ext-install bcmath gd pdo_mysql mcrypt zip
RUN pecl install apcu xdebug ds couchbase && docker-php-ext-enable apcu xdebug ds couchbase
COPY apcu.ini /usr/local/etc/php/conf.d/docker-php-ext-apcu.ini
RUN pip3 install awscli --upgrade
