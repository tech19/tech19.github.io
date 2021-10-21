# security

### referer url&#x20;

validate referer url: $\_SERVER\['HTTP\_REFERER'] is full url&#x20;

```php
if ($_SERVER['HTTP_HOST'] !== parse_url($_SERVER['HTTP_REFERER'], PHP_URL_HOST)) {
  $error = true;
}
```

