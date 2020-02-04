---
title: ajax
categories:
  - ajax
tags:
  - ajax
toc: true
---

# ajax

```php
$output = [
            "success" => $result,
            "data" => $id,
            "message" => $message
];
return json_encode($output);

$.ajax({
    url: "http://127.0.0.1/news2quick2/api/AttachLogDelete",  // class
    method: "delete",
    data: {id: log_id},
    dataType: "json",
    success: function (response, status, xhr) {
        if(response.success){
        // alert("success:");
        // dataTable.row($(this).parents('tr')).remove().draw();
            dataTable.ajax.reload();
        }else{
            alert("failed:" + response.message);
        }
    }
});

$.ajax({
    type: 'POST',
    url: 'PosOrderEdit2.php',
    data: {"name" : 'ship_confirm',"value" : t,"pk" : $(this).attr('data-pk')}
})
.done(function(response){
    if(response.success){
        // alert("success:");
        // dataTable.row($(this).parents('tr')).remove().draw();
            dataTable.ajax.reload();
    }else{
        alert("failed:" + response.message);
    }
})
.fail(function(){
    console.log('Something Went Wrong ....');
})

// post
$.post('createpdfPL.php', {'data_id': c_id}, function () {
    $('#loadingDiv').hide();
    alert("success");
});

$.post("demo_test_post.asp",
{
    name: "Donald Duck",
    city: "Duckburg"
},
function(data, status){
    alert("Data: " + data + "\nStatus: " + status);
});
```

