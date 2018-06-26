---
title: validation
categories: 
 - validation
tags: 
 - validation
toc: true
---

### jquery validation

additional-methods.min.js
message_xx.min.js
```javascript
$("#record_form").validate({
    rules:{
            ot_date: {required: true},
            s_time: {required: true},
            e_time: {required: true},
            reason: {required: true},
            tasks: {required: true}
          },
    messages:
           {
            ot_date: {required: "Please select Date to Perform OT"},
            s_time: {required: "Please select Starting time"},
            e_time: {required: "Please select Est. Ending  time"},
            reason: {required: "Please enter reason"},
            tasks:{required: "Please enter tasks"}
        },
    errorPlacement : function(error, element) {
        $(element).closest('.form-group').find('.help-block').html(error.html());
    },
    highlight : function(element) {
        $(element).closest('.form-group').removeClass('has-success').addClass('has-error');
    },
    unhighlight: function(element, errorClass, validClass) {
        $(element).closest('.form-group').removeClass('has-error').addClass('has-success');
        $(element).closest('.form-group').find('.help-block').html('');
    },
    submitHandler: function(form) {
        $.ajax({
            url: "insert.php",
            method: 'POST',
            data: new FormData(form),
            contentType: false,
            dataType: 'json', 
            processData: false,
            success: function (data) {
                alert(data);
                $('#record_form')[0].reset();
                $('#recordModal').modal('hide');
                dataTable.ajax.reload();  => change to add row
            }
        });
        return false;
    }
});
```
### recaptcha validate bt4

