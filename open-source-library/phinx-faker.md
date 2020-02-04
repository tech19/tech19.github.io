---
title: PHP Library
permalink: /php-library/
toc: true
---

# phinx faker

generates fake data

{% hint style="info" %}
composer require fzaninotto/faker
{% endhint %}

{% embed url="https://github.com/fzaninotto/Faker" %}

### Phinx

{% embed url="https://book.cakephp.org/phinx/0/en/migrations.html" %}

phinx init   
phinx create MyNewMigration   
new file

change\(\) 와 up/down\(\)은 같이 있을 수 없다. up/down이 필요한경우에는 따로 파일

#### up\(\) 사용예

```php
// execute()
$count = $this->execute('DELETE FROM users'); // returns the number of affected rows

// query()
$stmt = $this->query('SELECT * FROM users'); // returns PDOStatement
$rows = $stmt->fetchAll(); // returns the result as an array
```

#### Seed

phinx seed:create UserSeeder   
phinx seed:run

```php
$faker = Faker\Factory::create();
        $data = [];
        for ($i = 0; $i < 100; $i++) {
            $data[] = [
                'username'      => $faker->userName,
                'password'      => sha1($faker->password),
                'password_salt' => sha1('foo'),
                'email'         => $faker->email,
                'first_name'    => $faker->firstName,
                'last_name'     => $faker->lastName,
                'created'       => date('Y-m-d H:i:s'),
            ];
        }

        $this->table('users')->insert($data)->saveData();
```

