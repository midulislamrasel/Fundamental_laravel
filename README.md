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
# Paginate()
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
# simplePaginate()

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




## Laravel : Join Table

INNER JOIN ->join()
LEFT JOIN ->leftJoin()
RIGHT JOIN ->rightJoin()
CROSS JOIN ->crossJoin()

```php
DB::table('students')
->join('cities','students.city','=','cities.cid')
->get()
```



### INNER JOIN ->join()
###### StudentController File
```php
    public function showStudent()
    {
        $students = DB::table('students')
            ->join('cities', 'students.city', '=', 'cities.id')
            ->select('students.*','cities.city_name')
            ->where('students.email','=','admin@gmai.com')
            ->get();

        return view('welcome', compact('students'));
    }

```



#### Union() Method
```php
    $students = DB::table("students")


    $lecturers = DB::table("lecturers")
                ->union($students)
                ->get()
```

#### Union Method + Join Method

```php

    $lecturers = DB::table("lecturers")
                    ->select('name','email','city_name')
                    ->join('cities','lecturers.city', '=' , 'cities.id')

    $students = DB::table("students")
                ->union($students)
                ->select('name','email','city_name')
                ->get()

    return $students;
```

#### Where Method

```php

    $lecturers = DB::table("lecturers")
                    ->select('name','email','city_name')
                    ->join('cities','lecturers.city', '=' , 'cities.id')
                    ->where('city_name','=','Dhaka')

        return  $lecturers
;
```

#### When Method

```php

    $students = DB::table("students")
                   ->when(true,function($query){
                        $query->where('age','>',20)
                   })
                    ->get()

            return $students

```

```php

    $test = false
    $students = DB::table("students")
                   ->when($test,function($query){
                        $query->where('age','>',20)
                   },function($query){
                    $query->where('age','<',20)
                   })
                    ->get()

            return $students
```

#### chunk Method

```php
    $students = DB::table("students")
                   ->orderBy('id')
                   ->chunk(3,function($students){
                        foreach($students as student){
                            echo $student->name
                        }
                   });
                    ->get()

            return $students
```

### Raw SQL Queries

##### Selects
```php
$student = DB::select("select name,age from students where name =  ?", ["Rasel"])
 return $students;
```
##### insert
```php
$student = DB::insert("insert into student (name,email,age,city) values(>?,?,?,?,)",["Ram Kumar","ram@gmail.com",20,2]);
 return $students;
```


##### Update
```php
$student = DB::update("update students set email='test@gmail.com' where id = ? ", [11]);
 return $students;
```

##### Delete

```php
$student = DB::delete("delete from students  where id = ? ", [11]);
 return $students;
```


## Form Validation


##### app/Http/Controllers/FormController.php

```php 
namespace App\Http\Controllers;
      
use Illuminate\Http\Request;
use App\Models\User;
use Illuminate\View\View;
use Illuminate\Http\RedirectResponse;
     
class FormController extends Controller
{

    public function create(): View
    {
        return view('createUser');
    }
          
    public function store(Request $request): RedirectResponse
    {
        $validatedData = $request->validate([
                'name' => 'required',
                'password' => 'required|min:5',
                'email' => 'required|email|unique:users'
            ], [
                'name.required' => 'Name field is required.',
                'password.required' => 'Password field is required.',
                'email.required' => 'Email field is required.',
                'email.email' => 'Email field must be email address.'
            ]);
        
        $validatedData['password'] = bcrypt($validatedData['password']);
        $user = User::create($validatedData);
              
        return back()->with('success', 'User created successfully.');
    }
}
```



##### routes/web.php

```php
use Illuminate\Support\Facades\Route;
use App\Http\Controllers\FormController;
  
Route::get('users/create', [ FormController::class, 'create' ]);
Route::post('users/create', [ FormController::class, 'store' ])->name('users.store');
```

##### resources/views/createUser.blade.php
```php
<!DOCTYPE html>
<html>
<head>
    <title>Laravel 11 Form Validation Example - ItSolutionStuff.com</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" crossorigin="anonymous">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css" />
</head>
<body>
<div class="container">
  
    <div class="card mt-5">
        <h3 class="card-header p-3"><i class="fa fa-star"></i> Laravel 11 Form Validation Example - ItSolutionStuff.com</h3>
        <div class="card-body">
            @session('success')
                <div class="alert alert-success" role="alert"> 
                    {{ $value }}
                </div>
            @endsession
          
            <!-- Way 1: Display All Error Messages -->
            @if ($errors->any())
                <div class="alert alert-danger">
                    <strong>Whoops!</strong> There were some problems with your input.<br><br>
                    <ul>
                        @foreach ($errors->all() as $error)
                            <li>{{ $error }}</li>
                        @endforeach
                    </ul>
                </div>
            @endif
             
            <form method="POST" action="{{ route('users.store') }}">
            
                {{ csrf_field() }}
            
                <div class="mb-3">
                    <label class="form-label" for="inputName">Name:</label>
                    <input 
                        type="text" 
                        name="name" 
                        id="inputName"
                        class="form-control @error('name') is-invalid @enderror" 
                        placeholder="Name">
      
                    <!-- Way 2: Display Error Message -->
                    @error('name')
                        <span class="text-danger">{{ $message }}</span>
                    @enderror
                </div>
           
                <div class="mb-3">
                    <label class="form-label" for="inputPassword">Password:</label>
                    <input 
                        type="password" 
                        name="password" 
                        id="inputPassword"
                        class="form-control @error('password') is-invalid @enderror" 
                        placeholder="Password">
      
                    <!-- Way 3: Display Error Message -->
                    @if ($errors->has('password'))
                        <span class="text-danger">{{ $errors->first('password') }}</span>
                    @endif
                </div>
             
                <div class="mb-3">
                    <label class="form-label" for="inputEmail">Email:</label>
                    <input 
                        type="text" 
                        name="email" 
                        id="inputEmail"
                        class="form-control @error('email') is-invalid @enderror" 
                        placeholder="Email">
      
                    @error('email')
                        <span class="text-danger">{{ $message }}</span>
                    @endif
                </div>
           
                <div class="mb-3">
                    <button class="btn btn-success btn-submit"><i class="fa fa-save"></i> Submit</button>
                </div>
            </form>
        </div>
    </div>       
          
</div>
</body>
</html>
```



