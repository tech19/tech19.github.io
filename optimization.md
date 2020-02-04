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

### phpFastCache

{% hint style="info" %}
composer require phpfastcache/phpfastcache
{% endhint %}

**event :** when something is deleted from the cache, you could catch this event and refresh or delete related data as well

[https://code.tutsplus.com/tutorials/boost-your-website-performance-with-phpfastcache--cms-31031](https://code.tutsplus.com/tutorials/boost-your-website-performance-with-phpfastcache--cms-31031)

```php
// directory writable by the web server, 775
CacheManager::setDefaultConfig([
  "path" => __DIR__ . "/cache"
]);
$objFilesCache = CacheManager::getInstance('files');
$key = "home_page";
$CachedString = $objFilesCache->getItem($key);
if (!$CachedString->isHit()))
{
    $numberOfSeconds = 60;
    $CachedString->set("a")->expiresAfter($numberOfSeconds);
    $objFilesCache->save($CachedString);
}
$result = $CachedString->get();
```

### GZIP Compression

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

