# hhvm-fastcgi-boilerplate

This repository contains boilerplate code for a dockerized HHVM project that utilizes nginx, FastCGI, and HHVM.

The unique aspect of this project is that nginx proxies every request to www/public/index.hack (rather than to a matching script name based on the request URI).

This is a work in progress, but is nevertheless a good startingpoint. Of course, you may customize every file to fit your needs.

## Requirements

-   Docker
-   Docker-compose
-   npm (optional)
-   php (optional)
-   hhvm (optional)
-   composer (optional)

## Details

This project uses docker-compose to run both nginx and the HHVM server. The "./docker-hhvm-fastcgi" directory contains the Dockerfile for the HHVM server. For nginx, the default image is used.

Having npm is optional, but recommended because the "package.json" defines several convenience commands:

-   npm start (docker-compose up)
-   npm stop (docker-compose stop)
-   npm run reload-nginx (Runs nginx -s reload within the already running docker container)

Having HHVM, PHP, and Composer installed is also optional. In this case, if you do not have these installed, the docker image (defined in the "./docker-compose-with-hhvm" directory) is a convenience image for running these commands through docker. "package.json" defines a few commands for these as well:

-   npm run install-composer (Builds the docker image -- run this first)
-   npm run composer \<composer sub-command\> (Eg. run with "install" to set up composer packages)
-   npm run update-autoload-map (Runs hh-autoload within container to rebuild hack autoload map)
-   npm run build (Same as above for now)

## Directory structure

-   **docker-composer-with-hhvm** (Dockerfile for convenience image for running composer/hhvm/php)
-   **docker-hhvm-fastcgi** (Dockerfile for hhvm server set up to with in fastcgi mode)
-   **hhvm-config** (Only contains site.ini, to define additional php-ini settings)
-   **nginx-config** (Config files for nginx conf)
-   **www** (Hacklang source root)
    -   **public**
        -   **assets** (public assets served directly/statically by nginx)
        -   index.hack (HHVM entrypoint)
    -   **src** (Server source code)
    -   .hhconfig
    -   composer.json
    -   hh_autoload.json