## Form Request Validation 

###### artisan commned
```php
php artisan make:request UserRequest
```

###### app/Http/Requests/StoreUserRequest.php:
```php
class StoreUserRequest extends FormRequest
{
    public function authorize()
    {
        return Gate::allows('user_create');
    }
 
    public function rules()
    {
        return [
            'name' => 'required',
            'email' => 'required|unique:users',
            'password' => 'required',
        ];
    }
   public function messages(){
     return[
          "username.required"=>'user Name is Required !',
          "useremail.required"=>'User Email is Required !',
          "useremail.email"=>'Enter the correct emial address!',
          ]
     }



//first error show than secend error show

protected $stopOnFirstFailure = true




//used too Larvel error message
//attributes add 
  public function attributes(){
      return [
                'username'=>'User Name',
                'useremail'=>'User Email',
                'userpassword'=>'User Password',
           ]
      }




//Used too form attributes uppercase and lowrcase
       protected function prepareForValidation():void{
                 $this->merge([
                 'username'=>strtoupper($this->username),
                 ])
             }
   
}
```

###### controllar Fille
```php
public function store(StoreUserRequest $request) 
{

 
 return $request->all();
}

```





## Custom validation  - Rule Objects
##### set 01 aritsan commnect
```php
    php aritsan make:rule Uppercase
```


##### set 02 app/Rules/Uppercase.php
```php

namespace App\Rules;
use Illuminate\Contracts\Validation\InvokableRule;


class Uppercase implements ValidationRule{
    public function validation(string $attribute, mixed $value, Closure $fail):void
    {
           if (strtoupper($value) !== $value) {
           $fail('The :attribute must be uppercase.');
       }
    }
}
```


#####  set 03 app/Http/Controllers/FormController.php

```php 
namespace App\Http\Controllers;
      
use Illuminate\Http\Request;
use App\Models\User;
use Illuminate\View\View;
use Illuminate\Http\RedirectResponse;

use App\Rules\Uppercase;
     
class FormController extends Controller
{
          
    public function store(Request $request): RedirectResponse
    {
        $validatedData = $request->validate([
                'name' => ['required',new Uppercase],
            ])
      return $req->all()
    }

}
```






## Resource Controller 

##### (stp: 01)resource controller create
```php
php artisan make:controller UserController --resource
```

###### show all route 
 ```php
php artisan route:list --name=users
```

##### (stp: 02)route file web route
```php 
use App\Http\Controllers\UserController;
use Illuminate\Support\Facades\Route;



Route::resource('users', UserController::class);


// route name change index name now alluser
//Route::resource('users', UserController::class)->names([
//   'index' => 'users.allUser',
//    'show' => 'users.view',
//]);


// only used index , store, update route show other route hide
//Route::resource('users', UserController::class)->only(
//    ['index', 'store', 'update']
//);


//// only used index', 'store hide and other route show 
//Route::resource('users', UserController::class)->except(
//    ['index', 'store']
//);

```


### Eloquent ORM


##### (step 01 ) Model and Controller file create

````php
php artisan make:model user --controller
````

###### model controller and resource
````php
php artisan make:model user --controller --resource
````

##### (step 02 )Controller add Models File
````php
namespace App\Http\Controllers;
use App\Models\user;

use Illuminate\Http\Request;

class UserController extends Controller
{
    public function show()
    {
        $users = User::all();
        return $users;
1.     }
}
````
##### (step 03 )Route File web route
````php
use App\Http\Controllers\UserController;
use Illuminate\Support\Facades\Route;


Route::get('/user',[UserController::class,'show']);

````


##### (step 04 )view Fille 
````php
<body>
        <div class="container">
            <div class="row">
                <div class="col-7">
                    <table class="table table-striped table-bordered">
                            @foreach( $users as $user)
                            <tr>
                                <td> {{$user->name}}</td>
                                <td> {{$user->email}}</td>
                                <td> {{$user->age}}</td>
                            </tr>
                            @endforeach
                    </table>
                </div>
            </div>
        </div>
</body>
````
    

##### some query
````php
$users ::where('city','goa')
        ->where('age', '>', 20)
        ->get()

//-----------//

$users ::where([
               ['city', '=' , 'Dhaka'],
               ['age', '>', 20]
           ])
        ->get()

//--------------//
$users::where('city','goa')
        ->orWhere('age', '>', 20)
        ->get()


//--------------//
$users::where('city','goa')
        ->orWhere('age', [18,20])
        ->get()


//--------------//
$users::whereIn(city',['Dilli','goa'])
        ->get()


//--------------//

$users::whereNotIn(city',['Dilli','goa'])
        ->get()


//--------------//
$users::whereNotIn('city',['Dilli','goa'])
        ->get()


//--------------//
$users::orWhereIn(city',['Dilli','goa'])
        ->get()


//--------------//
$users::whereNull(city',['Dilli','goa'])
        ->get()


//--------------//
$users::whereNotNull(city',['Dilli','goa'])
        ->get()


//--------------//
$users::whereDate('create_at','2023-06-28'])
        ->get()


//--------------//
$users::whereMonth('create_at','6'])
        ->get()


//--------------//
$users::whereMonth('create_at','6'])
        ->get()


//--------------//
$users::whereDay('create_at','26'])
        ->get()


//--------------//
$users::whereYear('create_at','2024'])
        ->get()


//--------------//
$users::whereTime('create_at','08:01:34'])
        ->get()


//-----------------------------//
if(DB::table('orders')->where('id',1)->exists()){
}

````




## RESOURCE CRUD
##### setp-1
```php
php artisan make:controller UserController --resource
```


###### route chack
```php 
php artisan route:list --name=user
```


