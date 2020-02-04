# security

### referer url

validate referer url: $\_SERVER\['HTTP\_REFERER'\] is full url

```php
if ($_SERVER['HTTP_HOST'] !== parse_url($_SERVER['HTTP_REFERER'], PHP_URL_HOST)) {
  $error = true;
}
```



