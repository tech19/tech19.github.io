---
title: slim
categories:
  - slim
tags:
  - slim
toc: true
---

# slim

## $this

* inside route: it's container. how to use: $this-&gt;name
* how to access container inside function global $container; $db = $container\['mysqlDB'\];
* in class

  \`\`\`php use Psr\Container\ContainerInterface; protected $container; public function \_\_construct\(ContainerInterface $container\) { $this-&gt;container = $container; } public function xxx\(\){ /_\* @var MysqliDb $db_ / $db = $this-&gt;container-&gt;get\('mysqlDB'\); or $db = $container-&gt;get\('mysqlDB'\); // todo test $db = $container-&gt;mysqlDB; // todo test }

//Override the default Not Found Handler $c\['notFoundHandler'\] = function \($c\) { return function \($request, $response\) use \($c\) { return $c\['response'\] -&gt;withStatus\(404\) -&gt;withHeader\('Content-Type', 'text/html'\) -&gt;write\('Page not found'\); }; };

$container\['view'\] = function \($c\) { $view = new \Slim\Views\Twig\('./public/template/'\); $view-&gt;addExtension\(new \Slim\Views\TwigExtension\( $c\['router'\], $c\['request'\]-&gt;getUri\(\) \)\); return $view; };

$container\['notFoundHandler'\] = function \($c\) { return function \($request, $response\) use \($c\) { return $c\['view'\]-&gt;render\($response-&gt;withStatus\(404\), '404.html', \[ "myMagic" =&gt; "Let's roll" \]\); }; };

$container\['view'\] = new \Slim\Views\PhpRenderer\('../templates/'\);

$app-&gt;get\('/tickets', function \(Request $request, Response $response\) { $this-&gt;logger-&gt;addInfo\('Ticket list'\); $mapper = new TicketMapper\($this-&gt;db\); $tickets = $mapper-&gt;getTickets\(\);

```text
$response = $this->view->render($response, 'tickets.php', ['tickets' => $tickets]);
return $response;
```

}\);

$app-&gt;get\('/ticket/{id}', function \(Request $request, Response $response, $args\) { // ... }\)-&gt;setName\('ticket-detail'\);

&lt;?php foreach \($tickets as $ticket\): ?&gt;  &lt;?php endforeach; ?&gt;

```text
### install
subfolder에 -> composer create-project slim/slim-skeleton [folder] => 이거 말고

그냥 composer로 넣고, directory 만들고 (ex. api), 
.htaccess만들고 안에
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^ index.php [QSA,L]

composer.json 에 psr-4 autoload 넣고
,
"autoload": {
  "psr-4": {
    "API\\": "api/"
  }
}

index.php 만들고 
```php
use \Psr\Http\Message\ServerRequestInterface as Request;
use \Psr\Http\Message\ResponseInterface as Response;

$app = new \Slim\App;
$app->get('/hello/{name}', function (Request $request, Response $response) {
    $name = $request->getAttribute('name');
    $response->getBody()->write("Hello, $name");

    return $response;
});
...
try {
    $app->run();
} catch (Exception $e) {
    echo $e->getMessage();
}
```

