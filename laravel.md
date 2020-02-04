# Laravel

### Functions

authentication  
routing  
sessions  
caching  
translation

psm supported by laravel plugin and laravel-ide-helper below

{% embed url="https://github.com/barryvdh/laravel-ide-helper" %}

{% embed url="https://plugins.jetbrains.com/plugin/7532-laravel" %}

### phpstorm setup

[https://www.jetbrains.com/help/phpstorm/laravel.html](https://www.jetbrains.com/help/phpstorm/laravel.html)  

1. **Laravel plugin** is [installed and enabled](https://www.jetbrains.com/help/phpstorm/managing-plugins.html#repos)  
   `code completion(ctrl+space), code navigation(ctrl+B or ctrl+click), Live Templates`

2. **Live Templates for phpstorm**  
   type a few letter **and ctrl+J** then continue type to filter  
   Generating code with Live Templates \([https://github.com/koomai/phpstorm-laravel-live-templates](https://github.com/koomai/phpstorm-laravel-live-templates)\)

   1. Go to _Preferences \| Tools \| Settings Repository_
   2. Add Read-only Source [https://github.com/koomai/phpstorm-laravel-live-templates](https://github.com/koomai/phpstorm-laravel-live-templates)
   3. Restart PhpStorm.
   4. To see all templates, go to _Preferences \| Live Templates_ and expand the Template Group.

  
   Annotations   
   Blade   
   Input   
   Request   
   Cookie   
   Route   
   View   
   Response   
   Redirect   
   Schema \(includes column types\)   
   Cache   
   Form   
   Session   
   Helpers  

3. **Laravel IDE helper :   
   PHPDoc**  
   Install [Laravel IDE helper generator](https://github.com/barryvdh/laravel-ide-helper)   `barryvdh/laravel-ide-helper`

   `artisan ide-helper:generate` command to generate the required `PHPDoc` information  
  
   Add Laravel IDE helper as a `ServiceProvider` into the application  
    In the config/app.php file, add `Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider::class` under the `providers` element:  
   `// Laravel IDE helper   
   'Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider',`

4. **Laravel generators Composer package**  3개의 추가 make commands install the [Laravel generators Composer package](https://github.com/laracasts/Laravel-5-Generators-Extended) to add various Laravel generators for models, views, controllers, and much more. [https://github.com/laracasts/Laravel-5-Generators-Extended](https://github.com/laracasts/Laravel-5-Generators-Extended) `composer require laracasts/generators --dev`

{% hint style="info" %}
 [Laracast PhpStorm tutorials](https://laracasts.com/series/how-to-be-awesome-in-phpstorm)  
그냥 phpstorm에 관한설명
{% endhint %}



