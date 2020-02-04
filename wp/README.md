---
title: wordpress
categories:
  - wordpress
tags:
  - wordpress
toc: true
---

# wp

[**http://www.wpbeginner.com**](http://www.wpbeginner.com)

### recaptcha

_Google Captcha \(reCAPTCHA\) by BestWebSoft_

구글 reCAPTCHA API 키 발급: site key와 secret key

?????? 확인 If you add reCAPTCHA to your comments form and it doesn't show up but when you're trying to submit the comment you see the error message, then the following information can be useful.

First of all, check the browser console for errors. All errors should be fixed as they can cause the problems with reCAPTCHA work.

Our plugin uses the following hooks to display reCAPTCHA: 'comment\_form\_after\_fields' and 'comment\_form\_logged\_in\_after' that are present in the standard WordPress 'comment\_form\(\)' function.

If your theme doesn't use that function to display the comment form, you should complete the following steps:

1. Open the file with the form \(where you would like to add reCAPTCHA\);
2. Find a place to insert the code for the reCAPTCHA output;
3. Then you should add:

&lt;?php echo apply\_filters\( 'gglcptch\_display\_recaptcha', '', 'comments\_form' \); ?&gt; ??????

### recaptcha test in localhost

Site key: 6LeIxAcTAAAAAJcZVRqyHh71UMIEGNQ\_MXjiZKhI   
Secret key: 6LeIxAcTAAAAAGG-vFI1TnRWxMZNFuojJ4WifJWe

### login

### front post add \(User Submitted posts plugin\)

_? wordpress form 만들기_   
[http://www.wpbeginner.com/wp-tutorials/how-to-allow-users-to-submit-posts-to-your-wordpress-site/](http://www.wpbeginner.com/wp-tutorials/how-to-allow-users-to-submit-posts-to-your-wordpress-site/)

* no login
* registered users
* XXXX -&gt; Method 1: Front-end WordPress Post Submissions with WPForms

  1 site $49/year

  [https://wpforms.com/pricing/](https://wpforms.com/pricing/)  :: 기능참조

* OOOO -&gt; Method 2: Accept User-Generated Content with _User Submitted Posts_ Plugin

  [https://wordpress.org/plugins/user-submitted-posts/](https://wordpress.org/plugins/user-submitted-posts/)

* XXXX -&gt; Method 3: Allowing Users to Register and Submit Posts in WordPress

  create content using **WordPress admin interface** with limited capabilities

> custom user registration form in WordPress. [http://www.wpbeginner.com/plugins/how-to-create-a-custom-user-registration-form-in-wordpress/](http://www.wpbeginner.com/plugins/how-to-create-a-custom-user-registration-form-in-wordpress/)

* User Submitted posts plugin [https://wordpress.org/plugins/user-submitted-posts/\#installation](https://wordpress.org/plugins/user-submitted-posts/#installation)
  * Redirect URL: after post-submission 
  * Categories: select or hidden -&gt; hidden with cat id
  * form style change
    * copy these two plugin files: \(in plugins directory\)

      /user-submitted-posts/resources/usp.css

      /user-submitted-posts/views/submission-form.php

      into

      /wp-content/themes/your-theme/usp/usp.css

      /wp-content/themes/your-theme/usp/submission-form.php

    * change “Form style” to “Custom Form + CSS” 
  * Displaying submitted posts
    * under “Auto-Display Content” 
    * each submitted post includes a set of Custom Fields
      * `user_submit_ip` – the IP address of the submitted-post author
      * `user_submit_name` – the name of the submitted-post author
      * ...
    * [get\_post\_meta\(\)](https://codex.wordpress.org/Function_Reference/get_post_meta) 

       &lt;?php get\_post\_meta\($post\_id, '$key', $single\); ?&gt; 

       &lt;?php get\_post\_meta\($post-&gt;ID, 'post-icon', true\); ?&gt; 

    * [Helper Plugin to display Custom Fields](https://plugin-planet.com/usp-pro-custom-field-helper-plugin/). 

      It originally is designed for use with USP Pro, but also works great with the free version of USP 

### comment

default: pending status!! Publish Immediately ?????

### remove url input: functions.php in child

```php
function mko_disable_comment_url($fields) { 
    unset($fields['url']);
    return $fields;
}
add_filter('comment_form_default_fields','mko_disable_comment_url');
```

### Automatically block bad bots $25

[https://plugin-planet.com/blackhole-pro/](https://plugin-planet.com/blackhole-pro/)

### use built-in theme editor in admin area to edit functions.php file

## custom fileds

## Kboard

### display, layout change

/wp-content/plugins/kboard/skin/skin-name/....................

