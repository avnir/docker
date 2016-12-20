# php5-fpm docker container

This is a [Docker](http://www.docker.com) image using [PHP-FPM](http://php-fpm.org/).


A few examples how to run this container
- ```docker run -d phpfpm -v $PWD:/var/www/ avnir/php5-fpm -p 9000:9000```
- ```docker run -d --name phpfpm -v $PWD:/var/www/ avnir/php5-fpm -p 9000:9000```
- ```docker run --rm -ti -v $PWD:/var/www/ avnir/php5-fpm -p 9000:9000```


Feedback or improvements are welcome.