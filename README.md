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
###### tables name students and create seeder name student (s) not used and mustbe used studentSeeder
```php
php artisan make:seeder StudentSeeder
```
##### (step:03)
###### tables name students and create seeder name student (s) not used and mustbe used studentSeeder
#### single data add
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

      /*--Data insert-- used create*/
        studet::created([
            'name'=>'yahoo baba',
            'email'=>'yahoo baba@gmail.com'
        ]);
    }
}
```

##### Multiple Data Ade

```php
class StudentSeeder extends Seeder
{
    public function run(): void
    {

 $student = collect(
    [
       [
       'name'=>"Midul Islam",
       'email'=>'midul@gamil.com'
       ],
       [
       'name'=>"Rasel Islam",
       'email'=>'rasel@gamil.com'
       ],
       [
       'name'=>"Aktehr Islam",
       'email'=>'aktehr@gamil.com'
       ],
       [
       'name'=>"Samiul Islam",
       'email'=>'samiul@gamil.com'
       ]
   ]
);

     $students->each(function($student){
     student::insert($studnet)
     })

    }
}

```
### JSON FILE Add
```php
/----input------/
use Illuminate\Support\Faceds\File
-----------------------------------------------

 $json = File::get(path:'Database/json/studenst');

 $studenst = collect(josn_decode($json));

 $stundents->each(function($student){
            stundents::created([
            'name'=>stundents->name
            'email'=>stundents->email
        ]);
 })
```


### Fack Data add 
```php
use App\Models\studet;
use Illuminate\Database\Console\Seeds\WithoutModelEvents;
use Illuminate\Database\Seeder;

class StudentSeeder extends Seeder
{
    public function run(): void
    {
     for($i=0; $i<10; $i){
        studet::created([
            'name'=>fake()->name(),
            'email'=>fake()->unique()->email()
        ]);
       }
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

### migrations fille fresh and seed data all comment
```php
    php artisan migrate:fresh --seed
```

#### onle run for Seeders 
```php
     db:seed --class=StudentSeeder
``









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



### mySql VS Query Bulder
```php
my SQL         -> SELECT * FROM users
Query Builder  -> DB::table('users')->get()

my SQL         -> SELECT name,city From users
Query Builder  -> DB::table('users')->select('name','city')->get()

my SQL         -> SELECT FROM User WHERE city = 'Dhaka';
Query Builder  -> DB::table('users')->where('city','=','Dhaka')->get()
Query Builder  -> DB::table('users')->where('city','=','Dhaka')->where('age','=>','19')
Query Builder  -> DB::table('users')->where('city','=','Dhaka')->orwhere('age','=>','19')

```




### Query Builder CRUD ->READ

##### (step:01)
Database create 
```php
php artisan make:migration create_users_table
```


##### (step:02)
Migrations create 
```php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    /**
     * Run the migrations.
     */
    public function up(): void
    {
        Schema::create('users', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->string('email')->unique();
            $table->string('age');
            $table->string('city');
            $table->rememberToken();
            $table->timestamps();
        });
    }

    /**
     * Reverse the migrations.
     */
    public function down(): void
    {
        Schema::dropIfExists('users');
    }
};

```

##### (step:03)
Model create
```php
php artisan make:model user
//--------------------------------------//
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class user extends Model
{
    use HasFactory;
}

```


##### (step:04)
Seeder create
```php
php artisan make:seeder UserSeeder
//----------------------------------//
namespace Database\Seeders;

use App\Models\User;
use Illuminate\Database\Console\Seeds\WithoutModelEvents;
use Illuminate\Database\Seeder;
class userSeeder extends Seeder
{
    /**
     * Run the database seeds.
     */
    public function run(): void
    {
        //
        user::created([
            'name'=>'midul',
            'email'=>'miduli@gmail.com',
            'age'=>'25',
            'city'=>'Dhaka'
        ]);
    }
}


```


##### (step:04)
Controller Create
```php
php artisan make:controller UserController
//----------------------------------------//


namespace App\Http\Controllers;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\DB;

class UserController extends Controller
{
    public function showUsers()
    {
        $users = DB::table('users')->get();
        return view('allusers', ['data' => $users]);
    }
}

```





##### (step:05)
Routes Create

```php
Route::get('/', [UserController::class,'showUsers']);


//-------Singel User Detels--------//
Route::get('/user/{id}', [UserController::class, 'singleUser'])->name('view.user');
```


##### (step:06)
View Create

```php
<table class="table table-bordered table-striped">
              <tr>
                   <th>ID</th>
                   <th>Name</th>
                   <th>Email</th>
                   <th>Age</th>
                   <th>City</th>
                   <th>View</th>
               </tr>

        @foreach( $data as $id => $user)
              <tr>
                 <td>{{$user ->id}}</td>
                 <td>{{$user ->name}}</td>
                 <td>{{$user ->email}}</td>
                 <td>{{$user ->age}}</td>
                 <td>{{$user ->city}}</td>
                 <td><a href="{{route('view.user',$user ->id)}}" class="btn btn-primary btn-sm">View</a></td>
              </tr>
       @endforeach

 </table>


