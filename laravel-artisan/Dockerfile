FROM ubuntu:14.04
MAINTAINER Avni Rexhepi <arexhepi@gmail.com>


ENV DEBIAN_FRONTEND noninteractive
ENV TERM xterm
ENV PATH /usr/local/rvm/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin


RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8


RUN apt-get update && apt-get install -qy software-properties-common && \
    add-apt-repository -y ppa:ondrej/php5-5.6 && \
    apt-get update && apt-get autoremove -y && apt-get install -y --force-yes \
            php5-cli \
            php5-gd \
            php5-curl \
            php5-mcrypt \
            php5-mysqlnd \
            libsqlite3-dev \
            php5-sqlite \
            sqlite3 \
            --no-install-recommends && \
    apt-get remove -y --force-yes --purge software-properties-common && \
    apt-get -y autoremove && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


WORKDIR /var/www


ENTRYPOINT ["php", "artisan"]