with slim + Idiorm + Monolog 2014: without container [https://www.sitepoint.com/best-practices-rest-api-scratch-introduction/](https://www.sitepoint.com/best-practices-rest-api-scratch-introduction/)  
[https://www.sitepoint.com/best-practices-rest-api-scratch-implementation/](https://www.sitepoint.com/best-practices-rest-api-scratch-implementation/)

[http://blog.daum.net/techtip/12415195](http://blog.daum.net/techtip/12415195) [https://www.slideshare.net/ssuser7887b3/restful-api](https://www.slideshare.net/ssuser7887b3/restful-api)

\*[https://www.ibm.com/developerworks/library/x-slim-rest/index.html](https://www.ibm.com/developerworks/library/x-slim-rest/index.html)

## slim / RedBean

```php
// load required files
require 'Slim/Slim.php';
require 'RedBean/rb.php';

// register Slim auto-loader
\Slim\Slim::registerAutoloader();

// set up database connection
R::setup('mysql:host=localhost;dbname=appdata','user','pass');
R::freeze(true);

// initialize app
$app = new \Slim\Slim();

// handle GET requests for /articles
$app->get('/articles', function () use ($app) {  
  // query database for all articles
  $articles = R::find('articles'); 

  // send response header for JSON content type
  $app->response()->header('Content-Type', 'application/json');

  // return JSON-encoded response body with query results
  echo json_encode(R::exportAll($articles));
});

// run
$app->run();

// handle GET requests for /articles  **** middleware: authenticate
$app->get('/articles', 'authenticate', function () use ($app) {    // old version
  // query database for all articles
  $articles = R::find('articles'); 

  // send response header for JSON content type
  $app->response()->header('Content-Type', 'application/json');

  // return JSON-encoded response body with query results
  echo json_encode(R::exportAll($articles));
});

// generates a temporary API key using cookies
// call this first to gain access to protected API methods
$app->get('/demo', function () use ($app) {    
  try {
    $app->setEncryptedCookie('uid', 'demo', '5 minutes');
    $app->setEncryptedCookie('key', 'demo', '5 minutes');
  } catch (Exception $e) {
    $app->response()->status(400);
    $app->response()->header('X-Status-Reason', $e->getMessage());
  }
});

// run
$app->run();
```

## slim-bookshelf

_\*\*_ [https://github.com/akrabat/slim-bookshelf](https://github.com/akrabat/slim-bookshelf) slim-bookshelf/app/src/Bookshelf/ 안에 controller, model 들이 있다.

// Route configuration $app-&gt;get\('/', 'Bookshelf\AuthorController:listAuthors'\)-&gt;setName\('list-authors'\);

$app-&gt;map\(\['GET', 'POST'\], '/authors/{author\_id:\[0-9\]+}/edit', 'Bookshelf\AuthorController:editAuthor'\)-&gt;setName\('edit-author'\);

$app-&gt;get\('/books', 'Bookshelf\BookController:listBooks'\)-&gt;setName\('list-books'\);

$app-&gt;get\('/authors/{author\_id:\[0-9\]+}', 'Bookshelf\AuthorController:listBooks'\)-&gt;setName\('author'\); --&gt; ? city/cityname .... -&gt; setName\('citySlist'\) --&gt; echo ... /city/city ////**---&gt; setName ---&gt; \*\*** generate a URL for this named route with the application router’s pathFor\(\) method. echo $app-&gt;getContainer\(\)-&gt;get\('router'\)-&gt;pathFor\('author', \[ 'author\_id' =&gt; '432' \]\); // Outputs "/author/432" to display url list ????  
_\*_ --&gt; ex. change part of url \(city -&gt; cities\)

**add 404** [http://help.slimframework.com/discussions/problems/10851-how-to-add-404-template-in-slim-3](http://help.slimframework.com/discussions/problems/10851-how-to-add-404-template-in-slim-3) **\*** NotFound function or class

\*\*DI: [http://wani.kr/posts/2015/08/07/wandu-di/](http://wani.kr/posts/2015/08/07/wandu-di/)

* container ? container setting code -&gt; where?
* class + func + container
* class 

!!! url direct access block ???

_\*_ restful api test client 사용

\[authentication middleware\] search 'with slim'

* oscarotero/psr7-middlewares
* tuupola/slim-basic-auth
* jeremykendall/slim-auth

\[authentication middleware\]

* slimphp/Slim-Csrf

\*\*slim index 구성 \[index\]

```php
session_start();
// app config file
if (file_exists('app/settings.php')) {
    $settings = require 'app/settings.php';
} else {
    $settings = require 'app/settings.php.dist';
}
// Instantiate Slim
$app = new \Slim\App($settings);
// container setting
require 'app/src/dependencies.php';
    -> db connection ...
require 'app/src/middleware.php';
// Register the routes
require 'app/src/routes.php';
    $app->get('/', 'Bookshelf\AuthorController:listAuthors')->setName('list-authors');
    $app->map(['GET', 'POST'], '/authors/{author_id:[0-9]+}/edit', 'Bookshelf\AuthorController:editAuthor')->setName('edit-author');
    $app->get('/authors/{author_id:[0-9]+}', 'Bookshelf\AuthorController:listBooks')->setName('author');
    $app->get('/books', 'Bookshelf\BookController:listBooks')->setName('list-books');
// Register the database connection with Eloquent
$capsule = $app->getContainer()->get('capsule');
$capsule->bootEloquent();
$app->run();
```

## middleware auth in class

\*\*slim middleware class example

```php
namespace App\middleware;
use Psr\Http\Message\ServerRequestInterface as Request;
use Psr\Http\Message\ResponseInterface as Response;
use Slim\Router;
class Auth
{
    protected $router;
    public function __construct(Router $router)
    {
        $this->router = $router;
    }
    /**
     * Auth middleware invokable class
     *
     * @param \Psr\Http\Message\ServerRequestInterface $request  PSR7 request
     * @param \Psr\Http\Message\ResponseInterface      $response PSR7 response
     * @param callable                                 $next     Next middleware
     *
     * @return \Psr\Http\Message\ResponseInterface
    **/
    public function __invoke(Request $request, Response $response, $next)
    {
        $loggedIn = $_SESSION['isLoggedIn'];
        if ($loggedIn != 'yes') {
            // If the user is not logged in, redirect them home
            return $response->withRedirect($this->router->pathFor('home'));
        }
        // The user must be logged in, so pass this request down the middleware chain
        $response = $next($request, $response);
        // And pass the request back up the middleware chain.
        return $response;
    }
}
```

--&gt; class + invoke + middleware + auth\(session으로\) --&gt; register into container --&gt; add to route ?? --&gt; csrf도 같은 방법으로?? --&gt; referer도 같은 방법으로?? --&gt; ?? 여러개의 middleware를 거는 방법, 끝에서 부터적용 --&gt; chain -&gt;add\(\)-&gt;add\(\)-&gt;add\(\)

--&gt; 처음거 실패면 나머지 skip??

## Get all get/put/post parameters:  slim3

GET

```php
$allGetVars = $request->getQueryParams();
foreach($allGetVars as $key => $param){
   //GET parameters list
}
```

POST or PUT

```php
$allPostPutVars = $request->getParsedBody();
foreach($allPostPutVars as $key => $param){
   //POST or PUT parameters list
}
```

Single parameters value:

Single GET parameter

```text
$getParam = $allGetVars['title'];
```

Single POST/PUT parameter

```text
$postParam = $allPostPutVars['postParam'];
```

OR -&gt;

```text
public function editAuthor($request, $response, $params)
$id = $params['author_id'];
```

## to use session within class

```php
//session_start();   ????  ok without ??
if (!isset($_SESSION['names']))
    $_SESSION['names'] = array("jane","jim","john","emily","bill","sara");

class Name
{
  public $id;
  public $name;
  public function __construct($id, $name)
  {
    $this->id = $id;
    $this->name = $name;
  }
  public function create()
  {
    $_SESSION['names'][] = $this->name;
  }
  public function update()
  {
    $_SESSION['names'][$this->id] = $this->name;
  }
  public static function delete($id)
  {
    unset($_SESSION['names'][$id]);
  }
  public static function findAll()
  {
    $names = array();
    foreach($_SESSION['names'] as $id => $name)
        $names[] = new Name($id , $name);
    return $names;
  }
  public static function find($id)
  {
    return new Name($id, $_SESSION['names'][$id]);
  }
}
```

\*\* [https://gist.github.com/jlebensold/1469109](https://gist.github.com/jlebensold/1469109) Deleting with REST, SLIM and JSON

\*\* \[[https://www.userfrosting.com/](https://www.userfrosting.com/)\] slim, twig, eloquent: slim app example

??

slim function: $params how to use =&gt; A\) in route URL ex\) /aaa/{id} within class function: $id2 = $params\['id'\]; // it's null. not working OK with $allPostPutVars = $request-&gt;getParsedBody\(\); // post method $id = $allPostPutVars\['id'\];

## Use Plates template: view

PHP template system template layouts and inheritance Built-in escaping helpers [https://github.com/projek-xyz/slim-plates](https://github.com/projek-xyz/slim-plates) _\*_ github: thephpleague [http://platesphp.com/](http://platesphp.com/)  
[https://github.com/slimphp/PHP-View](https://github.com/slimphp/PHP-View)

## index.php

route를 function으로 할때는 mydb를 container에 넣지 않고 top에 두고 global로 access

## template dir direct access block

.htaccess

## Directory sturctures

composer.json, ... /public slim index /app/src route, middle, dependency /templates /class hier

/public slim index /app /controllers /src route, middle, dependency, settings /templates /vendor

/public slim index composer.json, ... /vendor /app route, middle, dependency /src /templates /class hier ??

\*\* Slim-skeleton /app - contains all application code. /routes - Slim framework routes a, b, c /views - all views /views/master - master layouts that you can extend with twig init.php  
/public - contains all assets, javascript and stylesheets. slim index : call app/init.php /vendor - contains dependencies handled by composer. composer.json, ...

## asset directory access /js /css

## pathFor

```php
pathFor('aaa', ['id' => '3']) // for route url (/asdfsd/{id})
```

