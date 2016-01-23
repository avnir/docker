# Laravel artisan docker container

This is a [Docker](http://www.docker.com) image for [Laravel PHP framework](http://www.laravel.com) using [Nginx](http://nginx.org).

This image works well with the below related images.
- [avnir/laravel-artisan]
- [avnir/composer]
- [avnir/php5-fpm]
- [avnir/nginx]

A few examples how to run these containers
- ```docker run -d -v ${PWD}:/var/www:rw avnir/larave-artisan```
- ```docker run -d --volumes-from=container --link fpm-container:fpm avnir/nginx```
- ```docker run --volumes-from container --rm avnir/composer install --prefer-source```
- ```docker run --volumes-from container --rm avnir/laravel-artisan route:list```

Feedback and improvements are welcome.