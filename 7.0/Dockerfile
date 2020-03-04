FROM ridibooks/php:7.0

RUN apt-get update && apt-get install libmcrypt-dev zlib1g-dev php-phpdbg python3 python3-pip -yqq
RUN docker-php-ext-install bcmath pdo_mysql mcrypt zip
RUN pecl install apcu xdebug ds couchbase && docker-php-ext-enable apcu xdebug ds couchbase
RUN pip3 install awscli --upgrade