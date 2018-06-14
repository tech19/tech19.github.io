---
title: github open source
categories: 
 - open source
tags: 
 - open source
toc: true
---

### Date Time

Carbon/Carbon

### Domain / url

Php domain parser:  jeremykendall/php-domain-parser

### Boostrap maxlength

### x-editable

success:  ß response.status == ‘error’ …

### csv

thephpleague / csv

### valitron

domain, email DNS validation

### .env

composer require vlucas/phpdotenv

```php
$dotenv = new Dotenv\Dotenv(__DIR__);
$dotenv->load();
	// call
$s3_bucket = getenv('S3_BUCKET');
$s3_bucket = $_ENV['S3_BUCKET'];
$s3_bucket = $_SERVER['S3_BUCKET'];
```

### summernote



### sweetalert2

- input validator

```javascript
	inputValidator: function (result) {
        return new Promise(function (resolve, reject) {
            if (result) {
                resolve()
            } else {
                reject('You need to write something!')
            }
        })
    },
```
- two fields

```javascript
swal({
  title: 'Multiple inputs',
  html:
    '<input id="swal-input1" class="swal2-input">' +
    '<input id="swal-input2" class="swal2-input">',
  preConfirm: function () {
    return new Promise(function (resolve) {
      resolve([
        $('#swal-input1').val(),
        $('#swal-input2').val()
      ])
    })
  },
  onOpen: function () {
    $('#swal-input1').focus()
  }
}).then(function (result) {
  swal(JSON.stringify(result))
}).catch(swal.noop)
```

- ajax

```javascript
swal({
  title: 'Submit your Github username',
  input: 'text',
  inputAttributes: {
    autocapitalize: 'off'
  },
  showCancelButton: true,
  confirmButtonText: 'Look up',
  showLoaderOnConfirm: true,
  preConfirm: (login) => {
    return fetch(`//api.github.com/users/${login}`)
      .then(response => {
        if (!response.ok) {
          throw new Error(response.statusText)
        }
        return response.json()
      })
      .catch(error => {
        swal.showValidationError(
          `Request failed: ${error}`
        )
      })
  },
  allowOutsideClick: () => !swal.isLoading()
}).then((result) => {
  if (result.value) {
    swal({
      title: `${result.value.login}'s avatar`,
      imageUrl: result.value.avatar_url
    })
  }
})

var CustomerKey = 1234;//your customer key value.
swal({
    title: "Add Note",
    input: "textarea",
    showCancelButton: true,
    confirmButtonColor: "#1FAB45",
    confirmButtonText: "Save",
    cancelButtonText: "Cancel",
    buttonsStyling: true
}).then(function () {       
    $.ajax({
        type: "POST",
        url: "YourPhpFile.php",
        data: { 'CustomerKey': CustomerKey},
        cache: false,
        success: function(response) {
            swal(
            "Sccess!",
            "Your note has been saved!",
            "success"
            )
        }
        failure: function (response) {
            swal(
            "Internal Error",
            "Oops, your note was not saved.", // had a missing comma
            "error"
            )
        }
    });
}, 
function (dismiss) {
  if (dismiss === "cancel") {
    swal(
      "Cancelled",
        "Canceled Note",
      "error"
    )
  }
})	
```
### 토스트 UI editor

