---
title: magento
categories:
  - magento
tags:
  - magento
toc: true
---

# Magento restful API, "FROM OUTSIDE OF SERVER"

* SOAP
* XML-RPC
* RESTful API \*\*

## Setting up the REST API credentials

OAuth 1.0 protocol to provide authentication System \| Web Services \| REST - OAuth Consumers, and selecting Add New in the Admin panel

```php
$callbackUrl = "http://magento.localhost.com/oauth_admin.php";
$temporaryCredentialsRequestUrl = "http://magento.localhost.com/oauth/ initiate?oauth_callback=" . urlencode($callbackUrl);
// /oauth/initiate :: WILL RETURN oauth_token, oauth_token_secret

$adminAuthorizationUrl = 'http://magento.localhost.com/admin/oAuth_authorize';
// /admin/oAuth_authorize

$accessTokenRequestUrl = 'http://magento.localhost.com/oauth/token';
// /oauth/token

$apiUrl = 'http://magento.localhost.com/api/rest';
$consumerKey = 'yourconsumerkey';
$consumerSecret = 'yourconsumersecret';

session_start();

$authType = ($_SESSION['state'] == 2) ? OAUTH_AUTH_TYPE_AUTHORIZATION : OAUTH_AUTH_TYPE_URI;
$oauthClient = new OAuth($consumerKey, $consumerSecret, OAUTH_SIG_METHOD_HMACSHA1, $authType);

$oauthClient->setToken($_SESSION['token'], $_SESSION['secret']);

// reading data
$resourceUrl = $apiUrl . "/products";
$oauthClient->fetch($resourceUrl, array(), 'GET', array('Content- Type' => 'application/json'));
$productsList = json_decode($oauthClient->getLastResponse());
// fileter category
$categoryId = 3;
$resourceUrl = $apiUrl . "/products/category_id=" . categoryId;
$oauthClient->fetch($resourceUrl, array(), 'GET', array('Content- Type' => 'application/json'));
$productsList = json_decode($oauthClient->getLastResponse());

// Update data

$productData = json_encode(array(
  'type_id'           => 'simple',
  'attribute_set_id'  => 4,
  'sku'               => 'simple' . uniqid(),
  'weight'            => 10,
  'status'            => 1,
  'visibility'        => 4,
  'name'              => 'Test Product',
  'description'       => 'Description',
  'short_description' => 'Short Description',
  'price'             => 29.99,
  'tax_class_id'      => 2,
));
$oauthClient->fetch($resourceUrl, $productData, OAUTH_HTTP_METHOD_POST, array('Content-Type' => 'application/json'));
$updatedProduct = json_decode($oauthClient- >getLastResponseInfo());

// Delete data

$productData = json_encode(array(
  'id'           => 4
));
$oauthClient->fetch($resourceUrl, $productData, OAUTH_HTTP_METHOD_DELETE, array('Content-Type' => 'application/json'));
$updatedProduct = json_decode($oauthClient- >getLastResponseInfo());
```

## Steps

Registering an Application: to get consumer Key and Secret 받고, -&gt; System &gt; Web Services &gt; REST - OAuth Consumers and clicking Add New in the Admin Panel. When registering the application, you also need to define the callback URL

## Guzzle for magento

