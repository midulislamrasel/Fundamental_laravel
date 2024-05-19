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






