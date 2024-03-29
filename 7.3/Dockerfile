FROM php:7.3-fpm-stretch

RUN apt-get update && apt-get install -y \
    software-properties-common \
    wget \
    netcat

RUN wget http://packages.couchbase.com/releases/couchbase-release/couchbase-release-1.0-6-amd64.deb
RUN dpkg -i couchbase-release-1.0-6-amd64.deb

RUN wget https://github.com/edenhill/librdkafka/archive/refs/tags/v1.6.1.tar.gz
RUN tar xvfz v1.6.1.tar.gz -C /

WORKDIR /librdkafka-1.6.1
RUN ./configure --install-deps
RUN make && make install

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
RUN pecl install rdkafka-5.0.0

# Extensions installed but not enabled by default, or installed by PECL needs to be enabled manually
RUN docker-php-ext-enable \
    apcu.so \
    couchbase.so \
    ds.so \
    mcrypt.so \
    opcache.so \
    rdkafka.so


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
COPY apcu.ini /usr/local/etc/php/conf.d/docker-php-ext-apcu.ini
RUN pip3 install awscli --upgrade
