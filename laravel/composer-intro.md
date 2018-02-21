# Composer intro

## What is a dependency?
Dependencies are outside code packages that a project may utilize (i.e. they depend on it).

Examples:
+ `Form.php` is a single-file dependency I provided that you manually included in your projects.
+ jQuery is a client-side JS dependency that can be manually included with your projects or linked via a CDN (*Content Delivery Network*, e.g. [cdnjs.com](http://cdnjs.com)).
+ Similar to jQuery, Bootstrap is a client-side CSS dependency.

Frameworks like Laravel require many dependencies, and so it is built using dependency management software called Composer.

## What is Composer?
[Composer](https://getcomposer.org) is a **dependency manager** program for PHP. Rather than manually downloading or referencing code packages like you might with the above examples, you can specify in a configuration file what packages your application needs. Composer will then read this config file and download/update the appropriate software as needed.

For example, here's the dependency configuration for a new Laravel project:
```json
 "require": {
        "php": ">=5.6.4",
        "laravel/framework": "5.4.*",
        "laravel/tinker": "~1.0"
    },
    "require-dev": {
        "fzaninotto/faker": "~1.4",
        "mockery/mockery": "0.9.*",
        "phpunit/phpunit": "~5.7"
    },
```

The full library of packages available for management via Composer are found via [Packagist](http://packagist.org).

(Dependency management is not unique to PHP - other examples include Node's *NPM* and Ruby's *Bundler*.)

Like Git, Composer is a __command line program__ (installation instructions in the notes that follow).
<img src='http://making-the-internet.s3.amazonaws.com/laravel-composer-logo-in-command-line@2x.png' class='' style='max-width:776px; width:100%' alt='Composer called in command line'>

## Composer = server-side packages
While there are some client-side packages available via Packagist/Composer, we will only use it to manage our __server-side, PHP-based packages__.

If you choose to use client-side packages in your projects (like jQuery, Bootstrap, etc.) you should manually download them to your project or link them from a CDN. 

Dependency management for client-side assets is outside the scope of this course. However, later in the semester I will post some supplemental material in the course Issues forum with details on how you might manage your client-side assets.





## Tangential feature of Composer: Autoloading
[Autoloading](http://php.net/manual/en/language.oop5.autoload.php) allows you to access classes in your application without having to explicitly include the class file.

Instead, you can provide a map for your application where it will look for classes and load them, on-demand, as needed.

With autoloading, you no longer have to do something like this:
```php
require 'Form.php';

use DWA\Form;
$form = new Form;
```

Instead, your application can find the class for you, so you only need to do this:

```php
use DWA\Form;
$form = new Form;
```

It seems trivial in this small example, but it's a very useful feature to have as the complexity of your application grows and with it, your usage of classes.

In addition to managing packages, Composer also builds and maintains a class map for your application, allowing you to harness auto-loading.

You don't have to worry about using/understanding auto-loading right now, just know that when we use it, it's being powered by Composer.

