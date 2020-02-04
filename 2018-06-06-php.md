---
title: php
categories:
  - php
tags:
  - php
toc: true
---

# php

## Dynamic variable\(variable variable\)

{ }, $$

```php
${“aaa” . $i}  =  $aaa34   // ** double quote
${“a”.”b”} =  $ab
$var1 = “aa”;  $$var1 = “bb”;  $aa = “bb”;
```

## filter\_var\(\)

```php
if (filter_var($ttt, FILTER_VALIDATE_INT) === false) {
    // not integer
}
```

## data type

array list set sorted set hash

## double quote

"The {$type}s are"

