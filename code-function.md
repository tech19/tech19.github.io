# code function

### safe url string

[http://cubiq.org/the-perfect-php-clean-url-generator](http://cubiq.org/the-perfect-php-clean-url-generator)

```php
/**
 * Function: sanitize
 * Returns a sanitized string, typically for URLs.
 *
 * Parameters:
 *     $string - The string to sanitize.
 *     $force_lowercase - Force the string to lowercase?
 *     $anal - If set to *true*, will remove all non-alphanumeric characters.
 */
function sanitize($string, $force_lowercase = true, $anal = false) {
    $strip = array("~", "`", "!", "@", "#", "$", "%", "^", "&", "*", "(", ")", "_", "=", "+", "[", "{", "]",
                   "}", "\\", "|", ";", ":", "\"", "'", "&#8216;", "&#8217;", "&#8220;", "&#8221;", "&#8211;", "&#8212;",
                   "â€”", "â€“", ",", "<", ".", ">", "/", "?");
    $clean = trim(str_replace($strip, "", strip_tags($string)));
    $clean = preg_replace('/\s+/', "-", $clean);
    $clean = ($anal) ? preg_replace("/[^a-zA-Z0-9]/", "", $clean) : $clean ;
    return ($force_lowercase) ?
        (function_exists('mb_strtolower')) ?
            mb_strtolower($clean, 'UTF-8') :
            strtolower($clean) :
        $clean;
}
```

### hash password

```php
// smtop: UserController.php
$hashed_password = password_hash('mypassword', PASSWORD_DEFAULT);
echo $hashed_password;
if (hash_equals($hashed_password, crypt('mypassword', $hashed_password))) {
//echo "Password verified!";}
```

### Adblock detact

Create ads.js file within var canRunAds = true;

```php
<body>
	<script>
		if(window.canRunAds === undefined){
			//adblock detected
		}
	</script>
</body>
// above not working in latest chrome
// so below
<!-- Fake js script to inject, adblockers will block this script load -->
<script
  async
  src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"
  onerror="adBlockFunction();"
></script>
// insie adBlockFunction()에
var adblocker = document.getElementById('adblock-message');
adblocker.style.display = 'block';

<div id="adblock-message" class="hidden">Sorry, you have your adblocker on!</div>

```

### responsive Email

```php
$messageBody = file_get_contents('email.html'); // inline style...
$messageBody = str_replace("##aaa##", $link, $messageBody);
$messageBody = str_replace("##bbb##", $f->sdffsdf, $messageBody);
$messageBody = str_replace("##ccc##", $f->sdfsfd, $messageBody);

$mail = new PHPMailer;
$mail->isSMTP();
$mail->SMTPDebug = 0;
$mail->Host = SMTP_HOST;
$mail->SMTPAuth = true;
$mail->Username = SMTP_USER;
$mail->Password = SMTP_PW;
$mail->setFrom($_POST['emailFrom'], $_POST['emailFromName']);
$mail->addAddress($_POST['emailTo'], $_POST['emailToName']);
$mail->isHTML(true);
$mail->Subject = $_POST['emailSubject'];
//$mail->msgHTML(file_get_contents('email.html'), dirname(__FILE__));
$mail->msgHTML($messageBody);
$error = (!$mail->send()) ? true : false;
```

### User IP

```php
if (isset($_SERVER['HTTP_CLIENT_IP']))
{
  $client_ip = $_SERVER['HTTP_CLIENT_IP'];
} else if(isset($_SERVER['HTTP_X_FORWARDED_FOR'])) {
    $client_ip = $_SERVER['HTTP_X_FORWARDED_FOR'];
} else if(isset($_SERVER['HTTP_X_FORWARDED'])) {
    $client_ip = $_SERVER['HTTP_X_FORWARDED'];
} else if(isset($_SERVER['HTTP_FORWARDED_FOR'])) {
    $client_ip = $_SERVER['HTTP_FORWARDED_FOR'];
} else if(isset($_SERVER['HTTP_FORWARDED'])) {
    $client_ip = $_SERVER['HTTP_FORWARDED'];
} else if(isset($_SERVER['REMOTE_ADDR'])) {
    $client_ip = $_SERVER['REMOTE_ADDR'];
}
```

### 한글 사이트 검사

1. EUC-KR인 경우 \
   if(preg\_match("/\[\xA1-\xFE]\[\xA1-\xFE]/", $str))\
   &#x20; echo "한글포함."; \
   else \
   &#x20; echo "한글없음";
2. UTF-8인 경우 \
   if(preg\_match("/\[\xE0-\xFF]\[\x80-\xFF]\[\x80-\xFF]/", $str))\
   &#x20; echo "한글포함."; \
   else \
   &#x20; echo "한글없음";
