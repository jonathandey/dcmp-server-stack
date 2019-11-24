# DCMP Stack

A Docker, Caddy (v1), Mariadb & PHP-FPM starting template for your PHP projects

## Getting started

1. `cp docker/db/.env.example docker/db/.env`
2. Optionally add an initial SQL file to the `docker/db/docker-entrypoint-initdb.d` directory
3. Run `docker-compose up app web db`
4. Visit 127.0.0.1:8080 in your web browser

## Configuring the Caddy server

All Caddy server configuration is in the file `docker/caddy/Caddyfile`
See the [Caddy V1 documentation](https://caddyserver.com/v1/docs) for further configuration options

## Configuring the database

The default database credentials are copied from the file `docker/db/.env.example` during the first step of Getting Started.
You can change the values to suit your project. More information about these values can be found at the [Mariadb docker hub page](https://hub.docker.com/_/mariadb)

```
MYSQL_DATABASE=app
MYSQL_USER=user
MYSQL_PASSWORD=password
MYSQL_RANDOM_ROOT_PASSWORD=true
```

## Running your code

This base template should get you running with most PHP applications. The PHP extensions: gd, iconv & pdo (mysql) are installed from the start, should you need to you can configure more extensions in the file `docker/php/Dockerfile`.

Now just add your code to the `src` folder.

## Running a Laravel app

Before Getting Started, run the command `docker-compose run composer composer create-project --prefer-dist laravel/laravel .` to install the latest version of Laravel.

Then update the file `docker/caddy/Caddyfile` to point the root to the public directory

```
0.0.0.0

root /var/www/html/public

fastcgi / app:9000 php {
	root /var/www/html/public
}

rewrite {
    regexp .*
    ext /
    to /index.php?{query}
}

gzip

tls off
```

Don't forget to update your applications `src/.env` file to match the database configuration values you set in `docker/db/.env`.