//--------------singel User-----------//
@foreach($users as $id=>$user)
    <h3>Name:{{$user->name}}</h3>
    <h3>Email:{{$user->email}}</h3>
    <h3>age:{{$user->age}}</h3>
    <h3>city:{{$user->city}}</h3>
@endforeach

```



same query
```php

$users = DB::table('users')
        ->where('city','goa')
        ->where('age', '>', 20)
        ->get()

//-----------//

$users = DB::table('users')
        ->where([
               ['city', '=' , 'Dhaka'],
               ['age', '>', 20]
           ])
        ->get()

//--------------//
$users = DB::table('users')
        ->where('city','goa')
        ->orWhere('age', '>', 20)
        ->get()


//--------------//
$users = DB::table('users')
        ->where('city','goa')
        ->orWhere('age', [18,20])
        ->get()


//--------------//
$users = DB::table('users')
        ->whereIn(city',['Dilli','goa'])
        ->get()


//--------------//
$users = DB::table('users')
        ->whereNotIn(city',['Dilli','goa'])
        ->get()


//--------------//
$users = DB::table('users')
        ->whereNotIn('city',['Dilli','goa'])
        ->get()



//--------------//
$users = DB::table('users')
        ->orWhereIn(city',['Dilli','goa'])
        ->get()


//--------------//
$users = DB::table('users')
        ->whereNull(city',['Dilli','goa'])
        ->get()


//--------------//
$users = DB::table('users')
        ->whereNotNull(city',['Dilli','goa'])
        ->get()



//--------------//
$users = DB::table('users')
        ->whereDate('create_at','2023-06-28'])
        ->get()


//--------------//
$users = DB::table('users')
        ->whereMonth('create_at','6'])
        ->get()


//--------------//
$users = DB::table('users')
        ->whereMonth('create_at','6'])
        ->get()


//--------------//
$users = DB::table('users')
        ->whereDay('create_at','26'])
        ->get()


//--------------//
$users = DB::table('users')
        ->whereYear('create_at','2024'])
        ->get()


//--------------//
$users = DB::table('users')
        ->whereTime('create_at','08:01:34'])
        ->get()





//-----------------------------//
if(DB::table('orders')->where('id',1)->exists()){
  ........
}


```





### Query Builder CRUD -> CREARE , UPDATE  AND DELETE


first on controller fille add 
```php
 use illminate\Support\Facades\DB;
```

##### (Add New Record)
```php
DB::table('users')->insert([
 'name'=>'Midul Islam',
 'email'=>'midul@gamil.com'
])


/----multipul add Data-----/

DB::table('users')->insert([
[
 'name'=>'Midul Islam',
 'email'=>'midul@gamil.com'
],
[
 'name'=>'Rasel Islam',
 'email'=>'rasel@gamil.com'
]
])
```


##### inserOringore
```php
$user = DB::table('user') 
       ->insertOringore([
           'name':'Rasel',
           'email': 'rasel@gamil.com'
       ])

      if($user){
        echo "<h1> Data Successfull Added.</h1>"
      }else{
       echo "<h1> Data Not Added.</h1>"
      }
```
##### upsert
```php
$user = DB::table('user') 
       ->upsert([
           'name':'Rasel',
           'email': 'rasel@gamil.com',
           'city': 'Dhaka'
       ],
      ['email'],
      ['city']
    /----only update city -----/
      )

      if($user){
        echo "<h1> Data Successfull Added.</h1>"
      }else{
       echo "<h1> Data Not Added.</h1>"
      }
```




##### (Update)

```php
DB::table('users')
    ->where('id',1)
    ->update([
 'email'=>'midul@gamil.com'
])

```


###### updateOrInsert
```php

DB::table('users')
    ->where('id',1)
    ->updateOrInsert(
    [
     'email'=>'midul@gamil.com'
     'name'=>'midul'
    ],
    [
    'age':33
    ]
)

```

###### increment
```php
DB::table('users')
    ->where('id',1)
    ->increment('age')
     /--->increment('age',5)-----/
```


###### increment
```php
DB::table('users')
    ->where('id',1)
    ->increment('age' ['city'=>'Cox Buzzar'])
     /--->increment('age',5)-----/
```


###### incrementEach
```php
DB::table('users')
    ->where('id',1)
    ->incrementEach(
[
'age'=>3,
'vores'=>1,
]
)

