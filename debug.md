---
title: debug
categories:
  - debug
tags:
  - debug
  - log
toc: true
---

# debug

## monolog

```php
use Monolog\Logger;
$log = new Logger('my_logger');
$log->pushHandler(new StreamHandler('your.log', Logger::WARNING));  // file name, current dir
$log->warning('Foo');
$log->error('Bar');
```

## error log

use function:  **error\_log**\(message,type,destination,headers\);   
\[php.ini\]   
error\_log = php\_errors.log   
error\_log="C:\xampp\tmp\php\_error\_log"   
with **mtail.exe**

```php
error_log("hello, this is a test!");
```

## ChromePhp

```php
ChromePhp::log($pk);
```

