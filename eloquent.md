# eloquent

### condition

* assume the **User** model stores records in the **users** table
* assume that each table has a primary key column named **id**
* updated\_at, created\_at: do not wish -> $timestamps property on your model to false
*   incrementing property on your model to false. ??

    ```php
    class User extends Model {
      protected $table = 'my_users';
      // primaryKey
    }
    ```

    **pathFor**

```php
$app->get('/ccc/{id}', '\xxxController:bbb')->setName('aaa');
// redirect with attribute
return $response->withRedirect($this->router->pathFor('aaa', ['id' => 0]));  // id is in route
```

### Select

```php
$users = User::all();  
$user = User::find(1);
// slim inside class
$user = User::query()->where(['username' => $username])->first();
```

To catch the ModelNotFoundException, add some logic to your app/Exceptions/Handler.php file.

```php
$users = User::where('votes', '>', 100)->take(10)->get();
$count = User::where('votes', '>', 100)->count();
$users = User::whereRaw('age > ? and votes = 100', [25])->get(); // **raw query
$flights = Flight::where('active', 1)->orderBy('name',
'desc')->take(10)->get();
```

Query builder: [https://laravel.com/docs/5.1/queries](https://laravel.com/docs/5.1/queries)

### Retrieving ONE Single Row / Columns From A Table

```php
$user = DB::table('users')->where('name', 'John')->first();
$email = DB::table('users')->where('name', 'John')->value('email');
// slim
// use Illuminate\Database\Capsule\Manager as Capsule; 
$user = Capsule::table('users')->where('name', 'John')->first();
$email = Capsule::table('users')->where('name', 'John')->value('email');
```

### Retrieving A List Of Column Values

If you would like to retrieve an array containing the values of a single column, you may use the lists method. In this example, we'll retrieve an array of role titles:

```php
$titles = DB::table('roles')->lists('title');
foreach ($titles as $title) {
    echo $title;
}
```

You may also specify a custom key column for the returned array: $roles = DB::table('roles')->lists('title', 'name'); foreach ($roles as $name => $title) { echo $title; }

```php
User::chunk(200, function($users){}
$user = User::on('connection-name')->find(1);
$user = User::onWriteConnection()->find(1); // read/write connection
fillable or guarded
$user = User::create(['name' => 'John']);
$user = User::firstOrCreate(['name' => 'John']);
$user = User::firstOrNew(['name' => 'John']);
$user->push(); // ?
$affectedRows = User::where('votes', '>', 100)->update(['status' => 2]);
$user->touch(); // update timestamps
```

Soft Deleting use SoftDeletes;

### Create Table For Migration: schema()

First create a new folder and name it “database”. Now, create a new file for the users table and name it “User.php”.

```php
use Illuminate\Database\Capsule\Manager as Capsule;
Capsule::schema()->create('users', function ($table) {
       $table->increments('id');
       $table->string('name');
       $table->string('email')->unique();
       $table->string('password');
       $table->string('userimage')->nullable();
       $table->string('api_key')->nullable()->unique();
       $table->rememberToken();
       $table->timestamps();
       $table->foreign('user_id')->references('id')->on('users')->onDelete('cascade');
});
```

### Using The Query Builder

Query builder: [https://laravel.com/docs/5.1/queries](https://laravel.com/docs/5.1/queries)

```php
$users = Capsule::table('users')->where('votes', '>', 100)->get();
$results = Capsule::select('select * from users where id = ?', array(1));
Capsule::schema()->create('users', function ($table) {
    $table->increments('id');
    $table->string('email')->unique();
    $table->timestamps();
});
```

### Insert

1.  save method

    ```php
    $flight = new Flight;
    $flight->name = $request->name;
    $flight->save();
    ```
2.  create method : **with fillable, guarded attribute in Model**

    ```php
    protected $fillable = ['name'];
    ...  
    $flight = Flight::create(['name' => 'Flight 10']);
    ```
3.  **firstOrCreate**, firstOrNew

    ```php
    $flight = App\Flight::firstOrCreate(['name' => 'Flight 10']);
    ```

If the model can not be found in the database, a record will be inserted with the given attributes.

```php
$flight = App\Flight::firstOrNew(['name' => 'Flight 10']);
```

if a model is not found, a new model instance will be returned. Note that the model returned by firstOrNew has not yet been persisted to the database. You will need to call **save** manually to persist it:

### Update

1.  Save method

    ```php
    $flight = new Flight;
    $flight->name = $request->name;
    $flight->save();
    ```
2.  Update method with query?

    ```php
    Flight::where('active', 1)
    ->where('destination', 'San Diego')
            ->update(['delayed' => 1]);
    ```
3. updateOrCreate

```php
// If there's a flight from Oakland to San Diego, set the price to $99.
// If no matching model exists, create one.
$flight = App\Flight::updateOrCreate(
    ['departure' => 'Oakland', 'destination' => 'San Diego'],
    ['price' => 99]
);
```

### Delete

1. Load, find and delete()
2. With primary key, don’t need find, just destroy(id)
3. With query result -> delete()

### Scope

Predefined query function

```php
/**
     * Scope a query to only include active users.
     *
     * @return \Illuminate\Database\Eloquent\Builder
     */
    public function scopeActive($query)
    {
        return $query->where('active', 1);
    }
```

How to use

```php
$users = App\User::popular()->active()->orderBy('created_at')->get();
```

### Globally with static method

ex)

```php
$capsule-\>setAsGlobal();
$users = Capsule::table('users')->where('votes', '>', 100)->get();
$results = Capsule::select('select * from users where id = ?', array(1));  //?? no select method??
Capsule::schema()->create('users', function ($table) {
    $table->increments('id');
    $table->string('email')->unique();
    $table->timestamps();
});
class User extends Illuminate\Database\Eloquent\Model {}
$users = User::where('votes', '>', 1)->get();
```

### Multiple DB

```php
$capsule->addConnection($container['settings']['db']);
$capsule->addConnection($container['settings']['db_second'], '**db_second**');

protected $connection = '**db_second**';  //or 
$capsule->getConnection('**db_second**');

$capsule->addConnection(array, $name);
$capsule->getConnection('**db_second**');
```

## Relation

### one to many

### many to many

Q. need foreign key setting in DB -> Q. delete user then 'on cascade' work automatically

> create and attach(detach) relationship in the map table

```php
$user = new \Mj\User();
$user->name = "test test";
$user->username = "test";
$user->email = "test@email.com";
$user->password = password_hash('mypassword', PASSWORD_DEFAULT);
$user->save();
// $user->id has value!!!
$user->roles()->attach(2);
```

> **Transaction**

```php
// create Model to get connection
namespace Mj;
use Illuminate\Database\Eloquent\Model as EloquentModel;

class Model extends EloquentModel
{
    public static function beginTransaction()
    {
        self::getConnectionResolver()->connection()->beginTransaction();
    }

    public static function commit()
    {
        self::getConnectionResolver()->connection()->commit();
    }

    public static function rollBack()
    {
        self::getConnectionResolver()->connection()->rollBack();
    }
}

// use
\Mj\Model::beginTransaction();
try {
    $user = new \Mj\User();
    $user->name = "test test";
    $user->username = "test";
    $user->email = "test@email.com";
    $user->password = password_hash('mypassword', PASSWORD_DEFAULT);
    $user->save();
        // $user->id has value!!!
    $user->roles()->attach(2);
    //$user->roles()->detach(2);

    \Mj\Model::commit();
} catch (Exception $e) {
        \Mj\Model::rollBack();  
}
```

### Lazy Load  :  Eager Load  :  Lazy Eager Load

```php
// n+1 query
$books = App\Book::all();
foreach ($books as $book) {
    echo $book->author->name;
}
// 2 query : with method
$books = App\Book::with('author')->get();
foreach ($books as $book) {
    echo $book->author->name;
}
// lazy eager
$books = App\Book::all();
if ($someCondition) {
    $books->load('author', 'publisher');
}
```