```php
<!DOCTYPE html>
<html>
<head>
    <title>JQuery-validation demo | Bootstrap</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.0/css/bootstrap.min.css"
          integrity="sha384-9gVQ4dYFwwWSjIDZnLEWnxCjeSWFphJiwGPXr1jddIhOegiu1FwO5qRGvFXOdJZ4" crossorigin="anonymous">
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
    <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/jquery-validate/1.17.0/jquery.validate.min.js"></script>
    <script src="https://www.google.com/recaptcha/api.js" async defer></script>
</head>
<body>
<div class="container">
    <div class="row">
        <div class="col-sm-8 offset-sm-2">
            <div class="border-bottom mb-4 mt-4 pb-2">
                <div class="alert alert-info" role="alert">
                    <h6>integrate JQuery-validation and the Bootstrap 4 framework.</h6>
                </div>
            </div>
            <div class="card">
                <div class="card-header">
                    <h6 class="card-text">Simple Form</h6>
                </div>
                <div class="card-body">
                    <form id="signupForm" method="post" class="form-horizontal" action="">
                        <div class="form-group row">
                            <label class="col-sm-4 col-form-label" for="firstname">Name</label>
                            <div class="col-sm-6">
                                <input type="text" class="form-control" id="name" name="name"
                                       placeholder="Name"/>
                            </div>
                        </div>
                        <div class="alert alert-info" role="alert">
                            <h6>integrate JQuery-validation and the Bootstrap 4 framework.</h6>
                            <ul>
                                <li><a href="https://google.com/" class="alert-link">google</a>.</li>
                            </ul>
                        </div>
                        <div class="form-group row">
                            <label class="col-sm-4 col-form-label" for="username">Username</label>
                            <div class="col-sm-6">
                                <input type="text" class="form-control" id="username" name="username"
                                       placeholder="Username"/>
                            </div>
                        </div>

                        <div class="form-group row">
                            <label class="col-sm-4 col-form-label" for="email">Email</label>
                            <div class="col-sm-6">
                                <input type="text" class="form-control" id="email" name="email" placeholder="Email"/>
                            </div>
                        </div>

                        <div class="form-group row">
                            <label class="col-sm-4 col-form-label" for="password">Password</label>
                            <div class="col-sm-6">
                                <input type="password" class="form-control" id="password" name="password"
                                       placeholder="Password"/>
                            </div>
                        </div>

                        <div class="form-group row">
                            <label class="col-sm-4 col-form-label" for="confirm_password">Confirm password</label>
                            <div class="col-sm-6">
                                <input type="password" class="form-control" id="confirm_password"
                                       name="confirm_password" placeholder="Confirm password"/>
                            </div>
                        </div>

                        <div class="form-group row">
                            <div class="col-sm-6 offset-sm-4">
                                <div class="form-check">
                                    <input type="checkbox" id="agree" name="agree" value="agree"
                                           class="form-check-input"/>
                                    <label class="form-check-label">Please agree to our policy</label>
                                </div>
                            </div>
                        </div>
                        <div class="form-group row">
                            <div class="col-sm-6 offset-sm-4">
                                <div id="re" name="re" class="g-recaptcha" data-sitekey="6LeIxAcTAAAAAJcZVRqyHh71UMIEGNQ_MXjiZKhI"></div>
                                <input type="hidden" class="hiddenRecaptcha required" name="hiddenRecaptcha" id="hiddenRecaptcha">
                            </div>
                        </div>
                        <div class="form-group row">
                            <div class="col-sm-9 offset-sm-4">
                                <button type="submit" id="smbutton" class="btn btn-primary" name="signup" value="Sign up">Sign up
                                </button>
                            </div>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>
</div>
<script type="text/javascript">
    $.validator.setDefaults({
        ignore: ".ignore",
        debug: true,
        submitHandler: function () {
            alert("submitted!");
        }
    });
    $(document).ready(function () {
        var v = $("#signupForm").validate({
            rules: {
                name: "required",
                username: {
                    required: true,
                    minlength: 2
                },
                password: {
                    required: true,
                    minlength: 5
                },
                confirm_password: {
                    required: true,
                    minlength: 5,
                    equalTo: "#password"
                },
                email: {
                    required: true,
                    email: true
                },
                agree: "required",
                hiddenRecaptcha: {
                    required: function () {
                        if (grecaptcha.getResponse() == '') {
                            return true;
                        } else {
                            return false;
                        }
                    }
                }
            },
            messages: {
                name: "Please enter your name",
                username: {
                    required: "Please enter a username",
                    minlength: "Your username must consist of at least 2 characters"
                },
                password: {
                    required: "Please provide a password",
                    minlength: "Your password must be at least 5 characters long"
                },
                confirm_password: {
                    required: "Please provide a password",
                    minlength: "Your password must be at least 5 characters long",
                    equalTo: "Please enter the same password as above"
                },
                email: "Please enter a valid email address",
                agree: "Please accept our policy",
                hiddenRecaptcha: 'You must complete the antispam verification'
            },
            errorElement: "em",
            errorPlacement: function (error, element) {
                // Add the `invalid-feedback` class to the error element
                error.addClass("invalid-feedback");

                if (element.prop("type") === "checkbox") {
                    error.insertAfter(element.next("label"));
                } else {
                    error.insertAfter(element);
                }
            },
            highlight: function (element, errorClass, validClass) {
                $(element).addClass("is-invalid").removeClass("is-valid");
            },
            unhighlight: function (element, errorClass, validClass) {
                $(element).addClass("is-valid").removeClass("is-invalid");
            },
            submitHandler: function (form) {
                var submitButton = $('#smbutton');
                submitButton.prop('disabled',true);
                submitButton.text("Processing...");
                $.ajax({
                    url: '/registerProcessApi',
                    dataType: 'json',
                    type: 'post',
                    data: $(form).serialize()
                }).done(function (result) {
                    if (result.error) {
                        var fields = result.fields;
                        for (var i = 0, len = fields.length; i < len; i++) {
                            var name = fields[i].name;
                            obj = {};
                            obj[name] = fields[i].error;
                            v.showErrors(obj);
                        }
                        // $('#sendError').removeAttr('style')
                        //$('#sendError').css({ display: "block" });
                    } else {
                        window.location.replace('/');
                    }
                    submitButton.text("Sign up");
                    submitButton.prop('disabled',false);
                }).fail(function (res) {
                    //validator.showErrors({dir_name: "dir name exist"});
                });
                return false
            }
        });
        //
        // function recaptchaCallback() {
        //     $('#hiddenRecaptcha').valid();
        // };
    });

</script>
</body>
</html>
```



### Serverside: valitron



