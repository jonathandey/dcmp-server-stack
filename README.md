# DCMP

A Docker, Caddy (v1), Mariadb & PHP-FPM starting template for your PHP projects

## Getting started

1. `cp docker/db/.env.example docker/db/.env`
2. Optionally add an initial SQL file to the `docker/db/docker-entrypoint-initdb.d`
3. Run `docker-compose up app web db`
4. Visit 127.0.0.1:8080 in your web browser


