<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>





### Installed
##### After you have installed PHP and Composer, you may create a new Laravel project via Composer's create-project command:
```php
composer create-project laravel/laravel example-app
```

##### Or, you may create new Laravel projects by globally installing the Laravel installer via Composer:

```php
composer global require laravel/installer
 
laravel new example-app

```


##### Once the project has been created, start Laravel's local development server using Laravel Artisan's serve command:

```php
cd example-app
 
php artisan serve
```

#### VS CODE EXTENSIONS  
##### use full easy coding in Laravel

- PHP IntelliSens (Damian Cvetko)
-  PHP Namespace Resolver (Mehedi Hassan)
- Laravel Extra Instellisense (amir)
- laravel-blade (Christian Howe)
- Laravel-Blade Snippets (Winnie Lin)
- Laravel goto view (codingyu)






### Routing

##### Basic Routing

```php
use Illuminate\Support\Facades\Route;
 
Route::get('/greeting', function () {
    return 'Hello World';
});
```


##### View Routes
```php
Route::view('/welcome', 'welcome');
```


##### Route Parameters

```php
Route::get('/user/{id}', function (string $id) {
    return 'User '.$id;
});

```


##### Route Optional Parameters

```php
Route::get('/post/{id?}', function (string $id = null) {
    if ($id) {
        return "<h1> POST ID : " . $id . "</h1>";
    } else {
        return "<h1>NO ID FOUND</h1>";
    }
});
```


##### Route Multipulte Optional Parameters

```php
Route::get('/post/{id?}/comment/{commentid}', function (string $id = null, string $coommentId = null) {
    if ($id) {
        return "<h1> POST ID : " . $id . "$ comment" . $coommentId . "</h1>";
    } else {
        return "<h1>NO ID FOUND</h1>";
    }
});

```



##### Router Constraints 

- WhereNumber
- WhereAlpha
- whereAlpha
- weherAlphaNumeric
- whereIn
- where

```php
Route::get('/user/{id}', function (string $id) {
    return 'User '.$id;
})->whereNumber('id');

```

###### User Define Values
```php
Route::get('/user/{id}', function (string $id) {
    return 'User '.$id;
})->wherein('id' ,['movie','song','paomtomg']);

```


##### Router Regular Expressions

```php
Route::get('/user/{id}', function (string $id) {
    return 'User '.$id;
})->where('id' ,'[0-9]+');
```


##### Route Multipulte Optional Parameters Constraints

```php
Route::get('/post/{id?}/comment/{commentid}', function (string $id = null, string $coommentId = null) {
    if ($id) {
        return "<h1> POST ID : " . $id . "$ comment" . $coommentId . "</h1>";
    } else {
        return "<h1>NO ID FOUND</h1>";
    }
})->where('id' ,'[0-9]+')->whereAlpha('commentid');

```


##### Named Routes

```php
Route::get('test2', function () {
    return view('testPage');
})->name('mypost');


<!--- USE CODE -->

<a href="{{route('mypost')}}">About 2 page</a>
```


##### Redirect Routing
```php
Route::get('test2', function () {
    return view('test_Page');
})->name('my_post);

<---! The old route is my_post new route tes--->

Route::redirect('/my_post', '/test');
Route::redirect('/my_post', '/test' , 301);
```



#### Route Groups // Route Prefixes

```php
Route::prefix('page')->group(function () {
    Route::get('/post1/1', function () {
        return view('page1');
    });
    Route::get('/post2/1', function () {
        return view('page2');
    });
    Route::get('/post3/1', function () {
        return view('page3');
    });
});

//used path:  page/post1/1

```

#### Page Not Found

```php
Route::fallback(function(){
eturn "<h1>Page Note Found . </h1>";
})
```



### Blade Template
Template Engine Based on PHP






video 10

## Template Inheritance
```php
<body>
    <h1>This page show all Templates</h1>
    @yield('content')
</body>

-----Other page used-----
@section('content')
    <h1> This is Post Page</h1>
@endsection

```
###### @yield('content','default_parameter')


```php
@extends('layouts.master_layout)

@section('content')
    <h1> This is Post Page</h1>
@endsection
```


##### chack in a value set or not used @hasSection and @yield default page 
```php
        @hasSection('content')
            @yield('content')
        @else
            <h1>This Section No Define</h1>
        @endif
```




#### jodi kono section er pore amara kono default kichu dite chai tahole @section er pore @show thkakte hobe @section end kora jabe na

```php
@section('sidebar')
 <ul>
   <li><a href="home">Home</a></li>
   <li><a href="home">Home</a></li>
   <li><a href="home">Home</a></li>
 </ul>
@show
```

```php
@section('sidebar')
 @parent
 <p> add one pore title </p>
@endsection
```

##### asset
```php
<link rel="stylesheet" heft="{{asset('css/style.css')}}">
```



##### PHP IN JAVASCRIPT

```php
  @php
      $user = "Miudl";
  @endphp
  
  <script>
      var data = @json($user);
      console.log(data);
  </script>
```

