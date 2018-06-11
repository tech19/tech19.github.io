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
### Serverside: valitron



