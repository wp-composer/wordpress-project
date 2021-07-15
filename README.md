# Composer template for Wordpress projects

This project template provides a starter kit for managing your site
dependencies with [Composer](https://getcomposer.org/).

## Usage

First you need to [install Composer](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx).

> Note: The instructions below refer to the [global Composer installation](https://getcomposer.org/doc/00-intro.md#globally).
You might need to replace `composer` with `php composer.phar` (or similar)
for your setup.

After that you can create the project:

``` bash
composer create-project wp-composer/wordpress-project:5.x-dev some-dir --no-interaction
```

With `composer require ...` you can download new dependencies to your
installation.

``` bash
cd some-dir
composer require wpackagist-plugin/really-simple-ssl
```