```


###### decrement
```php
DB::table('users')
    ->where('id',1)
    ->decrement('age')
     /---  decrement('age',5)  -----/
```



#### (Delete) or Truncate
##### Delete
```php
DB::table('users')
   ->where('id',1)
   ->delete();
```

##### Truncate
 // delete all user and resate user id 1 
```php
DB::table('users')
   ->where('id',1)
   ->truncate();
```





#### Delete
##### (step:01)
CONTROLLER
```php
    public function deleteUser ( string $id)
    {
        $user = DB::table('users')
            ->where('id', $id)
            ->delete();

        if ($user) {
            echo "<h1>Delete Successfully</h1>";
        }else{
            echo "<h1>Delete Failed</h1>";
        }
        if($user){
            return redirect()->route('home');
        }
    }
```

##### (step:02)
ROUTE
```php
Route::get('/delete/{id}', [UserController::class, 'deleteUser'])->name('delete.user');
```

##### (step:02)
view
```php
<h2 class="text-center">All USERS LIST</h2>
                    <table class="table table-bordered table-striped">
                            <tr>
                                <th>ID</th>
                                <th>Name</th>
                                <th>View | Delete</th>
                            </tr>

                        @foreach( $data as $id => $user)
                                    <tr>
                                        <td>{{$user ->id}}</td>
                                        <td>{{$user ->name}}</td>
                                        <td>
                                            <a href="{{route('view.user',$user ->id)}}" class="btn btn-primary btn-sm">View</a>
                                            <a href="{{route('delete.user',$user ->id)}}" class="btn btn-danger btn-sm">Delete</a>
                                        </td>

                                    </tr>
                            @endforeach
                    </table>

```




<img src="https://codewolfy.com/wp-content/uploads/laravel-application-to-perform-crud-operations-1682107778qcupf-1024x569.webp" alt="">


### Controller

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Illuminate\Support\Facades\DB;

class UserController extends Controller
{

//================Show All User==============
    public function showUsers()
    {
        $users = DB::table('users')->get();
        return view('allusers', ['data' => $users]);
    }



//=============Singel User Find================
    public  function singleUser(string $id)
    {
        $users = DB::table('users')->where('id', $id)->get();
        return view('user', ['users' => $users]);
    }



//==================Inser User===================
    public function addUser(Request $req)
    {
        $user = DB::table('users')
            ->insert(
                [
                    'name' => $req->username,
                    'email' => $req->useremail,
                    'age' => $req->userage,
                    'city' => $req->usercity,
                    'remember_token' => $req->usertoken
                ]
            );

        if ($user) {
            return redirect()->route('home');
            // echo "<h1> Data Successfully</h1>";
        } else {
            echo "<h1> Data Not Add</h1>";
        }
    }




    // =========Update page================
    //---------Find Data and fild from----------
    public function updatepage(string $id)
    {
        // $users = DB::table('users')->where('id', $id)->get();
        $users = DB::table('users')->find($id);
        return view('updateuser', ['data' => $users]);
    }




    //================Update From==============
    public function update(Request $req, $id)
    {
        $user = DB::table('users')
            ->where('id', $id)
            ->update([
                'name' => $req->username,
                'email' => $req->useremail,
                'age' => $req->userage,
                'city' => $req->usercity,
                'remember_token' => $req->usertoken
            ]);

        if ($user) {
            return redirect()->route('home');
        } else {
            echo "<h1>Update Failed</h1>";
        }
    }




//================Delete======================
    public function deleteUser(string $id)
    {
        $user = DB::table('users')
            ->where('id', $id)
            ->delete();

        if ($user) {
            echo "<h1>Delete Successfully</h1>";
        } else {
            echo "<h1>Delete Failed</h1>";
        }
        if ($user) {
            return redirect()->route('home');
        }
    }
}
```



### Route
```php
<?php

use App\Http\Controllers\UserController;
use Illuminate\Support\Facades\Route;

Route::controller(UserController::class)->group(function () {

    Route::get('/', 'showUsers')->name('home');

    Route::get('/user/{id}', 'singleUser')->name('view.user');

    Route::post('/add', 'addUser')->name('addUser');

    Route::post('/update/{id}', 'update')->name('update.user');

    Route::get('/updatepage/{id}', 'updatepage')->name('update.page');

    Route::get('/delete/{id}', 'deleteUser')->name('delete.user');
});

Route::view('newuser', '/adduser');
```


