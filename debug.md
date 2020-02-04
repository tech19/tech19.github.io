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

;error\_log="C:\xampp\php\logs\php\_error\_log" error\_log="C:\xampp\tmp\php\_error\_log"

```php
error_log("hello, this is a test!");
```

## ChromePhp

```php
ChromePhp::log($pk);
```