[http://devdocs.magento.com/guides/m1x/api/rest/introduction.html\#RESTAPIIntroduction-ProductCategories](http://devdocs.magento.com/guides/m1x/api/rest/introduction.html#RESTAPIIntroduction-ProductCategories)

guzzle, gutte: Oauth composer require guzzlehttp/guzzle [https://hackernoon.com/creating-rest-api-in-php-using-guzzle-d6a890499b02](https://hackernoon.com/creating-rest-api-in-php-using-guzzle-d6a890499b02)

```php
require ‘vendor/autoload.php’;
use GuzzleHttp\Client;
use GuzzleHttp\Exception\RequestException;
use GuzzleHttp\Psr7\Request;
```

base URI, HTTP verb and headers If there is an authentication layer in the external API, you can also pass these parameters

\*\* goutte: scrap, crawing -&gt;&gt; use guzzle

* set up Guzzle 

  Admin =&gt; System =&gt; Extensions :: Integrations =&gt; Add New Integration  \(version 2 only?\)

  Consumer Key

  Consumer Secret

  Access Token

  Access Token Secret

* guzzle

  ```php
  $client = new GuzzleHttp\Client();
  $res = $client->request(‘GET’, ‘https://api.cloudways.com/api/v1’, [
    ‘headers’ => [
        ‘Accept’ => ‘application/json’,
        ‘Content-type’ => ‘application/json’
    ]
  ]);
  ```

* "cpliakas/magento-client-php": "\*" /////////// test

  \`\`\`php use Magento\Client\Rest\MagentoRestClient;

$client = MagentoRestClient::factory\(array\( 'base\_url' =&gt; '[http://magentohost](http://magentohost)', 'consumer\_key' =&gt; 'abc123...', 'consumer\_secret' =&gt; 'def456...', 'token' =&gt; 'ghi789...', 'token\_secret' =&gt; 'jkl012...', \)\);

$result = $client-&gt;get\('/api/rest/products'\)-&gt;send\(\)-&gt;json\(\); //// -&gt;json ///

```text
### 1.9  local
Your License key is: 9559634d24ec1cc6437fc8bb6af14d9e    
http://localhost.com/magento
http://localhost.com/magento/admin

user
encrypt key: c7b375af51690e1b674f6c844a132dcc

- create category = save as file, place in root
```php
$mageFilename = 'app/Mage.php';
require_once $mageFilename;
Mage::setIsDeveloperMode(true);
ini_set('display_errors', 1);
umask(0);
Mage::app('admin');
Mage::register('isSecureArea', 1);
$parentId = '2'; 
//The root category in Magento, the one you get by default install, usually has the id 2
 try{
    $category = Mage::getModel('catalog/category');
    $category->setName('your cat name');
    $category->setUrlKey('your-cat-url-key');
    $category->setIsActive(1);
    $category->setDisplayMode('PRODUCTS');
    $category->setIsAnchor(1); //for active anchor
    $category->setStoreId(Mage::app()->getStore()->getId());
    $parentCategory = Mage::getModel('catalog/category')->load($parentId);
    $category->setPath($parentCategory->getPath());
    $category->save();
} catch(Exception $e) {
    print_r($e);
}
?>

function createCategory(){
    $parentId = 1;// Any of your parent category
    $category = Mage::getModel('catalog/category');
    $category->setName('My First Category');
    $category->setUrlKey('My-First-Category');
    $category->setIsActive(1); // to make active
    $category->setDisplayMode('PRODUCTS');
    $category->setIsAnchor(1); // This is for active anchor
    $category->setStoreId(Mage::app()->getStore()->getId());
    $parentCategory = Mage::getModel('catalog/category')->load($parentId);
    $category->setPath($parentCategory->getPath());
    $category->save();
 }

 // create product
 $product = Mage::getModel("catalog/product");
            $product
            ->setStoreId(0) 
            ->setWebsiteIds(array(1)) 
            ->setAttributeSetId(4) 
            ->setTypeId('simple') 
            ->setCreatedAt(strtotime('now')) 
            ->setSku('82394444')
            ->setName('product21')
            ->setWeight(4.0000)
            ->setStatus(1)
            ->setTaxClassId(4)
            ->setVisibility(Mage_Catalog_Model_Product_Visibility::VISIBILITY_BOTH)
            ->setManufacturer(28)
            ->setColor(24)
            ->setNewsFromDate('06/26/2014')
            ->setNewsToDate('06/30/2016')
            ->setCountryOfManufacture('AF')            
            ->setPrice(11.22)
            ->setCost(22.33)
            ->setSpecialPrice(00.44)
            ->setSpecialFromDate('06/1/2015')
            ->setSpecialToDate('06/30/2016')
            ->setMsrpEnabled(1)
            ->setMsrpDisplayActualPriceType(1)
            ->setMsrp(99.99)            
            ->setMetaTitle('test meta title 2')
            ->setMetaKeyword('test meta keyword 2')
            ->setMetaDescription('test meta description 2')            
            ->setDescription('This is a long description')
            ->setShortDescription('This is a short description')

            ->setMediaGallery (array('images'=>array (), 'values'=>array ()))
            ->addImageToMediaGallery('media/catalog/product/1/0/10243-1.png', array('image','thumbnail','small_image'), false, false)

            ->setStockData(array(
                               'use_config_manage_stock' => 0,
                               'manage_stock'=>1,
                               'min_sale_qty'=>1,
                               'max_sale_qty'=>2,
                               'is_in_stock' => 1,
                               'qty' => 999
                           )
            )

            ->setCategoryIds(array(3, 7)); 
            $product->save();
```