##### setp-2 (Models File)
```php
       namespace App\Models;
       
       use Illuminate\Database\Eloquent\Factories\HasFactory;
       use Illuminate\Database\Eloquent\Model;
       
       class User extends Model
       {
           use HasFactory;
           public $timestamps = false;
       
           protected $guarded = [];
       }
```


##### setp-3 (Web Route File)
```php
      use App\Http\Controllers\UserController;
      use Illuminate\Support\Facades\Route;
      
      Route::resource('/users', UserController::class);
```

##### setp-4 (Controller File)
```php
        namespace App\Http\Controllers;
        
        use App\Models\User;
        use Illuminate\Http\Request;
        
        class UserController extends Controller
        {
        
            //=====Display a listing of the resource=======
        
            public function index()
            {
                $users = User::all();
                return view('home', compact('users'));
            }
        
            //==========Show the form for creating a new resource.========
        
            public function create()
            {
                return view('adduser');
            }
        
            //==========Store a newly created resource in storage.===========
            public function store(Request $request)
            {
                //=======Validate From=========
                $request->validate([
                    'username' => 'required|alpha',
                    'useremail' => 'required|email',
                    'userage' => 'required|numeric',
                    'usercity' => 'required|alpha',
                ]);
        
        
                //----------- FIRST METHOD --------------
                // $user = new User;
        
                // $user->name = $request->username;
                // $user->email = $request->useremail;
                // $user->age = $request->userage;
                // $user->city = $request->usercity;
        
                // $user->save();
        
        
        
                //------------- Second METHOD ---------------
                // (1 setp) Models File add ( protected $guarded = []; )
        
                User::Create([
                    'name' => $request->username,
                    'email' => $request->useremail,
                    'age' => $request->userage,
                    'city' => $request->usercity
        
                ]);
        
                return redirect()->route('users.index')->with('status', 'New User Successfully');
            }
        
            //===========Display the specified resource.=============
        
            public function show(string $id)
            {
                $users = User::find($id);
                return view('viewuser', compact('users'));
            }
        
            //============ Show the form for editing the specified resource.==========
        
            public function edit(string $id)
            {
                $users = User::find($id);
                return view('updateuser', compact('users'));
            }
        
            //===========Update the specified resource in storage.===================
        
            public function update(Request $request, string $id)
        
            {
                //=======Validate From=========
                $request->validate([
                    'username' => 'required|alpha',
                    'useremail' => 'required|email',
                    'userage' => 'required|numeric',
                    'usercity' => 'required|alpha',
                ]);
        
                //----------- FIRST METHOD --------------
                //$user = User::find($id);
        
                // $user->name = $request->username;
                // $user->email = $request->useremail;
                // $user->age = $request->userage;
                // $user->city = $request->usercity;
        
                // $user->save();
        
                //------------- Second METHOD ---------------
                $user = User::where('id', $id)
                    ->update([
                        'name' => $request->username,
                        'email' => $request->useremail,
                        'age' => $request->userage,
                        'city' => $request->usercity
                    ]);
        
                return redirect()->route('users.index')->with('status', 'Updata Successfully');
            }
        
            //=========== Remove the specified resource from storage.===============
        
            public function destroy(string $id)
            {
                $users = User::find($id);
                $users->delete();
        
                return redirect()->route('users.index')->with('status', 'Delete Successfully');
            }
        }
```



##### setp-5 (Views File)
###### layout.blade.php
```php
     <!doctype html>
     <html lang="en">
     <head>
         <meta charset="UTF-8">
         <meta name="viewport"
               content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
         <meta http-equiv="X-UA-Compatible" content="ie=edge">
         <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">
         <title>Document</title>
     </head>
     <body>
     <div class="container">
     <div class="mx-auto">
         <div class="row">
             <div class="col-12 bg-success text-center py-2">
                <h2> Eloquent CRUD</h2>
             </div>
         </div>
         <div class="row">
             <div class="col-12 bg-warning-subtle mb-3 mt-3">
                 <h4> @yield('title') </h4>
             </div>
         </div>
     
         <div class="row">
             <div class="col-12">
                 @if (session('status'))
                     <div class="alert alert-success">
                         {{session('status')}}
                     </div>
                 @endif
             </div>
         </div>
     
         <div class="row">
             <div class="col-12">
                 @yield('content')
             </div>
         </div>
     </div>
     </div>
     </body>
     </html>

```


###### home.blade.php
```php
@extends('layout')

@section('title')
All New User
@endsection


@section('content')
    <a href="{{route('users.create')}}" class="btn btn-success btn-sm mb-3">Add New</a>
    <table class="table table-striped table-bordered">
        <tr>
            <th>ID</th>
            <th>Name</th>
            <th>Email</th>
            <th>Age</th>
            <th>city</th>
            <th>View</th>
            <th>Delete</th>
            <th>Update</th>
        </tr>
        @foreach( $users as $user)
            <tr>
                <td> {{$user->id}}</td>
                <td> {{$user->name}}</td>
                <td> {{$user->email}}</td>
                <td> {{$user->age}}</td>
                <td> {{$user->city}}</td>
                
                {{-- <td><a href="{{route('user.show',$user->id )}}" class="btn btn-primary btn-sm">View</a></td>
                <td><a href="" class="btn btn-danger btn-sm">Delete</a></td>
                <td><a href="{{route('user.edit',$user->id)}}" class="btn btn-info btn-sm">Update</a></td> --}}

                <td><a href="{{route('users.show', $user->id)}}" class="btn btn-primary btn-sm">View</a></td>
                <td>
                    <form action="{{route('users.destroy',$user->id)}}" method="POST">
                        @csrf
                        @method('DELETE')
                        <button type="submit" class="btn btn-danger btn-sm">Delete</button>
                    </form>
                </td>
                <td><a href="{{route('users.edit', $user->id)}}" class="btn btn-info btn-sm">Update</a></td>
            </tr>
        @endforeach
    </table>
@endsection
```



