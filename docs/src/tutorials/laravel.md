# Laravel

## Installation

````
composer global require laravel/installer
laravel new blog
````

## Design Pattern MVC

- controller 

/app/http/Controllers

- view 

/ressources/views


- Routage (url)

/routes/web.php

- Assets (css,js,img)

/public

- Configuration 

/.env

## command
````
laravel new blog

php artisan serve
````

## Routage

/routes/web.php
````php
Route::get('/hello/{name}/{id}', function ($name,$id){
    echo 'Hello ' . $name . ' : ' .$id;
});
````
with condition
````php
Route::get('/hello/{name}/{id}', function ($name,$id){
    echo 'Hello ' . $name . ' : ' .$id;
}) ->where(['name'=> '[a-zA-Z]+' , 'id'=>'[0-9]+']);
````

## Controller

/app/http/contollers

- 1 create controller

````
php artisan make:controller TestController
````

/app/http/Controllers/TestController.php

`````
namespace App\Http\Controllers;

use Illuminate\Http\Request;

class TestController extends Controller
{
    public function contact(){
        echo 'contact controller';

    }
}
`````

/routes/web.php

`````php
Route::get('/contact', 'TestController@contact');
`````

- 2 create controller

/app/http/Controllers/TestController.php

`````php
class TestController extends Controller
{
    public function contact($name){
        echo "from contact controller : $name";

    }
}
`````

/routes/web.php
````php
Route::get('/contact/{name}', 'TestController@contact');
````

##database

- commande

'contacts' -> start with lowercase and plural (+s)

````
php artisan make:migration create_contacts_table --create=contacts
````
 - database/migration/***_create_contacts_table.php
````
public function up()
    {
        Schema::create('contacts', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->string('email');
            $table->text('message');
            $table->timestamps();
        });
    }
````

- database configuraion
.env
````
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=demo
DB_USERNAME=root
DB_PASSWORD=
````

- commande
````
php artisan migrate
````

## Model

/app/

- commande

'Contact' -> start with uppercase and singular

````
php artisan make:model Contact
````

## Controller

/app/Http/Controllers

- commande
````
php artisan make:controller ContactController
````

/app/Http/Controllers/ContactController
````
namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Contact;

class ContactController extends Controller
{
    public function newContact(){
        $contact = new Contact();

        $contact->name = "Bayram Bani";
        $contact->email = "bayram.bani@gmail.com";
        $contact->message = "Hi there !";
        
        $contact->save();
    }
}

````

- route 

/routes/web.php
````php
Route::get('/contact/', 'ContactController@newContact');
````

go to route via navigator

## demo 1

routes/web.php
```
Route::get('/contacts', 'ContactController@listContact');
```

app/Http/Controllers/ContactController.php
````php
    public function listContact(){
        $contacts = Contact::all();
        return view('contacts',['contacts'=>$contacts]);
    }
````

resources/views/contacts.blade.php
````php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Contact</title>
</head>
<body>
<pre>
    {{print_r($contacts)}}
</pre>

</body>
</html>
````

## demo 2

resources/views/contacts.blade.php
````php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Contact</title>
</head>
<body>
<h1>Contacts list</h1>

<ul>
    @foreach($contacts as $contact)
        <li>
            <h3>{{$contact->name}}</h3>
            <p>{{$contact->message}}</p>
        </li>
    @endforeach
</ul>

</body>
</html>

````

## view

-layout

ressources/views/layouts/master.blade.php

````php
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <link rel="stylesheet" href="{{asset('assets/css/bootstrap.min.css')}}">
</head>
<body>
<nav class="navbar navbar-expand-lg navbar-light bg-light">
    <a class="navbar-brand" href="#">Navbar</a>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
            <li class="nav-item active">
                <a class="nav-link" href="{{url('test')}}">Home <span class="sr-only">(current)</span></a>
            </li>
            <li class="nav-item">
                <a class="nav-link" href="{{url('service')}}">Service</a>
            </li>
            <li class="nav-item">
                <a class="nav-link" href="{{url('contact')}}">Contact</a>
            </li>
        </ul>
    </div>
</nav>
<div class="container">
    <div class="row">
        <div class="col-12">
            @yield('content')
        </div>
    </div>
</div>
<script src="{{asset('assets/js/jquery.min.js')}}"></script>
<script src="{{asset('assets/js/bootstrap.bundle.min.js')}}"></script>
</body>
</html>
````

ressources/views/test.blade.php
ressources/views/service.blade.php
ressources/views/contact.blade.php

````php
@extends('layouts.master')
@section('content')
    <h1 class="display-2">Page d'accueil</h1>
    <p>
        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc varius, purus vel commodo auctor, dui felis
        fringilla nisl, quis ullamcorper ante nunc et ligula. Aenean vehicula erat non iaculis efficitur. Praesent nisl
        nibh, aliquam vitae quam in, molestie bibendum metus. Vivamus vitae sapien sodales, congue dui id, pharetra
        odio. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia curae; Quisque cursus
        mollis urna eget sagittis. Donec libero nunc, egestas vitae finibus vel, sollicitudin elementum ante. Mauris
        suscipit dui ut tellus lobortis efficitur. Praesent et egestas lectus. Cras egestas, dolor a malesuada auctor,
        lacus nisi auctor mauris, sed egestas eros eros eu augue. Nulla iaculis feugiat diam sit amet ultrices.
        Curabitur luctus pretium pulvinar. Mauris non risus laoreet elit scelerisque posuere. Duis molestie accumsan
        fringilla. Proin vestibulum cursus mauris, vitae consequat neque rhoncus u
    </p>
@endsection
````

routes/web.php

````php
Route::view('/test','test');
Route::view('/service','service');
Route::view('/contact','contact');
````

## steps

1. create migration
2. generate table
3. generate model
4. generate controller
5. create database methods
6. create routes
7. create views

## demo

1. create model + migration

````
php artisan make:model Task -m
````

database/migrations/2020_09_18_051717_create_tasks_table.php
````php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class CreateTasksTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('tasks', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->timestamps();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists('tasks');
    }
}

````

3. generate table
````
php artisan migrate
````

4. generate controller
````
php artisan make:controller TaskController
````

app/Http/Controllers/TaskController.php
````php
<?php

namespace App\Http\Controllers;

class TaskController extends Controller
{
    // list all tasks
    public function index()
    {
    }

    // show task form
    public function create()
    {
    }

    // store task to db
    public function store()
    {
    }

    // show existing task into form
    public function edit()
    {
    }

    // update task
    public function update()
    {
    }

    // delete task
    public function destroy()
    {
    }
}

````

5. create routes

routes/web.php
````php

````
