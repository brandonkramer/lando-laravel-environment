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
1. Install Laravel with `lando ssh -c "composer global require laravel/installer && laravel new app"`
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
## What now?
While writing commands with Lando for local Laravel development; replace php, prefix npm and composer with lando for example `lando artisan migrate` or `lando npm install`
### Install Authentication
https://laravel.com/docs/7.x/frontend

Since Laravel 6 the `artisan make:auth` command (Auth scaffolding) has been moved into a separate package. The scaffolding is now located in the laravel/ui Composer package, which may be installed using Composer:
``` 
lando composer require laravel/ui
```
Once the laravel/ui package has been installed, you may install the frontend scaffolding using the ui Artisan command:

```
lando artisan ui bootstrap
lando artisan ui vue
lando artisan ui react
```
Generate login / registration scaffolding...
```
php artisan ui bootstrap --auth
php artisan ui vue --auth
php artisan ui react --auth
```
After installing the laravel/ui Composer package and generating the frontend scaffolding, Laravel's package.json file will include the bootstrap package to help you get started prototyping your application's frontend using Bootstrap. However, feel free to add or remove packages from the package.json file as needed for your own application. You are not required to use the Bootstrap framework to build your Laravel application - it is provided as a good starting point for those who choose to use it.
#### Database tables
Edit the .env file with your database configuration if you haven't configure it yet. Create database tables from the laravel/ui package:
```
php artisan migrate
```
### Compiling Assets (Mix)
https://laravel.com/docs/7.x/mix

Before compiling your CSS, install your project's frontend dependencies using the Node package manager (NPM):
```
lando npm install
```

Once the dependencies have been installed using npm install, you can compile your SASS files to plain CSS using Laravel Mix. The npm run dev command will process the instructions in your webpack.mix.js file. Typically, your compiled CSS will be placed in the public/css directory:
```
lando npm run dev
```
The npm run watch command will continue running in your terminal and watch all relevant files for changes. Webpack will then automatically recompile your assets when it detects a change:
```
lando npm run watch
```
## Documentation
Refer to Lando's extensive [documentation](https://docs.lando.dev/config/laravel.html).