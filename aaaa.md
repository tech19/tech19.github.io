---
title: One
toc: true
---

# aaaa

## curl https problem

download: curl-7.56.1-win64-mingw.7z extract: c:\aaa\curl\  
    curl.exe, curl-ca-bundle.crt   
add path: C:\aaa\curl;

## error log

use function -&gt; error\_log\(message,type,destination,headers\);   
\[php.ini\]   
error\_log = php\_errors.log   
error\_log="C:\xampp\tmp\php\_error\_log"   
with **mtail.exe**

## phpFastCache

```php
    // In your config file
    include("php_fast_cache.php");
    phpFastCache::$storage = "auto";
    // you can set it to files, apc, memcache, memcached, pdo, or wincache
    // I like auto

    // In your Class, Functions, PHP Pages
    // try to get from Cache first.
    $products = phpFastCache::get("products_page");

    if($products == null) {
        $products = YOUR DB QUERIES || GET_PRODUCTS_FUNCTION;
        // set products in to cache in 600 seconds = 5 minutes
        phpFastCache::set("products_page",$products,600);
    }

   OUTPUT or RETURN your $products
```

[https://www.devildoxx.com/web-development/php-tutorials/phpfastcache-tutorials/configuring-phpfastcache/](https://www.devildoxx.com/web-development/php-tutorials/phpfastcache-tutorials/configuring-phpfastcache/)

```php
//phpFastCache(xxx), phpFastCache::set(xxx)
class mycache {
    public static $cache = array();
}
mycache::$cache['my_cache_name'] = phpFastCache(whatever);

//In your function, class, do call:
$fastCache = mycache::$cache['my_cache_name'] ;
phpFastCache::set("products_page",$products,600);
$products = phpFastCache::get("products_page");
$fastCache = phpFastCache("files", array("htaccess" => true,"path" => " booster","securityKey" => "auto"));   // config options
```

1. create folder: booster

## GZIP Compression

* header: Content-encoding: gzip
* Setting up the server

  In Apache, enabling output compression is fairly straightforward. Add the following to your .htaccess file:

compress text, html, javascript, css, xml:

AddOutputFilterByType DEFLATE text/plain   
AddOutputFilterByType DEFLATE text/html   
AddOutputFilterByType DEFLATE text/xml   
AddOutputFilterByType DEFLATE text/css   
AddOutputFilterByType DEFLATE application/xml   
AddOutputFilterByType DEFLATE application/xhtml+xml   
AddOutputFilterByType DEFLATE application/rss+xml   
AddOutputFilterByType DEFLATE application/javascript   
AddOutputFilterByType DEFLATE application/x-javascript

Or, compress certain file types by extension:

```php
<files *.html>
SetOutputFilter DEFLATE
</files>
```

## jQuery UI Sortable

{% embed url="https://stackoverflow.com/questions/15633341/jquery-ui-sortable-then-write-order-into-a-database" %}



react lazy loading   
html compress   
steemit design   
Heroku   
gg map   
crud, pw, reset pw, cmd   
sel sunra domparse, sel, sel gut   
typesource: text in image, banner

[https://github.com/eisbehr-/jquery.lazy](https://github.com/eisbehr-/jquery.lazy) !!!   
[https://github.com/ressio/lazy-load-xt/](https://github.com/ressio/lazy-load-xt/) old

[https://lobianijs.com/site/lobipanel](https://lobianijs.com/site/lobipanel):min, max bootstrap panel, unpin dragable  
webframeworks.kr       code example

## grid layout: masonry

## dragable, close button panel

* [lobianijs](https://lobianijs.com/) \(admin panel\)

## bootstrap 4 admin template

[https://coreui.io/](https://coreui.io/)

## bootstrap 4 online editor

[https://www.gridbox.io/](https://www.gridbox.io/) pw: gridmko

[https://bootstrap.build/app/v4.1.1/](https://bootstrap.build/app/v4.1.1/)

