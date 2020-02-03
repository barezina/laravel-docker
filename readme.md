## laravel-docker

I needed a simple way to bring up the following stack for laravel without
worrying about excess detail.

#### What does this do?
It brings up:
* A container to hold nginx for a static frontend.
* A container to hold nginx for serving up php.
* A container for php.
* A container for mysql.

#### How to use:
* Go get yourself a ubuntu 18.04 machine.
* Install docker: https://docs.docker.com/v17.09/engine/installation/linux/docker-ce/ubuntu/
* Install docker-compose: https://docs.docker.com/compose/install/
* Clone this repo to a folder: `git clone https://github.com/barezina/laravel-docker.git`
* Open a terminal and type `echo $UID`. 
* If the output is not 1000, open app-php and place your user ID into this file.
* Run docker-compose up --build -d

This should build the four containers listed above.

#### How to initialise laravel:
* Open up a terminal
* Type `docker ps` to get a list of running services - you should see a table that looks like this:
```$xslt
CONTAINER ID        IMAGE                      CREATED             PORTS                                
20bba3fa4ecc        laravel-docker_nginx-api   24 minutes ago      0.0.0.0:43080->80/tcp                
6bc041aea9d7        laravel-docker_php         24 minutes ago      9000/tcp                             
1f8626f089d2        laravel-docker_frontend    24 minutes ago      0.0.0.0:43081->80/tcp                
85bbe5811df8        mysql:8                    24 minutes ago      33060/tcp, 0.0.0.0:43006->3306/tcp   
```
* Find the `laravel-docker_php` container in the list and note it's container ID.
* Type the following `docker exec -it 6bc bash` where `6bc` is replaced with the first three characters your php container.
* You should now be logged into the PHP container
```$xslt
www@6bc041aea9d7:/var/www/html$ _
```
* `cp .example.env .env`
* `php artisan key:generate`
* `php artisan migrate`

#### Ports:

* API backend can be accessed on localhost:43080
* Static frontend can be accessed on localhost:43081
* Mysql can be accessed on localhost:43006 (username: root / password: secret)

Happy coding.