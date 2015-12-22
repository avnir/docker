# My personal tools docker container

A few examples how to run these containers
- ```docker run --rm -v $PWD:/var/www --name phpunit avnir/tools phpunit```
- ```docker run --rm -v $PWD:/var/www --name grunt avnir/tools grunt```
- ```docker run --rm -v $PWD:/var/www --name gulp avnir/tools gulp```