---
title: lumen
categories:
  - lumen
tags:
  - lumen
toc: true
---

# lumen

\[phpdotenv\] .env .env.example\(with no data\) file loads environment variables from `.env` to `getenv()`, `$_ENV` `$_SERVER` Add your application configuration to a .env file in the root of your project. Make sure the .env file is added to your .gitignore so it is not checked-in the code

`git commit -am"Enable Facades and Eloquent"`

PHP configuration files located in the vendor/laravel/lumen-framework/config folder create a config/ folder in the root of the project, you can copy over config files and the application will read your copied file instead of the vendor config file.

Unit Tests Running phpunit Tests -&gt; vendor/bin/phpunit

**laravel-ide-helper** supports Lumen as of August 2015. Here's what you need to do: Either execute the command composer require barryvdh/laravel-ide-helper or add the following to the require key in composer.json: "barryvdh/laravel-ide-helper": "2.\*"

Once you have installed the dependency, edit the file bootstrap/app.php and look for the Register Service Providers section and add the following line:

```text
After that, you just need to create the _ide_helper.php file with the following command:
php artisan ide-helper:generate
root에 설치경우와 sub에 설치시 차이점
    ? route와 user의 authen, authorize 가능
    sub로 할때 uri 처리가 어떻게 되는지 -> api로 쓸때
https://www.cloudways.com/blog/creating-rest-api-with-lumen/
** build a REST API in Lumen    
- bootstrap/app.php
```php
$app->withFacades();
$app->withEloquent();
```

* The Model app/Car.php

  ```php
  namespace App; 
  use Illuminate\Database\Eloquent\Model; 
  class Car extends Model
  { 
     protected $fillable = ['make', 'model', 'year'];     
  }
  ```

* The Controller app/Http/Controllers/CarController.php.

route setup app/Http/routes.php OR routes/web.php OR routes/api.php

Installing Laravel in a Subfolder

