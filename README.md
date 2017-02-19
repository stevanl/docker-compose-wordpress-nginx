# docker-compose-wordpress-nginx
Using docker compose to launch wordpress with nginx and php-fpm.

In the repository, there are two ways to build wordpress.

*docker-wordpress-1*: Using official images to run wordpress.

*docker-wordpress-3*: Separate php-fpm and wordpress, need to provide wordpress source files yourself.

## Installation

Clone the repository or download zip and decompression.

```bash
$ git clone https://github.com/stevanl/docker-compose-wordpress-nginx.git
```

## Usage

Before running, optionally modify profiles with your parameters.

e.g. official image version, ports, mysql password, wordpress version.

* If using *docker-wordpress-3*, download wordpress from the official website and decompress source files into the *wordpress* folder.

The `docker-compose.yml` file using the version 2 syntax, and version 2 files are supported by Compose 1.6.0+ and require a Docker Engine of version 1.10.0+.

Finally, execute the following command:

```bash
$ docker-compose up -d
```

Once started, if using *docker-wordpress-3*:

1. Create database for wordpress:

    ```bash
    $ docker exec -it <mysql_container_name> bash
    root@e50ef7ccca8f:/# mysql -u root -p
    Enter password: your_password
    mysql> CREATE DATABASE IF NOT EXISTS `wordpress`;
    mysql> exit;
    root@e50ef7ccca8f:/# exit
    ```

2. Change permissions of wordpress source files:

    ```bash
    $ docker exec -it <php_container_name> bash
    root@867b00000e95:/var/www/html# cd ..
    root@867b00000e95:/var/www# chown -R www-data:www-data html
    root@867b00000e95:/var/www# exit;
    ```
