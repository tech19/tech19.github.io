# Laravel

### Functions

authentication\
routing\
sessions\
caching\
translation\
migrate

psm supported by laravel plugin and laravel-ide-helper below

{% embed url="https://github.com/barryvdh/laravel-ide-helper" %}

{% embed url="https://plugins.jetbrains.com/plugin/7532-laravel" %}

### phpstorm setup

[https://www.jetbrains.com/help/phpstorm/laravel.html](https://www.jetbrains.com/help/phpstorm/laravel.html) &#x20;

1.  **Laravel plugin** is [installed and enabled](https://www.jetbrains.com/help/phpstorm/managing-plugins.html#repos)\
    `code completion(ctrl+space), code navigation(ctrl+B or ctrl+click), Live Templates`


2.  **Live Templates for phpstorm**\
    type a few letter **and ctrl+J** then continue type to filter\
    Generating code with Live Templates ([https://github.com/koomai/phpstorm-laravel-live-templates](https://github.com/koomai/phpstorm-laravel-live-templates))

    1. Go to _Preferences | Tools | Settings Repository_
    2. Add Read-only Source [https://github.com/koomai/phpstorm-laravel-live-templates](https://github.com/koomai/phpstorm-laravel-live-templates)
    3. Restart PhpStorm.
    4. To see all templates, go to _Preferences | Live Templates_ and expand the Template Group.

    \
    Annotations \
    Blade \
    Input \
    Request \
    Cookie \
    Route \
    View \
    Response \
    Redirect \
    Schema (includes column types) \
    Cache \
    Form \
    Session \
    Helpers\

3.  **Laravel IDE helper :** \
    **PHPDoc**\
    Install [Laravel IDE helper generator](https://github.com/barryvdh/laravel-ide-helper)   `barryvdh/laravel-ide-helper`

    `artisan ide-helper:generate` command to generate the required `PHPDoc` information\
    \
    Add Laravel IDE helper as a `ServiceProvider` into the application\
    &#x20;In the config/app.php file, add `Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider::class` under the `providers` element:\
    `// Laravel IDE helper` \
    `'Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider',`
4. **Laravel generators Composer package** \
   3개의 추가 make commands\
   install the [Laravel generators Composer package](https://github.com/laracasts/Laravel-5-Generators-Extended) to add various Laravel generators for models, views, controllers, and much more.\
   [https://github.com/laracasts/Laravel-5-Generators-Extended](https://github.com/laracasts/Laravel-5-Generators-Extended)\
   `composer require laracasts/generators --dev`

{% hint style="info" %}
&#x20;[Laracast PhpStorm tutorials](https://laracasts.com/series/how-to-be-awesome-in-phpstorm)\
그냥 phpstorm에 관한설명
{% endhint %}

## User / Admin

:heart: a make:auth

:heart: a make:migration create\_admins\_table --create=admins

:heart: a migrate

:heart: make admin model manually by coping User.php\
\[ Admin.php]  ??

```php
protected $guard = 'admin';
```

:heart: config admin guard \
\[ config/auth.php]

```php
//   config/auth.php
'defaults' => [
        'guard' => 'web',
        'passwords' => 'users',
],
// below use defaults guard
// Auth::check($a);
// Auth::attempt($a);
// to use specific guard
// Auth::guard('admin)->check($a);
'guards' => [
        'web' => [
            'driver' => 'session',
            'provider' => 'users',
        ],

        'api' => [
            'driver' => 'token',
            'provider' => 'users',
            'hash' => false,
        ],
],
'providers' => [
        'users' => [
            'driver' => 'eloquent',
            'model' => App\User::class,
        ],

        // 'users' => [
        //     'driver' => 'database',
        //     'table' => 'users',
        // ],
],
```

:heart: /admin 밑에 HomeController만들고, web.php에 get route만들고

라우트에 쓸 controller 중에 admin 권한을 필요로 할때 아래의 middleware 로&#x20;

```php
    public function __construct()
    {
        $this->middleware('auth:admin');
    }
```

\[redirect to admin login]

\[admin login: form, process]

:heart: a make:controller Auth/AdminLoginController\
trait AuthenticatesUsers 참고로\
Auth를 admin 밑에 두면 user에서 쓰는파일이름을 그대로 쓸수있다.
