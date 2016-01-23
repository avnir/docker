FROM phusion/baseimage:0.9.18
MAINTAINER Avni Rexhepi <arexhepi@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
ENV PATH /usr/local/rvm/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

RUN \
#usermod -u 99 nobody && \
#usermod -g 1000 nobody && \
    apt-get update && apt-get install -qy \
            software-properties-common && \
    add-apt-repository -y ppa:ondrej/php5-5.6 && \
    apt-get update && apt-get install -qy --force-yes \
            php5-cli \
            php5-gd \
            php5-curl \
            php5-mcrypt \
            php5-mysqlnd \
            libsqlite3-dev \
            php5-sqlite \
            sqlite3 \
            --no-install-recommends && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /var/www

ENTRYPOINT ["php", "artisan"]