###### view.blade.php
```php
@extends('layout')

@section('title')
  User Detail
@endsection

@section('content')
<table class="table table-striped table-bordered">
    <tr>
        <th width="80px">Name</th>
        <td>{{$users->name}}</td>
    </tr>
    <tr>
        <th>Email:</th>
        <td>{{$users->email}}</td>
    </tr>
    <tr>
        <th>Age:</th>
        <td>{{$users->age}}</td>
    </tr>
    <tr>
        <th>City:</th>
        <td>{{$users->city}}</td>
    </tr>

</table>
<a href="{{route('users.index')}}" class="btn btn-info">Back</a>

@endsection
```



###### adduser.blade.php

```php
@extends('layout')

@section('title')
    Add User
@endsection


@section('content')
    <form action="{{route('users.store')}}" method="POST">
        @csrf
        <div class="mb-3">
            <label for="username" class="form-label">User Name</label>
            <input type="text" class="form-control" name="username">
        </div>
        <div class="mb-3">
            <label for="useremail" class="form-label">User Email</label>
            <input type="text" class="form-control" name="useremail">
        </div>
        <div class="mb-3">
            <label for="userage" class="form-label">User Age</label>
            <input type="text" class="form-control" name="userage">
        </div>
        <div class="mb-3">
            <label for="usercity" class="form-label">User City</label>
            <input type="text" class="form-control" name="usercity">
        </div>
        <div class="mb-3">
            <input type="submit" value="Save" class="btn btn-success">
        </div>
    </form>
@endsection
```




###### updateuser.blade.php

```php
@extends('layout')

@section('title')
    Updata User Data
@endsection


@section('content')
    <form action="{{route('users.update',$users->id)}}" method="POST">
        @csrf
        @method('PUT')

        {{-- <pre>
            @php
                 print_r($errors->all());
            @endphp
        </pre> --}}
        <div class="mb-3">
            <label for="username" class="form-label">User Name</label>
            <input type="text" value="{{$users->name}}" class="form-control" name="username">
        </div>
        <div class="mb-3">
            <label for="useremail" class="form-label">User Email</label>
            <input type="text" value="{{$users->email}}"  class="form-control" name="useremail">
        </div>
        <div class="mb-3">
            <label for="userage" class="form-label">User Age</label>
            <input type="text" value="{{$users->age}}"  class="form-control" name="userage">
        </div>
        <div class="mb-3">
            <label for="usercity"class="form-label">User City</label>
            <input type="text" value="{{$users->city}}" class="form-control" name="usercity">
        </div>
        <div class="mb-3">
            <button class="btn btn-success" > Save</button>
            <a href="{{route('users.index')}}"  class="btn btn-info">Back</a>
        </div>
    </form>
@endsection
```

## Eloquent One To One Relationships 


##### one show one to one relationships table view
````php
Users Table
+----+----------+------------------+
| ID | Username | Email            |
+----+----------+------------------+
| 1  | john_doe | john@example.com |
+----+----------+------------------+

UserDetails Table
+--------+-------------+------------------+
|   ID   | address       |    User_ID     |
+--------+-------------+------------------+
| 1      | 123 Main St   |     1          |
+--------+-------------+------------------+
````

##### students table and contacts table studets table primary key contacts table forenkey create commnend
* #### students table to contacts table

````php
$table->foreign('Stuent_id')->references('id')->on('students');
````

````php
return $this->hasOne(Contact::class,'foreign_key','local_key');
````


#### step : 01
##### Student Controller
````php
php artisan make:controller StudentController --resource
````
##### Contact Controller
````php
php artisan make:controller ContactController 
````

#### step : 02
##### Student Model
````php
php artisan make:model Student
````
##### Contact Model
````php
php artisan make:model Contact
````

#### step : 03
##### Route create
````php
Route::resource('student',StudentController::class);
````



#### step : 04
##### Student Model File
````php
public function contact() {
    return $this->hasOne(Contact::class);        
}
````




#### step : 05
##### Student Controller File
###### import Student and contact model 

###### with used find add data
````php
    public function index() {
    $student = Student::with('contact')->get();
    return $student;
}
````


###### where used Student table condition
````php
    public function index() {
    $student = Student::with('contact')->where('gender','F')->get();
    return $student;
}
````

###### withWhereHas contact table condition and students table also condition
````php
    public function index() {
    $student = Student::withWhereHas('contact',function ($query){
        $query->where('city',"Delhi")
    })->get();
    return $student;
}
````





### Inverse Relationship 

* ##### contacts table to students table



#### step : 01
##### Contact Controller File
input model file
````php
public function show() {
    $contacts = Contact::get();
    return $contacts;    
}
````

#### Relationship student table
````php
public function show() {
    $contacts = Contact::with('student')->get();
    return $contacts;    
}
````


#### step : 02
##### Route create
````php
Route::get('/contact',[ContactController::class,'show']);
````


#### step : 03
#### contact model file
````php
public function student() {
    return $this->belongsTo(Student::class);        
}
````


## Eloquent One to Many Relationship

##### one to many relationship table used interface
````php
Departments Table
+--------+------------+
| DeptID | DeptName   |
+--------+------------+
| 1      | HR         |
| 2      | Finance    |
| 3      | IT         |
+--------+------------+

Employees Table
+--------+-------------+--------+
| EmpID  | EmpName     | DeptID |
+--------+-------------+--------+
| 1      | John Doe    | 1      |
| 2      | Jane Smith  | 1      |
| 3      | Mike Brown  | 2      |
| 4      | Emily Lee   | 3      |
| 5      | Alex Green  | 2      |
+--------+-------------+--------+
````



````php
public function contact() {
    return $this->hasMany(Contact::class);        
}
````

##### Migration create and update 
````php
php artisan make:migration create_users_table

php artisan migrate
````


##### Migration Relationship
````php
php artisan meke:migration create_users_table
Schema::create('lists', function(Blueprint $table) {
$table->increments('id');
$table->string('title', 255);
$table->integer('user_id')->unsigned();
$table->foreign('user_id')->references('id')->on('users');
$table->timestamps();
});
````



## Eloquent Many to Many Relationship
````php
Users Table          user_role Table             Roles Table

