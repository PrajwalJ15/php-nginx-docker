# Docker PHP-FPM 8.3 & Nginx 1.26 on Alpine Linux
Example PHP-FPM 8.3 & Nginx 1.26 container image for Docker, built on [Alpine Linux](https://www.alpinelinux.org/).

Repository: https://hub.docker.com/r/wodby/php-nginx


* Built on the lightweight and secure Alpine Linux distribution
* Multi-platform, supporting AMD4, ARMv6, ARMv7, ARM64
* Very small Docker image size (+/-40MB)
* Uses PHP 8.3 for the best performance, low CPU usage & memory footprint
* Optimized for 100 concurrent users
* Optimized to only use resources when there's traffic (by using PHP-FPM's `on-demand` process manager)
* The services Nginx, PHP-FPM and supervisord run under a non-privileged user (nobody) to make it more secure
* The logs of all the services are redirected to the output of the Docker container (visible with `docker logs -f <container name>`)
* Follows the KISS principle (Keep It Simple, Stupid) to make it easy to understand and adjust the image to your needs

[![Docker Pulls](https://hub.docker.com/r/wodby/php-nginx)
![nginx 1.26](https://img.shields.io/badge/nginx-1.26-brightgreen.svg)
![php 8.3](https://img.shields.io/badge/php-8.3-brightgreen.svg)
![License MIT](https://img.shields.io/badge/license-MIT-blue.svg)


## Goal of this project
The goal of this container image is to provide an example for running Nginx and PHP-FPM in a container which follows
the best practices and is easy to understand and modify to your needs.

## Usage

Start the Docker container:

    docker run -p 80:8080 wodby/php-nginx

See the PHP info on http://localhost, or the static html page on http://localhost/test.html

Or mount your own code to be served by PHP-FPM & Nginx

    docker run -p 80:8080 -v ~/my-codebase:/var/www/html wodby/php-nginx

Nginx configuration:

    docker run -v "`pwd`/nginx-server.conf:/etc/nginx/conf.d/server.conf" wodby/php-nginx

PHP configuration:

    docker run -v "`pwd`/php-setting.ini:/etc/php83/conf.d/settings.ini" wodby/php-nginx

PHP-FPM configuration:

    docker run -v "`pwd`/php-fpm-settings.conf:/etc/php83/php-fpm.d/server.conf" wodby/php-nginx

_Note; Because `-v` requires an absolute path I've added `pwd` in the example to return the absolute path to the current directory_
