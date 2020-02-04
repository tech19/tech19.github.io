---
title: mysqliDB
categories:
  - mysql
tags:
  - mysqliDB
toc: true
---

# mysqliDB

## static instance

```text
inside function: $db = MysqliDb::getInstance();
```

## insert

* multi insert

  \`\`\`php

  $ids = $db-&gt;insertMulti\('users', $data\); //implode\(', ', $ids\);

$keys = Array\("login", "firstName", "lastName"\); $ids = $db-&gt;insertMulti\('users', $data, $keys\);

```text
- insert update with mysql data function
```

use db function: 'password' =&gt; $db-&gt;func\('SHA1\(?\)',Array \("secretpassword+salt"\)\), 'createdAt' =&gt; $db-&gt;now\(\), 'expires' =&gt; $db-&gt;now\('+1Y'\) 'editCount' =&gt; $db-&gt;inc\(2\), 'active' =&gt; $db-&gt;not\(\)

```text
- insert with on duplicate key update
```php
$data = Array ("login" => "admin",
               "firstName" => "John",
               "lastName" => 'Doe',
               "createdAt" => $db->now(),
               "updatedAt" => $db->now(),
);
$updateColumns = Array ("updatedAt");
$lastInsertId = "id";
$db->onDuplicate($updateColumns, $lastInsertId);
$id = $db->insert ('users', $data);
```

* Insert Data: .CSV or .XML data into a specific table

```php
$options = Array("fieldChar" => ';', "lineChar" => '\r\n', "linesToIgnore" => 1);
$db->loadData("users", "/home/john/file.csv", $options);

$options = Array("linesToIgnore" => 0, "rowTag"    => "<user>"):
$path_to_file = "/home/john/file.xml";
$db->loadXML("users", $path_to_file, $options);
```

## select

* select with custom columns set

  ```php
  $cols = Array ("id", "name", "email");
  $users = $db->get ("users", null, $cols);
  ```

* select just one row: getOne\(\)

  \`\`\`php

  $user = $db-&gt;getOne \("users"\);

  echo $user\['id'\];

$stats = $db-&gt;getOne \("users", "sum\(id\), count\(\*\) as cnt"\); echo "total ".$stats\['cnt'\]. "users found";

```text
- select one column value or function result
```php
$count = $db->getValue ("users", "count(*)");
```

* select one column value or function result from multiple rows

  ```php
  $logins = $db->getValue ("users", "login", 5);
  // select login from users limit 5
  foreach ($logins as $login)
    echo $login;
  ```

  **Result transformation / map**

```php
$user = $db->map ('login')->ObjectBuilder()->getOne ('users', 'id,login,createdAt');
Array
(
    [user1] => stdClass Object
        (
            [id] => 1
            [login] => user1
            [createdAt] => 2015-10-22 22:27:53
        )

)
```

## return type

```text
$json = $db->JsonBuilder()->getOne("users");
```

## raw SQL queries

```php
$users = $db->rawQuery('SELECT * from users where id >= ?', Array (10));
$user = $db->rawQueryOne ('select * from users where id=?', Array(10));
$password = $db->rawQueryValue ('select password from users where id=? limit 1', Array(10));
$logins = $db->rawQueryValue ('select login from users limit 10');
foreach ($logins as $login)
    echo $login;
```

## total count of select

```php
$offset = 10;
$count = 15;
$users = $db->withTotalCount()->get('users', Array ($offset, $count));
echo "Showing {$count} from {$db->totalCount}";
```

## query option keyword

```php
$db->setQueryOption ('FOR UPDATE')->get ('users');
// GIVES: SELECT * FROM USERS FOR UPDATE;
```

## onDuplicate   insert

```php
$data = [
    "dir_id" => $_POST['data_id'],
    "file_name" => $_FILES["instantFiles"]["name"][0],
    "file_size" => $_FILES["instantFiles"]["size"][0],  // change to KB, remove calc in list
    "created_by"  => $user->name,
    "created_at" => $db->now(),
    "last_modified_by" => $user->name,
    "last_modified_at" => $db->now()
];
$updateColumns = ["file_size", "last_modified_by", "last_modified_at"];  //** what
$lastInsertId = "file_id";  // ** with (column name)
//$lastInsertId = ["dir_id", "file_name"];
$db->onDuplicate($updateColumns, $lastInsertId);
$id = $db->insert ('aa_instant_share_file', $data);
if(!$id)
    $output = ['error' => "upload failed"];
else
    $output = ['uploaded' => 'OK'];
```

