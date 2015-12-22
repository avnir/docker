# Laravel artisan docker container

This is a [Docker](http://www.docker.com) image for [Laravel PHP framework](http://www.laravel.com) using [Nginx](http://nginx.org).

This image works well with the below related images.
- [avnir/laravel-artisan]
- [avnir/composer]
- [avnir/phpfpm]
- [avnir/nginx]

A few examples how to run these containers
- ```docker run -d -v ${PWD}:/var/www:rw --name phpfpm avnir/phpfpm```
- ```docker run -d --name nginx --volumes-from=phpfpm --link phpfpm:fpm avnir/nginx```
- ```docker run --volumes-from phpfpm --rm avnir/composer install --prefer-source```
- ```docker run --volumes-from phpfpm --rm avnir/laravel-artisan route:list```

Feedback or improvements are welcome.