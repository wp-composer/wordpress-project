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

## What does the template do?

When installing the given `composer.json` some tasks are taken care of:

* Wordpress will be installed in the `web`-directory.
* Autoloader is implemented to use the generated composer autoloader in `vendor/autoload.php`
* Plugins (packages of type `wordpress-plugin`) will be placed in `web/wp-content/plugins/`
* Plugins (packages of type `wordpress-plugin`) will be placed in `web/wp-content/mu-plugins/`
* Theme (packages of type `wordpress-muplugin`) will be placed in `web/wp-content/themes/`
* Creates environment variables based on your .env file. See [.env.example](.env.example).

## Updating Wordpress Core

This project will attempt to keep all of your Wordpress Core files up-to-date.

Follow the steps below to update your core files.

1. Run `composer update "johnpbloch/wordpress-core" --with-dependencies` to update Wordpress Core and its dependencies.
2. Run `git diff` to determine if any custom changes are reverted.
   1. Commit everything all together in a single commit, so `web` will remain in
      sync with the `core` when checking out branches or running `git bisect`.
   2. In the event that there are non-trivial conflicts in step 2, you may wish
      to perform these steps on a branch, and use `git merge` to combine the
      updated core files with your customized files. This facilitates the use
      of a [three-way merge tool such as kdiff3](http://www.gitshah.com/2010/12/how-to-setup-kdiff-as-diff-tool-for-git.html). This setup is not necessary if your changes are simple;
      keeping all of your modifications at the beginning or end of the file is a
      good strategy to keep merges easy.

## FAQ

### Should I commit the plugins or themes I download?

Composer recommends **no**. They provide [argumentation against but also
workrounds if a project decides to do it anyway](https://getcomposer.org/doc/faqs/should-i-commit-the-dependencies-in-my-vendor-directory.md).

### How can I apply patches to downloaded plugins?

If you need to apply patches (depending on the project being modified, a pull
request is often a better solution), you can do so with the
[composer-patches](https://github.com/cweagans/composer-patches) plugin.

To add a patch to Wordpress plugin really-simple-ssl insert the patches section in the extra
section of composer.json:

```json
"extra": {
    "patches": {
        "wpackagist-plugin/really-simple-ssl": {
            "Patch description": "URL or local path to patch"
        }
    }
}
```

This will also work for Wordpress core patches.

```json
"extra": {
    "patches": {
        "johnpbloch/wordpress-core" : {
             "Issue #1486: Alter how Twenty Twenty-One sets up Dark Mode support.": "https://patch-diff.githubusercontent.com/raw/WordPress/wordpress-develop/pull/1486.patch"
        }
    }
}
```

### How do I specify a PHP version ?

This project supports PHP 7.4 as minimum version (see [Wordpress requirements](https://wordpress.org/about/requirements/)), however it's possible that a `composer update` will upgrade some package that will then require PHP 7.4+.

To prevent this you can add this code to specify the PHP version you want to use in the `config` section of `composer.json`:

```json
"config": {
    "sort-packages": true,
    "platform": {
        "php": "7.4.21"
    }
},
```