### All USER
```php
        <div class="container">
            <div class="row">
                <div class="col-6">
                    <h2 class="text-center">All USERS LIST</h2>
                    <a href="/newuser" class="btn btn-success btn-sm mb-3">Add New</a>
                    <table class="table table-bordered table-striped">
                            <tr>
                                <th>ID</th>
                                <th>Name</th>
                                <th>View | Delete</th>
                            </tr>

                        @foreach( $data as $id => $user)
                                    <tr>
                                        <td>{{$user ->id}}</td>
                                        <td>{{$user ->name}}</td>
                                        <td>
                                            <a href="{{route('view.user',$user ->id)}}" class="btn btn-primary btn-sm">View</a>
                                            <a href="{{route('delete.user',$user ->id)}}" class="btn btn-danger btn-sm">Delete</a>
                                            <a href="{{route('update.page',$user ->id)}}" class="btn btn-info btn-sm">Update</a>
                                        </td>

                                    </tr>
                            @endforeach
                    </table>
                </div>
            </div>
        </div>
```


### Singel USER
```php
<h1>USER DETAIL</h1>

@foreach($users as $id=>$user)
    <h3>Name:{{$user->name}}</h3>
    <h3>Email:{{$user->email}}</h3>
    <h3>age:{{$user->age}}</h3>
    <h3>city:{{$user->city}}</h3>
@endforeach

```



### INSER USER
```php
    <div class="container">
        <div class="row">
            <div class="col-4">
                <h1>Add new user</h1>
                <form action="{{route('addUser')}}" method="POST">
                    @csrf
                    <div class="mt-3">
                        <lable class ="form-label">Name</lable>
                        <input type="text" class="form-control" name="username" id="">
                    </div>
                    <div class="mt-3">
                        <lable class ="form-label">Email</lable>
                        <input type="email" class="form-control" name="useremail" id="">
                    </div>
                    <div class="mt-3">
                        <lable class ="form-label">Age</lable>
                        <input type="number" class="form-control" name="userage" id="">
                    </div>
                    <div class="mt-3">
                        <lable class ="form-label">city</lable>
                        <input type="text" class="form-control" name="usercity" id="">
                    </div>
                    <div class="mt-3">
                        <lable class ="form-label">Token</lable>
                        <input type="text" class="form-control" name="usertoken" id="">
                    </div>
                    <button type="submit" class="btn btn-primary">Submit</button>
                </form>
            </div>
        </div>
    </div>
```



### UPDARE USER
```php
    <div class="container">
        <div class="row">
            <div class="col-4">
                <h1>Update user Data</h1>
                <form action="{{route('update.user', $data->id)}}" method="POST">
                    @csrf
                    <div class="mt-3">
                        <lable class ="form-label">Name</lable>
                        <input type="text" value="{{$data->name}}" class="form-control" name="username" id="">
                    </div>
                    <div class="mt-3">
                        <lable class ="form-label">Email</lable>
                        <input type="email" value="{{$data->email}}"  class="form-control" name="useremail" id="">
                    </div>
                    <div class="mt-3">
                        <lable class ="form-label">Age</lable>
                        <input type="number" value="{{$data->age}}" class="form-control" name="userage" id="">
                    </div>
                    <div class="mt-3">
                        <lable class ="form-label">city</lable>
                        <input type="text" value="{{$data->city}}" class="form-control" name="usercity" id="">
                    </div>
                    <div class="mt-3">
                        <lable class ="form-label">Token</lable>
                        <input type="text" value="{{$data->remember_token}}" class="form-control" name="usertoken" id="">
                    </div>
                    <button type="submit" class="btn btn-primary">Update</button>
                </form>
            </div>
        </div>
    </div>
```



<img src="https://miro.medium.com/v2/resize:fit:720/format:webp/0*ZSZITzjdvwjuIXWo.png" alt="">

### Pagination Methods
#### Paginate()
```php
DB:table('users')->paginate(5)
```

##### controller Fille
```php
        public function showUsers()
    {
        $users = DB::table('users')
            ->paginate(5)
        return view('allusers', ['data' => $users]);
    }
```

##### views/alluser
```php
<div>
{{$data->link()}}
</div>
```

##### first the way
-   First, we need to turn off the tabloid sys and then to disable bootstrap we need to make some changes to the file => app/providers/appserviceProvider

```php
use Illuminate\Pagination\Paginator;
public function boot(): void
{
    Paginator::useBootstrapFive();
    Paginator::useBootstrapFour();
}
```

##### Secend the way
```php
<div>
{{$data->link('pagination::bootstrap-5')}}
</div>
```



<!-- ======SimplePaginate========== -->
###### simplePaginate()

```php
DB::table('users')->simplePaginate(5)
```

##### controller Fille
```php
        public function showUsers()
    {
        $users = DB::table('users')
            ->simplePaginate(5)
        return view('allusers', ['data' => $users]);
    }
```

##### views/alluser
```php
<div>
{{$data->link()}}
</div>

```

----------------test--------------
```php
<div>
{{$data->link()}}
</div>

```


















