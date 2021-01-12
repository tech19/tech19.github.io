# Lavavel Voyager

## Building a blog with Laravel and Voyager

[https://www.youtube.com/watch?v=R\_3OHYb8hsE&list=PLY7SzAmnEqp6bOl-AehM9dX3UKlxTjMVD&index=4](https://www.youtube.com/watch?v=R_3OHYb8hsE&list=PLY7SzAmnEqp6bOl-AehM9dX3UKlxTjMVD&index=4)

### create DB

### install Laravel with composer

with laravel version:   composer create-project laravel/laravel=7.30.0 laravel-voyager --prefer-dist  
change **.env** file

### configure Phpstorm for Lavavel

npm install

### install Voyager 

```bash
composer require tcg/voyager
php artisan voyager:install --with-dummy
```

[http://laravel-voyager/admin](http://laravel-voyager/admin)

> **email:** `admin@admin.com`  
> **password:** `password`

### create new admin user \(if not use dummy data option\)

```bash
php artisan voyager:admin your@email.com --create
```

And you will be prompted for the users name and password.

### site template

startbootstrap.com 같은데서 하나 정해서 git clone 주소 가지고 public/static-html 디렉토리 만들어서 그안에서 git clone 주소 =&gt; 하면 디렉토리가 생겨서 안됨, 어쨋든 파일 카피

### configure Views 

\[\[\[그런데 이렇게 sub directory안에서 계속 작업을 할건가? 🙄  
😀아아, static-html 폴더에 받은 파일들을 짤라서 밑에 만든 파일들에 넣을거다.  
laravel에서 어떻게 전체 페이지 와꾸를 잡는지를 밑에서 보여주고 있다.  
[https://www.youtube.com/watch?v=1lC5TF4RD1k&list=PLY7SzAmnEqp6bOl-AehM9dX3UKlxTjMVD&index=8](https://www.youtube.com/watch?v=1lC5TF4RD1k&list=PLY7SzAmnEqp6bOl-AehM9dX3UKlxTjMVD&index=8) \]\]\]

resources/views 밑에 /layouts 만들고 그안에 master.blade.php  
...

끝으로 route로 /를 즉 index 페이지를 welcome 에서 home으로.

라라벨 안의 route 를 통한 blade 파일들의 프로젝트 안에 있는 css, js 는 그냥 못 가져오고   
{{asset\(...\)}} 을 통해서 그리고 이것들은 /public 안에 있어야 하는듯.

### frontend에서 backend의 data이

create controller:  php artisan make:controller HomeController  
만들어진 controller의 위치는 /app/Http/Controllers

그런데 🙄 voyager가 만든 model은 Laravel의 model이 아니다. 그래서   
1. 라라벨 모델을 따로 만들거나  
2. use TCG\Voyager\Modes\모델이름 을써서 이

👀 blade 파일안에 그냥 php code를 써도 되나? blade 문법말고 👀