+----+------+        +---------+---------+       +----+------------+
| ID | Name |        | user_id | role_id |       | ID | Roles      |
+----+------+        +---------+---------+       +----+------------+
| 1  | John |        | 1       | 1       |       | 1  | Admin      |
| 2  | Jane |        | 1       | 2       |       | 2  | User       |
| 3  | Alex |        | 2       | 2       |       | 3  | Guest      |
| 4  | Emma |        | 3       | 3       |       | 4  | Manager    |
| 5  | Mark |        | 4       | 4       |       | 5  | Developer  |
| 6  | Sara |        | 5       | 5       |       | 6  | Tester     |
+----+------+        | 6       | 6       |       +----+------------+
                     +---------+---------+
````

##### One table used two foreign key
````php
$table->foreign('User_id')->references('id')->on('User');
$table->foreign('Role_id')->references('id')->on('Roles');
````


#### step : 01
##### all table create model file (user,role,user_role)


#### step : 02
#### contact model file->(Models/User.php)
````php
public function roles() {
    return $this->belongsToMany(Role::class, 'user_role');        
}
````

#### contact model file->(Models/Role.php)
````php
public function User() {
    return $this->belongsToMany(User::class, 'user_role');        
}
````


### step : 03
#### controller file -> (UserController.php)
##### Import User and Role Model file
````php
    user App\Model\User;
    user App\Model\Role;

    class UserController extends Controller{
        public function index(){
              $user = User::find(1)
              return $user->roles
              
    //   -------show all data in foreach method----------
    //           $users = User::get();
    //           foreach ($users as $user){
    //                echo $user->name . "<br>"
    //                echo $user->email . "<br>"
    //                
    //                foreach($users->roles as $role){
    //                    echo $role->role_name . "<br>";
    //                }
    //           }
    
            }
}
````

#### controller file -> (RoleController.php)
##### Import User and Role Model file
````php
    user App\Model\User;
    user App\Model\Role;
    class UserController extends Controller{
        public function index(){
              $user = User::find(1)
              return $user->roles
        }
}
````


### step : 04
#### Route
````php
    Route::resource('user',UserController::class);
    Route::resource('roles',RolleController::class)
````


Method
````php
Attach()
Detach()
Sync()
````

##### UserController File (used to attach method)
````php
public function create () {
    $user = User::find(2);
    $roles = [1,3];
    $user->roles()->attach($roles);
}
````



### Eloquent Has One Through Relationship

````php
Users Table
+----+------------+
| id | name       |
+----+------------+
| 1  | John       |
| 2  | Jane       |
| 3  | Mike       |
+----+------------+


Company table
+----+--------------+---------+
| id | name         | user_id |
+----+--------------+---------+
| 1  | Company A    | 1       |
| 2  | Company B    | 2       |
| 3  | Company C    | 3       |
+----+--------------+---------+


Phone_number table
+----+--------------+------------+
| id | number       | company_id |
+----+--------------+------------+
| 1  | 123-456-7890 | 1          |
| 2  | 987-654-3210 | 2          |
| 3  | 555-123-4567 | 3          |
+----+--------------+------------+
````

##### Migrations commands
````php
$table->foreign('User_id')->references('id')->on('Users');
````


### step:01 (Model file)
create users,company,phone_number models file


### step : 02
#### contact model file->(Models/User.php)
````php
public function company() {
    return $this->hasOne(company::class);        
}


public function companyPhoneNumber() {
    return $this->hasOneThrough(Phone_number::class, Company::class);        
}
````

### step:03
##### controller file -> (RoleController.php)
##### Import User and Company Model file
````php
    user App\Model\User;
    user App\Model\Company;
    class UserController extends Controller{
        public function index(){
//              $user = User::get()
//              $user = User::with("companyPhoneNumber")->find(2);
                $user = User::with('company')->with('companyPhoneNumber')->get()
//              return $user;
              
              echo $users->name ."<br>";
              echo $users->company->company_name . "<br>";
              echo $users->companyPhoneNumber->number . "<br>";
              
              
        }
}
````


### step : 04
#### Route
````php
    Route::resource('user',UserController::class);
    
````


### Eloquent Has One of Many Relationship
```php
customers Table
+----+---------+
| id | name    |
+----+---------+
| 1  | Alice   |
| 2  | Bob     |
| 3  | Charlie |
| 4  | Diana   |
+----+---------+

orders Table
+----------+--------+------------+-------------+
| order_id | amount | order_date | customer_id |
+----------+--------+------------+-------------+
| 1        | 99.99  | 2024-07-01 | 1           |
| 2        | 150.50 | 2024-07-02 | 2           |
| 3        | 200.00 | 2024-07-03 | 2           |
| 4        | 75.75  | 2024-07-04 | 3           |
| 5        | 125.25 | 2024-07-05 | 1           |
+----------+--------+------------+-------------+
```


