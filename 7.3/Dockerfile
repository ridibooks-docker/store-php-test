FROM php:7.3-fpm-stretch

RUN apt-get update && apt-get install -y \
    software-properties-common \
    wget \
    nc


RUN wget http://packages.couchbase.com/releases/couchbase-release/couchbase-release-1.0-6-amd64.deb
RUN dpkg -i couchbase-release-1.0-6-amd64.deb

# https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=863199
RUN mkdir -p /usr/share/man/man1

RUN apt-get update && apt-get install -y \
    build-essential \
    libcouchbase-dev \
    libcouchbase2-bin \
    libcouchbase2-core \
    libcouchbase2-libevent \
    libmcrypt-dev \
    libpng-dev \
    libzip-dev \
    libgmp3-dev \
    openjdk-8-jre-headless \
    python3-pip \
    zlib1g-dev

RUN pecl install apcu-5.1.17
RUN pecl install couchbase-2.6.2
RUN pecl install ds-1.2.9
RUN pecl install mcrypt-1.0.3
RUN pecl install xdebug-2.9.6

# Extensions installed but not enabled by default, or installed by PECL needs to be enabled manually
RUN docker-php-ext-enable \
    apcu.so \
    couchbase.so \
    ds.so \
    mcrypt.so \
    opcache.so \
    xdebug.so


# sockets: required by inicis
# gd: required by phpoffice/phpspreadsheet
RUN docker-php-ext-install \
    bcmath \
    gd \
    gmp \
    pdo \
    pdo_mysql \
    sockets \
    zip

COPY --from=composer /usr/bin/composer /usr/bin/composer

RUN pip3 install awscli --upgrade
