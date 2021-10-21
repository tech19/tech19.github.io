# remove website(url) in comment input field

```php
function mko_disable_comment_url($fields) {
    unset($fields['url']);
    return $fields;
}
add_filter('comment_form_default_fields','mko_disable_comment_url');
```
