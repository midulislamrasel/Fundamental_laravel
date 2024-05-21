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

































