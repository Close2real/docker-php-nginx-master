# Docker PHP-FPM 8.1 & Nginx 1.24 on Alpine Linux
Example PHP-FPM 8.1 & Nginx 1.24 container image for Docker, built on [Alpine Linux](https://www.alpinelinux.org/).

* Built on the lightweight and secure Alpine Linux distribution
* Multi-platform, supporting AMD4, ARMv6, ARMv7, ARM64
* Very small Docker image size (+/-40MB)
* Uses PHP 8.3 for the best performance, low CPU usage & memory footprint
* Optimized for 100 concurrent users
* Optimized to only use resources when there's traffic (by using PHP-FPM's `on-demand` process manager)
* The services Nginx, PHP-FPM and supervisord run under a non-privileged user (nobody) to make it more secure
* The logs of all the services are redirected to the output of the Docker container (visible with `docker logs -f <container name>`)
* Follows the KISS principle (Keep It Simple, Stupid) to make it easy to understand and adjust the image to your needs

![nginx 1.24](https://img.shields.io/badge/nginx-1.24-brightgreen.svg)
![php 8.3](https://img.shields.io/badge/php-8.1-brightgreen.svg)
![License MIT](https://img.shields.io/badge/license-MIT-blue.svg)

## Usage

Start the Docker container:

    docker run -p 80:8080 trafex/php-nginx

See the PHP info on http://localhost, or the static html page on http://localhost/test.html

Or mount your own code to be served by PHP-FPM & Nginx

    docker run -p 80:8080 -v ~/my-codebase:/var/www/html trafex/php-nginx

## Configuration
In [config/](config/) you'll find the default configuration files for Nginx, PHP and PHP-FPM.
If you want to extend or customize that you can do so by mounting a configuration file in the correct folder;

Nginx configuration:

    docker run -v "`pwd`/nginx-server.conf:/etc/nginx/conf.d/server.conf" trafex/php-nginx

PHP configuration:

    docker run -v "`pwd`/php-setting.ini:/etc/php81/conf.d/settings.ini" trafex/php-nginx

PHP-FPM configuration:

    docker run -v "`pwd`/php-fpm-settings.conf:/etc/php81/php-fpm.d/server.conf" trafex/php-nginx

_Note; Because `-v` requires an absolute path I've added `pwd` in the example to return the absolute path to the current directory_

## Documentation and examples
To modify this container to your specific needs please see the following examples;

* [Adding xdebug support](https://github.com/TrafeX/docker-php-nginx/blob/master/docs/xdebug-support.md)
* [Adding composer](https://github.com/TrafeX/docker-php-nginx/blob/master/docs/composer-support.md)
* [Getting the real IP of the client behind a load balancer](https://github.com/TrafeX/docker-php-nginx/blob/master/docs/real-ip-behind-loadbalancer.md)
* [Sending e-mails](https://github.com/TrafeX/docker-php-nginx/blob/master/docs/sending-emails.md)