```php
@php
    $fruits = ['Apple',' Bannana', 'Grapes', 'Orange'];
@endphp
 <script>
         var data = @json($fruits);
         data.forEach(function (entry){
            console.log(entry)
        })
 </script>
```

#### PHP IN JAVASCRIPT Othe Method 
```php
@php
    $fruits = ['Apple',' Bannana', 'Grapes', 'Orange'];
@endphp


    var data2 = {{Js::from($fruits)}};
    
    data2.forEach(function (entry){
        console.log(entry)
    })
```




### Js In Template Inheritance

```php
 @stack('scripts')

--------USED Others PAGE----------

@push('scripts')
         <script src='/example.js'></script>
@endpush

```

#### used @stack and @prepend  (Inline CSS) 

```php
 @stack('styles')

------Other pages -----

@prepend('styles') <---! kar upore ami likhte chaichi (styles CSS er upore style add korte chaichi) --->
    <style>
    #hader{
      background-color: red;
    }
    </style>
@endprepend
```



#### JavaScript Frameworks (vueJs)
```php
@verbatim
    {{user}}
@endvarbatim
```



#### ROUTE TO VIEW

```php
Route::get('/users',function (){
       $name = "Yahoo Baba";
       return view('user',['user'=>$name]);
//     return view('users')->with('user', $name)->with('city','Dhaka');
//     return view('users')->withUser($name)->withCity('Dhaka');

});


---------use fille ---------
 <h2>Hello {{$user}}</h2>

```

```php

Route::get('/users',function (){
    $name = [
        'a' => ['name'=>'Ahmed','email'=>'ahmed@gmail.com','phone'=>'01547854122','city'=>'Dhaka'],
        'b' => ['name'=>'Manik','email'=>'manik@gmail.com','phone'=>'01547854122','city'=>'NOGA'],
        'c' => ['name'=>'Ahammad','email'=>'ahammad@gmail.com','phone'=>'01547854122','city'=>'Meherpur'],
        'd' => ['name'=>'Rana','email'=>'rana@gmail.com','phone'=>'01547854122','city'=>'Khulna'],
    ];

    return view('users',[
        'user'=>$name
    ]);
});



//---------------use Fille --------


    @foreach($user as $id => $u)
        <h>{{$id}} | {{$u['name']}} | {{$u['email']}} <br> </h>
    @endforeach

```




```php
function  getUser(){
    return [
        'a' => ['name'=>'Ahmed','email'=>'ahmed@gmail.com','phone'=>'01547854122','city'=>'Dhaka'],
        'b' => ['name'=>'Manik','email'=>'manik@gmail.com','phone'=>'01547854122','city'=>'NOGA'],
        'c' => ['name'=>'Ahammad','email'=>'ahammad@gmail.com','phone'=>'01547854122','city'=>'Meherpur'],
        'd' => ['name'=>'Rana','email'=>'rana@gmail.com','phone'=>'01547854122','city'=>'Khulna'],
    ];
};

Route::get('/users',function (){
    $name = getUser();

    return view('users',[
        'user'=>$name
    ]);
});


Route::get('user/{id}',function ($id){
    $users = getUser();
    $user = $users[$id];

    return view('user',[ 'id'=>$user]);
});



```

## Controller


##### All comment used Terminal


###### All Laravel  command [options] [arguments]

```php
php artisan
```

###### controller Help File
```php
php artisan help make:controller
```
###### Controller create

```php
php artisan make:controller PageController
```



### Input Routes Folder Web.php

###### Controllers Route Filee
```php
use App\Http\Controllers\PageController;

//--------------Router------------//

Route::get('/pages',[PageController::class,'showUser']);

```



### Controllers Group -> Route

```php
Route::controller(PageController::class)->group(function(){
    Route::get('/pages','showHome');
    Route::get('/about','showAbout');
});

```

### Invokable
```php
 php artisan make:controller TestingController --invokable
```


### All Route path chack & class,method
```php
php artisan route:list --except-vendor
```


### singel Route path chack & class,method (user)
```php
php artisan route:list --path=user
```


## Database used 

### (C:01) Create a migration file
```php
php artisan make: migration create_student_table
```


### (C:02) Create Database migration
```php
php artisan migrate
```


### (C:03) Chack migrate Run
```php
php artisan migrate: status
```


### lst migrate delete
```php
php artisan migrate:rollback
```

### Specific migrate delete
second, migrate delete
```php
php artisan migrate:rollback --batch=2
```


###  migrate Reset
all remove
```php
php artisan migrate:reset
```


###  migrate Refresh
all roll back migrations and running migration
```php
php artisan migrate:refresh
```


###  migrate Fresh
Dropping all table and creating migration table
```php
php artisan migrate:fresh
```


### Model and Migrate create 
```php
php artisan make:model Test -m
```

 







## Modification with Migration

### Column Modification 
  ##### Add New Column
  ##### Rename COlumn
  ##### Delete Column
  ##### Change Column Order
  ##### Change Datatype or size of Column
  
