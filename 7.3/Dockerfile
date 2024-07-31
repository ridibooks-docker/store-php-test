FROM php:7.3-fpm-bullseye

RUN apt-get update && apt-get install -y \
    software-properties-common \
    wget \
    netcat

# https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=863199
RUN mkdir -p /usr/share/man/man1

RUN apt-get update && apt-get install -y \
    python3-pip \
    build-essential \
    libmcrypt-dev \
    libpng-dev \
    libzip-dev \
    libgmp3-dev \
    zlib1g-dev \
    cmake \
    libevent-dev \
    libev-dev \
    libuv1-dev \
    libssl-dev

# librdkafka Installation
RUN wget https://github.com/edenhill/librdkafka/archive/refs/tags/v1.9.2.tar.gz
RUN tar xvfz v1.9.2.tar.gz -C /

WORKDIR /librdkafka-1.9.2
RUN ./configure --install-deps
RUN make && make install

# Datadog tracer Installation
ADD https://github.com/DataDog/dd-trace-php/releases/download/0.97.0/datadog-php-tracer_0.97.0_amd64.deb .
RUN dpkg -i datadog-php-tracer_0.97.0_amd64.deb

RUN pecl install apcu-5.1.17
RUN pecl install ds-1.2.9
RUN pecl install mailparse-3.1.1
RUN pecl install mcrypt-1.0.3
RUN pecl install rdkafka-6.0.3

# Extensions installed but not enabled by default, or installed by PECL needs to be enabled manually
RUN docker-php-ext-enable \
    apcu.so \
    ds.so \
    mailparse.so \
    mcrypt.so \
    opcache.so \
    rdkafka.so


# sockets: required by inicis
# gd: required by phpoffice/phpspreadsheet
RUN docker-php-ext-install \
    bcmath \
    gd \
    gmp \
    pcntl \
    pdo \
    pdo_mysql \
    sockets \
    zip

# composer
COPY --from=composer /usr/bin/composer /usr/bin/composer

COPY apcu.ini /usr/local/etc/php/conf.d/docker-php-ext-apcu.ini
RUN pip3 install awscli --upgrade
