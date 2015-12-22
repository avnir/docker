FROM avnir/laravel-artisan:latest
MAINTAINER Avni Rexhepi <arexhepi@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
ENV PATH /usr/local/rvm/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN apt-get update && apt-get install -y \
            software-properties-common && \
    add-apt-repository -y ppa:ondrej/php5-5.6 && \
    apt-get update && apt-get install -y --force-yes \
            php5-fpm \
            php5-imap \
            php5-json \
            --no-install-recommends && \
    apt-get remove -y --force-yes --purge software-properties-common && \
    apt-get -y autoremove && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# error_reporting and display_errors should be enabled on development only
RUN sed -i \
        -e "s~^display_errors.*$~display_errors = Off~g" \
        -e "s~^ignore_repeated_errors.*$~ignore_repeated_errors = On~g" \
        -e "s~^ignore_repeated_source.*$~ignore_repeated_source = On~g" \
        -e "s~^display_startup_errors.*$~display_startup_errors = Off~g" \
        -e "s~^track_errors.*$~track_errors = Off~g" \
        -e "s~^;date.timezone.*$~date.timezone = UTC~g" \
        -e "s~^;cgi.fix_pathinfo.*$~cgi.fix_pathinfo=0~g" \
            /etc/php5/fpm/php.ini

RUN sed -i \
        -e "s~^;daemonize = yes*$~daemonize = no~g" \
        -e "s~^;emergency_restart_threshold.*$~emergency_restart_threshold = 10~g" \
        -e "s~^;emergency_restart_interval.*$~emergency_restart_interval = 1m~g" \
        -e "s~^;process_control_timeout.*$~process_control_timeout = 10s~g" \
            /etc/php5/fpm/php-fpm.conf

RUN sed -i \
        -e "s/^pm.max_children\(.*\)/pm.max_children = 100/g" \
        -e "s/^pm.start_servers\(.*\)/pm.start_servers = 10/g" \
        -e "s/^pm.min_spare_servers\(.*\)/pm.min_spare_servers = 5/g" \
        -e "s/^pm.max_spare_servers\(.*\)/pm.max_spare_servers = 15/g" \
        -e "s/^;pm.max_requests\(.*\)/pm.max_requests = 1000/g" \
        -e "s/^pm.max_requests\(.*\)/pm.max_requests = 1000/g" \
        -e "s/^listen\(.*\)/listen = 0.0.0.0:9000/g" \
        -e "s/^;slowlog/slowlog/g" \
        -e "s/^slowlog\(.*\)/slowlog = \/var\/log\/slowlog.log/g" \
        -e "s/^;request_slowlog_timeout/request_slowlog_timeout/g" \
        -e "s/^;pm.status_path/pm.status_path/g" \
        -e "s/^;request_terminate_timeout/request_terminate_timeout/g" \
        -e "s/^;catch_workers_output/catch_workers_output/g" \
            /etc/php5/fpm/pool.d/www.conf

RUN echo "\n\nopcache.memory_consumption=128" >> /etc/php5/mods-available/opcache.ini && \
    echo "opcache.interned_strings_buffer=8" >> /etc/php5/mods-available/opcache.ini && \
    echo "opcache.max_accelerated_files=4000" >> /etc/php5/mods-available/opcache.ini && \
    echo "opcache.revalidate_freq=60" >> /etc/php5/mods-available/opcache.ini && \
    echo "opcache.fast_shutdown=1" >> /etc/php5/mods-available/opcache.ini && \
    echo "opcache.enable_file_override=1" >> /etc/php5/mods-available/opcache.ini && \
    echo "opcache.save_comments=0" >> /etc/php5/mods-available/opcache.ini

RUN usermod -u 1000 www-data

# We need to create an empty file, otherwise the volume will belong to root.
# This is probably a Docker bug.
RUN mkdir -p /var/www/ && touch /var/www/placeholder
RUN chown -R www-data:www-data /var/www

VOLUME /var/www
WORKDIR /var/www


EXPOSE 9000

ENTRYPOINT ["/usr/sbin/php5-fpm", "-FO"]