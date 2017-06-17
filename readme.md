# Ancient PHP container for Kohana

These files provide a workable Docker context for the deprecated but still occasionally in use framework known as [Kohana](https://kohanaframework.org). It is inspired by the [realticaa/kohana-docker](https://hub.docker.com/r/realtica/kohana-docker) container.

The OS is Debian version 8 (jessie). It has some of the following features:

* PHP 5.4, the highest that supports Kohana.
* The extensions that show all green on the Kohana install page, namely [pecl_http-1.7.6](https://pecl.php.net/package/pecl_http/1.7.6), mysqli, [gd](http://php.net/manual/en/intro.image.php), and [mcrypt](http://php.net/manual/en/intro.mcrypt.php).
* [Composer](https://getcomposer.org)
* An updated SSL/TLS root certificate from the [ca-certificates](https://packages.debian.org/jessie/ca-certificates) package
* [Git](http://git-scm.com/) and [Vim](http://www.vim.org/) for managing files
* The MySQL client from [MariaDB](http://mariadb.org/)

## Server Name
If you'd like to run the site on a different hostname, create a `env_conf/environment.conf` file that defines the site name. It only needs
to have contents like the following:

    Define servername kohana-tutorial.dev

This would make the site available with domain name `kohana-tutorial.dev`

## Building and Running
Build the database and web server containers, then run it on forwarded ports. It is recommended to run the database on the same port on the host and container so that everything works the same in either environment:


    cd mariadb
    docker build -t enderandpeter/kohana-mariadb .
    cd ../php
    docker build -t enderandpeter/kohana .

    docker run -P -p 3311:3311 --name kohana-db -d enderandpeter/kohana-mariadb

### Windows

    docker run -p 8883:80 -v //c/Users/Spencer/Documents/kohana:/var/www/html --name kohana --link=kohana-db:kohana-db --add-host=kohana.local:127.0.0.1 -e KOHANA_ENV=DEVELOPMENT -e TERM=cygwin -d enderandpeter/kohana

### Linux or OS X

    docker run -p 8883:80 -v /home/Spencer/Documents/kohana:/var/www/html --name kohana --link=kohana-db:kohana-db --add-host=kohana.local:127.0.0.1 -e KOHANA_ENV=DEVELOPMENT -e TERM=cygwin -d enderandpeter/kohana
