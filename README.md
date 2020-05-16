# Lando Laravel Environment
This is a Laravel development environment based on Lando which I use for my Laravel projects. 
[Lando](https://github.com/lando/lando) is an extremely flexible local development environment that is based on [Docker](https://www.docker.com/).

> Lando is powered by Docker and Docker Compose, config php version, swap db or caching backends or web server, use composer. laravel CLI and artisan, xdebug and custom config files, oh and also import and export databases.

This repository contains the Lando configuration file `.lando.yml` along with `config/php.ini` `config/nginx.conf` `config/httpd.conf` files for server configuration.

## Getting started
Before you get started with this setup I assume that you have:
1. Installed [Lando](https://github.com/lando/lando) and gotten familiar with its basics
1. Got familiar with Lando's [Laravel recipe](https://docs.lando.dev/config/laravel.html)
1. Read about the various services, tooling, events and routing Lando offers.

## Usage  
1. Configure `.lando.yml`  and replace `{project}` with project name
1. Specify the desired PHP version, web server and database server
1. Install Laravel with `lando ssh -c "composer global require laravel/installer && laravel new app`
1. Run the command `lando start` from the project root.
1. Then visit `laravel-{project}.lndo.site` to see your Laravel project

## Info
Lando will automatically set up a database with a user and password and also set an environment variables called `lando info` that contains useful information about how your application can access other Lando services.
``` 
database: laravel
username: laravel
password: laravel
host: database
# for mysql
port: 3306
# for postgres
# port: 5432
```
Go to `pma.wp-{project}.lndo.site` to visit PHPMyAdmin and `mail.wp-{project}.lndo.site` to visit MailHog.
## .env
 Configuration for Laravel's .env file.
``` 
// Database configuration
DB_CONNECTION=mysql
DB_HOST=database
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=laravel
DB_PASSWORD=laravel

// Mailhog configuration
MAIL_MAILER=smtp
MAIL_HOST=sendmailhog
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS=test@test.nl
MAIL_FROM_NAME="${APP_NAME}"

# If you have `cache: redis` in this recipes config
# REDIS_HOST=cache
# REDIS_PASSWORD=null
# REDIS_PORT=6379

```

## Documentation
Refer to Lando's extensive [documentation](https://docs.lando.dev/config/laravel.html).