##### Migrations commands
````php
$table->foreign('customer_id)->references('id')->on('customers');
````


### step:01 (Model file)
create Customers,Orders models file



### step : 02
#### contact model file->(Models/Customers.php)
````php
public function latestOrder() {
    return $this->hasOne(Order::class)->latestOfMany();  
    
    //   Latest Order->latestOfMany
    //   Oldest Order->oldestOfMany
    //   Largest Order->largestOfMany
    //   Smallest Order->smallestOfMany
       
}
````


### step:03
##### controller file -> (Customers.php)
##### Import orders and Customers Model file
````php
    user App\Model\User;
    user App\Model\Company;
    class UserController extends Controller{
        public function index(){
              $customers = Customer::get();
//              $customers = Customer::with("latestOrder")->find(2)    
              return $customers;
         
        }
}
````


### step : 04
#### Route
````php
    Route::resource('user',CustomerController::class);
````




## Eloquent Has Many Through Relationship

````php
Countries Table
+----+---------+
| id | name    |
+----+---------+
| 1  | USA     |
| 2  | Canada  |
| 3  | Mexico  |
| 4  | Germany |
| 5  | Japan   |
+----+---------+


Users Table
+----+---------+------------+
| id | name    | country_id |
+----+---------+------------+
| 1  | Alice   | 1          |
| 2  | Bob     | 2          |
| 3  | Charlie | 3          |
| 4  | Diana   | 1          |
| 5  | Eve     | 5          |
| 6  | Res     | 2          |
+----+---------+------------+


Post Table
+----+--------+----------------+---------+
| id | title  | detail         | user_id |
+----+--------+----------------+---------+
| 1  | Post 1 | Detail of Post 1 | 1     |
| 2  | Post 2 | Detail of Post 2 | 2     |
| 3  | Post 3 | Detail of Post 3 | 1     |
| 4  | Post 4 | Detail of Post 4 | 5     |
| 5  | Post 5 | Detail of Post 5 | 5     |
+----+--------+----------------+---------+
````



##### Migrations commands
````php
$table->foreign('country_id')->references('id')->on('Countries');
$table->foreign('user_id')->references('id')->on('Users');
````


### step:01 (Model file)
create Countries,Users,Post models file



### step : 02
#### contact model file->(Models/Countries.php)
````php
public function user() {
    return $this->hasMany(User::class);  
}

public function posts() {
    return $this->hasManyThrough(Post::class,User::class);  
}
````


#### contact model file->(Models/User.php)
````php
public function posts() {
    return $this->hasMany(Post::class);  
}

public function countries() {
    return $this->belongsTO(Countries::class);  
}
````


### step:03
##### controller file -> (Customers.php)
##### Import orders and Customers Model file
````php
    user App\Model\User;
    user App\Model\Company;
    class CustomersController extends Controller{
        public function index(){
//              $countries = Countries::with('posts')->get();
//              $countries = Countries::with('posts')->find(1);
                $countries = Countries::with('posts')->with('posts')->get(1);
                return $country->posts;
         
        }
}
````

##### controller file -> (User.php)
##### Import orders and Customers Model file
````php
    user App\Model\User;
    user App\Model\Company;
    class UserController extends Controller{
        public function index(){
//                $users = User::with('posts')->get(1);
                  $users = User::with('posts')->with('countries')->get(1);
                  return  $users;
         
        }
}
````


### step : 04
#### Route
````php
    Route::resource('countries',CountriesController::class);
    Route::resource('user',UserController::class);
    Route::resource('post',PostController::class);
````


## One to One (Polymorphic)

````php
Users Table
+----+---------+
| id | name    |
+----+---------+
| 1  | Alice   |
| 2  | Bob     |
| 3  | Charlie |
+----+---------+

Images Table
+----+----------------------------+---------------+
| id | url        | imageable_id  | imageable_type|
+----+----------------------------+---------------+
| 1  | image1.jpg | 1             | User          |
| 2  | image2.jpg | 2             | User          |
| 3  | image3.jpg | 1             | Post          |
| 4  | image4.jpg | 3             | User          |
| 5  | image5.jpg | 2             | Post          |
+----+----------------------------+---------------+

Posts Table
+----+-------------+
| id | title       |
+----+-------------+
| 1  | First Post  |
| 2  | Second Post |
| 3  | Third Post  |
+----+-------------+
````
### step:01 (Model file)
create Image,User,Post models file


### step : 02
#### contact model file->(Models/Image.php)
````php
public function imageable() {
    return $this->morphTo(User::class);  
}

````


#### contact model file->(Models/User.php)
````php
public function image() {
    return $this->morphOne(Image::class,'imageable');  
}

````

#### contact model file->(Models/Post.php)
````php
public function image() {
    return $this->morphOne(Image::class,'imageable');  
}
````


### step:03
##### controller file -> (User.php)
````php
    user App\Model\User;
    class UserController extends Controller{
        public function create(){
                $user = User::find(1);
                $user->image()->create([
                
                'url'=>'images/users/user1.jpg'
            ]); 
         
        }
}

//user,image model file open and create a protected $guarded=[]; public $timestamps = false;
//post model file open and create a protected $guarded=[];
````


##### controller file -> (Post.php)
##### Import post and Customers Model file
##### create
````php
    user App\Post\Post;
    class PostController extends Controller{
        public function create(){
         $post = Post::create([
         'title'=>"News Title One",
         'description'=>'Sldf sdfosdfn jfsodfwe sijf',      
        ])
          $post->image()->create([
          'url'=>'images/post/post-one.jpg'
        ])  
    }
}
````

##### view
````php
    user App\Post\Post;
    class PostController extends Controller{
        public function Show(){

             $post = post::with('image')->find(1);
             return $post;
         
        }
}
````

### step : 04
#### Route
````php

    Route::resource('user',UserController::class);
    Route::resource('post',PostController::class);
    Route::resource('image',ImageController::class);
````




## Eloquent One to Many(Polymorphic)

````php
Posts Table
+----+-------------+
| id | title       |
+----+-------------+
| 1  | First Post  |
| 2  | Second Post |
| 3  | Third Post  |
+----+-------------+

Videos Table
+----+-------------+------------------------+
| id | title       | url                    |
+----+-------------+------------------------+
| 1  | First Video | http://example.com/vi  |
| 2  | Second Video| http://example.com/vid |
| 3  | Third Video | http://example.com/vi  |
+----+-------------+------------------------+

Comments Table
+----+--------------------+----------------+------------------+
| id | detail             | commentable_id | commentable_type |
+----+--------------------+----------------+------------------+
| 1  | Great post!        | 1              | Post             |
| 2  | Interesting read.  | 2              | Post             |
| 3  | Nice video!        | 1              | Video            |
| 4  | Very informative.  | 2              | Video            |
| 5  | Loved the content! | 3              | Post             |
+----+--------------------+----------------+------------------+

````


### step:01 (Model file)
create Comment,Post,Video models file


### step : 02
#### contact model file->(Models/comment.php)
````php
public function commentable() {
    return $this->morphTo(User::class);  
}

````

#### contact model file->(Models/Post.php)
````php
public function comments() {
    return $this->morphMany(Comment::class,'commentable');  
}
````



#### contact model file->(Models/Video.php)
````php
public function comments() {
    return $this->morphMany(Comment::class,'commentable');  
}

````


### step:03
##### controller file -> (VideoController.php)
##### Import post and Customers Model file
````php
    class VideoController extends Controller{
        public function index(){
            $video = video::find(1);
            return $video->comments;
    }
}
````

##### controller file -> (Video.php)
##### create
````php
    class VideoController extends Controller{
        public function create(){
                $video = video::find(1);
                $video->comments()->create([
                
                'detail'=>'Best Video'
            ]); 
         
        }
}

//Comments model file open and create a protected $guarded=[]; public $timestamps = false;
//post model file open and create a protected $guarded=[];
````

### step : 04
#### Route
````php

    Route::resource('video',VideoController::class);
    Route::resource('post',PostController::class);
    Route::resource('comment',CommentController::class);
````





## Eloquent Many to Many Polymorphic

````php

Posts Table
+----+-------------+
| id | title       |
+----+-------------+
| 1  | First Post  |
| 2  | Second Post |
| 3  | Third Post  |
+----+-------------+

Tags Table
+----+--------------+
| id | name         |
+----+--------------+
| 1  | Technology   |
| 2  | Education    |
| 3  | Entertainment|
+----+--------------+

Videos Table
+----+-------------+------------------------+
| id | title       | url                    |
+----+-------------+------------------------+
| 1  | First Video | http://example./video1 |
| 2  | Second Video| http://example./video2 |
| 3  | Third Video | http://example./video3 |
+----+-------------+------------------------+

Taggables Table
+--------+--------------+----------------+
| tag_id | taggable_id  | taggable_type  |
+--------+--------------+----------------+
| 1      | 1            | Post           |
| 2      | 1            | Post           |
| 3      | 2            | Post           |
| 1      | 1            | Video          |
| 2      | 2            | Video          |
| 3      | 3            | Video          |
+--------+--------------+----------------+

````

### step:01 (Model file)
createPost,Tag,Video models file


### step : 02
#### contact model file->(Models/post.php)
````php
protected $guarder = [];
public $timestamps = false;

public function tags() {
    return $this->morphToMany(Tag::class,'taggable');  
}

````
#### contact model file->(Models/Video.php)
````php
protected $guarder = [];
public $timestamps = false;

public function tags() {
    return $this->morphToMany(Tag::class,'taggable');  
}
````

#### contact model file->(Models/tag.php)
````php
protected $guarder = [];
public $timestamps = false;

public function posts() {
    return $this->morphByMany(Poss::class,'taggable');  
}

public function videos() {
    return $this->morphByMany(Video::class,'taggable');  
}
````



### step:03
##### controller file -> (PostController.php)
##### Import post and Customers Model file
````php
    use App\Models\Post;
    class PostController extends Controller{
        public function index(){
            $post = Post::find(1);
            return $post->tags;
    }
    
    
    public function create(){
                $post = Post::create([
                'title'=>'Best Video',
                'description'=>'lorem is sums.......'
            ]); 
            
            $post->tage()->create([
                'tag_name'=>'Sachin Tendulkar'
             ])                                              
         
        }
}
````

### step : 04
#### Route
````php

    Route::resource('video',VideoController::class);
    Route::resource('post',PostController::class);
    Route::resource('tag',TagController::class);
````




## Laravel Observers & Model Events


* Creating 
* Created
* Saving
* Updating
* updated
* Deleting
* Deleted
* Restoring
* Restored
* Retrieved


### model Events
#### setp : 01
.env
```php
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=modelEvents
DB_USERNAME=root
DB_PASSWORD=
```

#### Database Data insert
##### users
```php
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL
);

INSERT INTO users (name, email) VALUES
('John Doe', 'john.doe@example.com'),
('Jane Smith', 'jane.smith@example.com'),
('Alice Johnson', 'alice.johnson@example.com'),
('Bob Brown', 'bob.brown@example.com');
```
##### Posts
```php
CREATE TABLE posts (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    slug VARCHAR(255) NOT NULL UNIQUE,
    description TEXT NOT NULL,
    counter INT DEFAULT 0,
    user_id INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);


INSERT INTO posts (title, slug, description, counter, user_id) VALUES
('First Post', 'first-post', 'This is the description for the first post.', 10, 1),
('Second Post', 'second-post', 'This is the description for the second post.', 20, 2),
('Third Post', 'third-post', 'This is the description for the third post.', 30, 3),
('Fourth Post', 'fourth-post', 'This is the description for the fourth post.', 40, 4);

```


#### setp : 02
migrations 
* users
* posts

 ##### user migrations
```php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    public function up(): void
    {
        Schema::create('users', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->string('email')->unique();
            $table->timestamps();
        });
    }

    public function down(): void
    {
        Schema::dropIfExists('users');
    }
};

```
 ##### posts migrations
```php
<?php
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    public function up(): void
    {
        Schema::create('posts', function (Blueprint $table) {
            $table->id();
            $table->string('title',50);
            $table->string('slug',50);
            $table->longText('description');
            $table->integer('content')->default(0);
            $table->unsignedBigInteger('user_id');
            $table->timestamps();
        });
    }
    public function down(): void
    {
        Schema::dropIfExists('posts');
    }
};
```

#### setp : 03 
* Seeders


#### setp : 04 Model file
* Post
* User

##### User Model
```php
<?php
namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class User extends Model
{
    use HasFactory;

    public function post(){
        return $this->hasMany(Post::class);
    }

protected static function booted() : void{
        static::deleted(function($user){
            $user->post()->delete();
        });


//    static::created(function($user){
//
//    });


//    static::updated(function($user){
//
//    });

    }
}
```


#### setp : 04 Controllers file
* PostController
* UserController


###### UserController File
```php

<?php

namespace App\Http\Controllers;

use App\Models\Post;
use App\Models\User;
use Illuminate\Http\Request;

class UserController extends Controller
{

    public function index()
    {
       $user = User::with('post')->find(2);
       return $user;

    }

    public function create()
    {
        $user = User::find(2)->delete();
    }


    public function store(Request $request)
    {
        //
    }

    public function show(string $id)
    {
        //
    }

    public function edit(string $id)
    {
        //
    }

    public function update(Request $request, string $id)
    {
        //
    }

    public function destroy(string $id)
    {
        //
    }
}
```

#### setp : 04 Routes file

```php
<?php

use App\Http\Controllers\PostController;
use App\Http\Controllers\UserController;
use Illuminate\Support\Facades\Route;

Route::get('/', function () {
    return view('welcome');
});

Route::resource('user', UserController::class);
Route::resource('post', PostController::class);
```


## Laravel Observers

#### setp : 01
 ```php
php artisan make:observer PostObserver --model=Post
php artisan make:observer UserObserver --model=User
```

#### setp : 02
Model Fille 
```php
<?php
namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class User extends Model
{
    use HasFactory;

    public function post(){
        return $this->hasMany(Post::class);
    }
}
```

#### setp : 03
### Controllers 
```php
<?php

namespace App\Http\Controllers;

use App\Models\Post;
use App\Models\User;
use Illuminate\Http\Request;

class UserController extends Controller
{

    public function index()
    {
       $user = User::with('post')->find(2);
       return $user;

    }
    public function create()
    {
        $user = User::find(2)->delete();

    }
    public function store(Request $request)
    {
        //
    }
    public function show(string $id)
    {
        //
    }
    public function edit(string $id)
    {
        //
    }
    public function update(Request $request, string $id)
    {
        //
    }
    public function destroy(string $id)
    {

    }
}

```

#### setp : 04
User Observers
```php
<?php

namespace App\Observers;
use App\Models\User;

class UserObserver
{

    public function created(User $user): void
    {
        //
    }

    public function updated(User $user): void
    {
        //
    }

    public function deleted(User $user): void
    {
        $user->post()->delete();
    }


    public function restored(User $user): void
    {
        //
    }


    public function forceDeleted(User $user): void
    {
        //
    }
}
```
#### setp : 05
#### Providers Fille -> AppServiceProvider
```php
<?php

namespace App\Providers;

use App\Models\User;
use App\Observers\UserObserver;
use Illuminate\Support\ServiceProvider;

class AppServiceProvider extends ServiceProvider
{

    public function register(): void
    {
        //
    }

    public function boot(): void
    {
        User::observe(UserObserver::class);
    }
}
```





### Image / Other File Upload

##### step: 01
```php
    <form method="POST" enctype="multipart/form-data">
        @csrf
        <imput type="file" name="photo" accept="image/*">
    </form>
```

##### step: 02
```php
$request->validate([
    'photo'=>'required|mimes:jpg,png,gif|max:300',
    
])
```


##### step: 03
* store
* storeAS
```php
$request->file('photo')->store('images');
```

## Components
#### Step : 01
```php
php artisan make:component alert
```

#### Step:02
any View Blade File

```php
<html>
    <body>
      <x-alert type="info" message="This is error messages"/>
      <x-alert type="success" message="This is Success message Alert"/>
    </body>
</html>

```


#### Step: 03
app/View/Components/alert.php

```php
<div class="alert alert-{{$type}}" role="alert">
    {{$message}}
</div>
``` 

#### Step: 04
view/components/alert.php
```php
class alert extends Component
{
    public $type;
    public $message;
    public function __construct(string $type, string $message)
    {
        $this->type = $type;
        $this->message = $message;
    }



    public function render(): View|Closure|string
    {
        return view('components.alert');
    }
}
```

### or (NOT GOOD)
##### view/components/alert.php
type and message Blade file same name so shot hand
```php
public function __construct(public string $type, public string $message){

}
```






### Authentication 
##### *  Manually Authentication with Auth Class
##### *  Session Based Authentication
##### *  Starter Kit
##### *  API Authentication

```php
php aritsan make:comonents Alert
```

#### step:01
```php
use Illuminate\Support\Facades\Auth

class UserController extends Controller{
    public function login(Request $request){
        $credentials = $request->validate([
        'email'=>'request | email',
        'password'=>'required',
]);

    if(Auth::attempt($credentials)){
       if(Auth::check()){
             return view('dashboard');
            }else{
                return redirect()->route('login')
            }
        }
    }

}
```





### Type of Middleware

####    * Route Middleware
####    * Middleware Group
####    * Global Middleware

##### * artisan commends
```php
php artisan make:middleware ValidUser
```
##### step : 01 
App/http/middleware/ValidUser.php

```php
<?php

namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Auth;use Symfony\Component\HttpFoundation\Response;

class ValidUser
{
    public function handle(Request $request, Closure $next): Response
    {
    // -------------middleware create -----------
       if(Auth::check()){
       return $next($request);
       }else{
       return redirect()->route('login')
       }
    }
}
```

##### step : 02
Routes/web.php

```php
use App\Http\Controllers\UserController;
use App\Http\Middleware\ValidUser;


Route::get('/dashboard',[UserController::class,'dashboard'])->middleware(ValidUser::class)

```




#### Sessinon







## API

### Steps to Work With APIS

#### step:01
```php
    php artisan install:api
```
#### step:02
###### Models/User.php
```php
    use Laravel\Sanctum\HasApiTokens;


    use HasApiTokens;
```


#### step:03
##### UserController File
```php
public function login( Request $request) {
    
    if(Auth::attempt(['email'=>$request->email,'password'=>$request->password])){
        return response()->json([
            'status'=>true,
            'message'=>'User logged in Successfull',
            'token'=>Autho::user()->createToken("API TOKEN")->plainTextToken,
            'token_type'=>'bearer'
            ],200)
   
    }else{
             return response()->json([
             'status'=>false,
             'message'=>'Email & Password does not match with our record.'     
        ]401)
    }
    
    
}

```

#### step:04
##### UserController File

```php
publice function logout(Reques $request){
    $user=$request->user();
    $user->tokens()->delete();
    
    
    return response()->json([
        'status'=>true,
        'user'=>$user,
        'message'=>"You Have successfully been logged",
    ],200)
}
```











 























