#### Table Modification 
 ##### Rename Table
 ##### Delete Table




# add to column with Migration

### (step:01)
 ```php
 php artisan make:migration add_paid_to_users_table --table=users
```



### (step:02)
 ```php
return new class extends Migration
{

    public function up(): void
    {
        Schema::table('students', function (Blueprint $table) {
            $table->string('city')
        });
    }
}
```

### (step:03)
```php
php artisan migrate
```
===============Exta commnetd ==================
```php
$table->renameColumn('from', 'to');
```

```php
$table->dropColumn('city');
```

```php
$table->dropColumn('city', 'location'......);
```

##### one change
```php
$table->dropColumn('city',40)-change();
```

##### multipule change
```php
$table->integer('votes')->unsigned()->default(1)->comment('mycomment)->change()
```




#### constraints with Migration

  - NOT NULL         $table->string('email')->nullable()
  - UNIQUE           $table->string('email')->uniqe()
  - DEFAULT          $table->string('email')->default('Dhaka')
  - PRIMARY KEY      $table->string('email')->primary('id')
  - FOREIGN KEY      $table->string('email')->foreign('id')->references('id')->on('users')
  - CHECK           
       
    

#### Foreign Key with Cascade

```php
   $table->foreign('stu_id')->references('id')->on('students')
  -------------2------------
   $table->foreign('stu_id')->constrained('students')
```

#####  Cascade
```php
return new class extends Migration
{
   public function up(): void
    {
        Schema::create('libraries', function (Blueprint $table) {
            $table->id();
            $table->unsignedBigInteger('stu_id');
            $table->foreign('stu_id')->references('id')->on('students')
                ->onUpdate('cascade')
                ->onDelete('cascade');
            $table->string('book');
            $table->date('due_date')->nullable();
            $table->boolean('status')->default(0);
        });
    }

```

#####  Drop key constraints
```php
$table->dropPrimary('user_id_primary');
```

#####  Drop Unique
```php
$table->dropUnique('user_id_primary');
```

#####  Drop Foreign_key
```php
$table->dropForeign('user_id_primary');
/----------Other----------/
$table->dropForeign(['user_id']);
```


## Step to work in Seeder
##### (step:01)
```php
php artisan make:model student
```
##### (step:02)
```php
php artisan make:seeder StudentSeeder
```
##### (step:03)
```php
use App\Models\studet;
use Illuminate\Database\Console\Seeds\WithoutModelEvents;
use Illuminate\Database\Seeder;

class StudentSeeder extends Seeder
{
    /**
     * Run the database seeds.
     */
    public function run(): void
    {
        studet::created([
            'name'->'yahoo baba',
            'email'->'yahoo baba@gmail.com'
        ]);
    }
}
```

##### (step:04)
```php
seeders/DatabaseSeeder.php   ->(File)
//** ------------Example-------- **/
$this->call([
     StudentSeeder::class 
 ])
```

##### (step:05)
```php
 php arisan db:seed
```


## Steps to Work in Factory

##### (step:01)
```php
php arisan make:model student
```

##### (step:02)
```php
php artisan make:factory studentFactory
```

##### (step:03)
```php
class StudentFactory extends Factory {
 public function definition():array{
  return[
     'name'=>fack()->name(),
     'email'=>fack()->email()
  ];
 }
}
```

##### (step:04)
```php
Seeders/DatabaseSeeder.php -----(File)
//-----------//
 use App/Models/student;
student::factory()->count(5)->create();
```

##### (step:05)
```php
php artisan db:send
```



###  Factory and other command
```php
#1
php artisan make:factory studentFactory

#2
(Factory  & Model  )
php artisan make:factory studentFactory --model=Student

#3
(Model & Factory)
php artisan make:model student -f

#4
php artisan db:seed

#5 (Nidisto kono seeder )
php artisan db:seed --class=UserSeeder

#6 (Migration & Seeding)
php artisan migrate:fresh --seed 

```




## Steps to Work in Query Builder

##### (step:01)
create-controller
```php
php artisan make:controller UserController
```


##### (step:02)
```php
use illumiate\Support\Facades\DB

class UserController extends Controller{
 public function show(){
   $user = DB::table('users')->get();
   return $users;
 }
}
```


##### (step:03)
route-setup

```php
use App\Http\Controllers\UserController;

Route::get('/user'.[UserController::class,'show']);
```


my SQL         -> SELECT * FROM users
Query Builder  -> DB::table('users')->get()

my SQL         -> SELECT name,city From users
Query Builder  -> DB::table('users')->select('name','city')->get()

my SQL         -> SELECT FROM User WHERE city = 'Dhaka';
Query Builder  -> DB::table('users')->where('city','=','Dhaka')->get()
Query Builder  -> DB::table('users')->where('city','=','Dhaka')->where('age','=>','19')
Query Builder  -> DB::table('users')->where('city','=','Dhaka')->orwhere('age','=>','19')











































