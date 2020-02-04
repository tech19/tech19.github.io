# Optimization

### List

Combine css, js   
Minification css, js, html Gzip   
Asynchronous js   
Optimize css delivery: eliminate css render-blocking ?   
Optimize images CDN Lazy load images   
Http 헤더 : expires, cache-control, if-modified-since   
memcached, redis, oPcache, php7.2

```text
if (substr_count($_SERVER['HTTP_ACCEPT_ENCODING'], 'gzip')) ob_start('ob_gzhandler');
else ob_start();

mod_defalte
```

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

