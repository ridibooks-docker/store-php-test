FROM ridibooks/php:7.0

RUN apt-get update && apt-get install libmcrypt-dev zlib1g-dev php-phpdbg python3 python3-pip gnupg -yqq

RUN curl -O http://packages.couchbase.com/ubuntu/couchbase.key && \
    apt-key add couchbase.key
RUN echo "deb http://packages.couchbase.com/ubuntu buster buster/main" | tee /etc/apt/sources.list.d/couchbase.list

RUN apt-get update && apt-get install -yqq \
    libcouchbase-dev

RUN docker-php-ext-install bcmath pdo_mysql mcrypt zip
RUN pecl install apcu xdebug ds couchbase && docker-php-ext-enable apcu.so ds.so couchbase.so
RUN pip3 install awscli --upgrade