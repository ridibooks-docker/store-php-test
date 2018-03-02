FROM ridibooks/php:7.1
LABEL maintainer="Heechan Yang <heechan@ridi.com>"

RUN apt-get update && apt-get install libmcrypt-dev zlib1g-dev php-phpdbg python3 python3-pip -yqq
RUN docker-php-ext-install bcmath pdo_mysql mcrypt zip
RUN pecl install apcu xdebug && docker-php-ext-enable apcu xdebug
RUN pip3 install awscli --upgrade