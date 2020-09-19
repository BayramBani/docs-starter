# Lumen

- installation
````
composer create-project --prefer-dist laravel/lumen api-lumen
````

- serving

````
php -S localhost:8000 -t public
````

- configuration

.env
````
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=gs_database
DB_USERNAME=root
DB_PASSWORD=

CACHE_DRIVER=array
QUEUE_CONNECTION=database
````

- database migration 

````
php artisan make:migration create_tasks_table
````

database/migrations/2020_09_15_214456_create_tasks_table.php
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

- execute migration
````
php artisan migrate
````

- create model

app/Models/Task.php
````php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Task extends Model
{
    protected $table = 'tasks';

    protected $fillable = ['name'];
}

````

- use Eloquent and Fascades

bootstrap/app.php
````php
<?php
/*
|--------------------------------------------------------------------------
| Create The Application
|--------------------------------------------------------------------------
|
| Here we will load the environment and create the application instance
| that serves as the central piece of this framework. We'll use this
| application as an "IoC" container and router for this framework.
|
*/

$app = new Laravel\Lumen\Application(
    dirname(__DIR__)
);

$app->withFacades();

$app->withEloquent();
````

- create controller

app/Http/Controllers/TaskController.php
````php
<?php

namespace App\Http\Controllers;

use App\Models\Task;
use Illuminate\Http\Request;

class TaskController extends Controller
{
    public function __construct()
    {
    }

    public function index(){
        $tasks = Task::all();
        return response()->json($tasks);
    }

    public function create(Request $request){
        $task = new Task;
        $task->name = $request->name;
        $task->save();
        return response()->json($task);
    }

    public function show($id){
        $task = Task::find($id);
        return response()->json($task);
    }

    public function update(Request $request, $id){
        $task = Task::find($id);
        $task->name = $request->input('name');
        $task->save();
        return response()->json($task);
    }

    public function destroy($id){
        $task = Task::find($id);
        $task->delete();
        return response()->json('Task removed successfully');
    }
}

````

- create routes

routes/web.php
````php
<?php
$router->group(['prefix'=>'api'],function () use($router){
    $router->get('/tasks', 'taskController@index') ;
    $router->get('/task/{id}', 'taskController@show');
    $router->post('/task', 'taskController@create');
    $router->put('/task/{id}', 'taskController@update');
    $router->delete('/task/{id}', 'taskController@destroy');
});

````








