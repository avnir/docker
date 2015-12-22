FROM avnir/composer:latest
MAINTAINER Avni Rexhepi <arexhepi@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
ENV PATH /usr/local/rvm/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

RUN apt-get update && apt-get install -y --force-yes \
            mysql-client-5.6 nodejs npm \
            --no-install-recommends && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN ln -s `which nodejs` /usr/bin/node

RUN npm install -g gulp && \
    npm install -g bower && \
    npm install -g grunt-cli

RUN echo "{ \"allow_root\":  true, \"interactive\": false }" >> /.bowerrc
RUN composer global require "phpunit/phpunit=4.8.*" && \
    echo "export PATH=~/.composer/vendor/bin/:$PATH" >> ~/.bashrc && \
    ln -s ~/.composer/vendor/bin/phpunit /usr/local/bin/phpunit

RUN rm -Rf /var/www/*

ENTRYPOINT ["/bin/sh", "-c"]
CMD ["phpunit"]