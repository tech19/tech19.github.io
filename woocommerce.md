# woocommerce

[http://domain/wp-login.php?action=logout](http://domain/wp-login.php?action=logout)\
[http://domain/wp-login.php?action=register](http://domain/wp-login.php?action=register)

> Bypass "Are you sure you want to log out?" message in (WooCommerce) or not Removing logout confirmation

```php
add_action('wp_logout','logout_redirect');
function logout_redirect(){
    wp_redirect( home_url() );
    exit;
}

function change_menu($items){
  foreach($items as $item){
    if( $item->title == "Logout"){
         $item->url = $item->url . "&_wpnonce=" . wp_create_nonce( 'log-out' );
    }
  }
  return $items;
}
add_filter('wp_nav_menu_objects', 'change_menu');
```

#### Customize woocommerce pages

#### Copy wp

When and how to install wordpress in a subdirectory\
File, db 넣고\
wp-options table에 siteurl, home 바꾸고\
Wp-config.php에 db 정보 바꾸고\
Searchdb 를 실행하고 \
Settings > Permalinks : save

### woocommerce rest api

{% embed url="https://woocommerce.github.io/woocommerce-rest-api-docs/#" %}

> REST API keys

1. WordPress admin interface WooCommerce > Settings > API > Keys/Apps.
2. can be auto-generated through an endpoint

> composer require automattic/woocommerce

```php
require __DIR__ . '/vendor/autoload.php';
use Automattic\WooCommerce\Client;
$woocommerce = new Client(
    'http://example.com', // Your store URL
    'consumer_key', // Your consumer key
    'consumer_secret', // Your consumer secret
    [
        'wp_api' => true, // Enable the WP REST API integration
        'version' => 'wc/v2', // WooCommerce WP REST API version
		
		//Example for servers that not properly parse the Authorization header:
		'query_string_auth' => true // Force Basic Authentication as query string true and using under HTTPS
    ]
);
```
