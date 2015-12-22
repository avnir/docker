FROM avnir/laravel-artisan:latest
MAINTAINER Avni Rexhepi <arexhepi@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
ENV PATH /usr/local/rvm/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

RUN apt-get update && apt-get install -y --force-yes \
            git \
            php5-readline \
            --no-install-recommends && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN php -r "readfile('https://getcomposer.org/installer');" | php && \
    mv composer.phar /usr/local/bin/composer && \
    composer self-update

RUN usermod -u 1000 www-data

RUN echo "export PATH=~/.composer/vendor/bin/:$PATH" && \ 
    echo "export COMPOSER_HOME=/var/www/"

# We need to create an empty file, otherwise the volume will belong to root.
# This is probably a Docker bug.
RUN touch /var/www/placeholder && chown -R www-data:www-data /var/www

ENTRYPOINT ["composer"]
# CMD ["--help"]