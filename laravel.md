# Laravel

authentication  
routing  
sessions  
caching

psm supported by laravel plugin and laravel-ide-helper below

{% embed url="https://github.com/barryvdh/laravel-ide-helper" %}

{% embed url="https://plugins.jetbrains.com/plugin/7532-laravel" %}

plugin: Enable autopopup for completion in plugin setting

### phpstorm setup

[https://www.jetbrains.com/help/phpstorm/laravel.html](https://www.jetbrains.com/help/phpstorm/laravel.html)  

1. Laravel plugin is [installed and enabled](https://www.jetbrains.com/help/phpstorm/managing-plugins.html#repos)  
   code completion,   
   code navigation,   
   Generating code with Live Templates \([https://github.com/koomai/phpstorm-laravel-live-templates](https://github.com/koomai/phpstorm-laravel-live-templates)\)

   1. Go to _Preferences \| Tools \| Settings Repository_
   2. Add Read-only Source [https://github.com/koomai/phpstorm-laravel-live-templates](https://github.com/koomai/phpstorm-laravel-live-templates)
   3. Restart PhpStorm.
   4. To see all templates, go to _Preferences \| Live Templates_ and expand the Template Group.

   Enable Blade debugging

2. Install [Laravel IDE helper generator](https://github.com/barryvdh/laravel-ide-helper) barryvdh/laravel-ide-helper
3.  Add Laravel IDE helper as a `ServiceProvider` into the application  In the config/app.php file, add `Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider::class` under the `providers` element: // Laravel IDE helper  'Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider',
4.  install the [Laravel generators Composer package](https://github.com/laracasts/Laravel-5-Generators-Extended) to add various Laravel generators for models, views, controllers, and much more. [https://github.com/laracasts/Laravel-5-Generators-Extended](https://github.com/laracasts/Laravel-5-Generators-Extended)
5. artisan as a command line tool  `artisan ide-helper:generate` command to generate the required `PHPDoc` information

{% hint style="info" %}
 [Laracast PhpStorm tutorials](https://laracasts.com/series/how-to-be-awesome-in-phpstorm)  
그냥 phpstorm에 관한
{% endhint %}



