$$\colorbox{pink}{\large{\color{red}{Laravel \ Framework \ Commands}}}$$

<img src="https://laravel.com/img/logomark.min.svg" alt="Loading image....." width="10%">

:link:[Home](all-file-links.md)     


<a name="top"></a>
Topic: 
#
 [Laravel Installation CMDS](#laravel-installation-cmds) 
 
 [Installing Inertia - React in Laravel Project](#laravel-intertial-react) 
 
 [Laravel 9 CRUD Example Tutorial for Beginners](#laravel9-crud) 
 
 [Laravel Breeze Inertia js CRUD with React Tutorial](#laravel-breeze-react)
  
 [Laravel 9 Vue JS CRUD App using Vite Example ](#larvel-breeze-vue)
 
 [Laravel 10 CRUD](#larvel10-crud)
 
 [Laravel 10 Select2 Ajax Autocomplete Search Example](#laravel10-autosearch)
 
#  

[Top](#top)
<a name="laravel-installation-cmds"></a>
# Laravel Installing CMDS


Composer create-project command:


    composer create-project laravel/laravel example-app


Laravel installer via Composer:

    composer global require laravel/installer

    laravel new example-app


    cd example-app
    php artisan serve


    composer create-project laravel/laravel <your-project-name>
    composer require laravel/jetstream


    Install Jetstream With Livewire
    php artisan jetstream:install livewire
    php artisan jetstream:install livewire --teams


    Install Jetstream With Inertia
    php artisan jetstream:install inertia
    php artisan jetstream:install inertia --teams


 Finalizing The Installation: 
 
    npm install
    npm run dev
    php artisan migrate


Livewire:

    php artisan vendor:publish --tag=jetstream-views




Laravel Breeze: 

    composer require laravel/breeze --dev

Breeze & Blade:

    php artisan breeze:install

    php artisan migrate
    npm install
    npm run dev

Dark Mode: 

    php artisan breeze:install --dark
 
 
Breeze & React / Vue:

    php artisan breeze:install vue

    # Or...

    php artisan breeze:install react

    php artisan migrate
    npm install
    npm run dev
 
 
 
 Server-Side Rendering:
 
    php artisan breeze:install vue --ssr
    php artisan breeze:install react --ssr
    
    
Breeze & Next.js / API:

    php artisan breeze:install api
    php artisan migrate

 
#

[Top](#top)
<a name="laravel-intertial-react"></a>
# Installing Inertia - React in Laravel Project


Step 1 - Install the Inertia package in your Laravel project

    composer require inertiajs/inertia-laravel


Step 2 - Add root template


     <!DOCTYPE html>
     <html>
         <head>
             <meta charset="utf-8" />
             <meta name="viewport" content="width=device-width, initial-scale-1.0, maximum-scale=1.0" />
             <link href="{{ mix('/css/app.css') }}" rel="stylesheet" />
             <script src="{{ mix('/js/app.js') }}" defer></script>
         </head>
         <body>
             @inertia
         </body>
     </html>



Step 3 - Setup middleware

    php artisan inertia:middleware
    
    
'web' => [
    // ...
    \App\Http\Middleware\HandleInertiaRequests::class,
],  



Step 4 - Install client-side dependencies


    npm install @inertiajs/inertia @inertiajs/inertia-react 
    yarn add @inertiajs/inertia @inertiajs/inertia-react


Step 5 - Initialize app

resources/js/app.js


    import React from "react";
    import { render } from "react-dom";
    import { createinertiaApp } from "@inertiajs/inertia-react";

    createInertiaApp({
        resolve: name => import(`.Pages/${name}`),
        setup({ el, App, props }) {
            render(<App {...props} />, el);
        }
    });


Step 6 - Install babel plugins


    npm install @babel/plugin-syntax-dynamic-import
    yarn add @babel/plugin-syntax-dynamic-import


    {
        "presets": ["@babel/preset-env", "@babel/preset-react"]
    } 


Step 7 - Create a Test.js component


resources/js/Pages

    import React from 'react';
    import { Head } from '@inertiajs/inertia-react';

    export default function Test() {
        return (
            <h1>Welcome</h1>
        )
    } 


Step 8 - Make controller and route

    <?php 

    namespace App\Http\Controllers;

    use Illuminate\Http\Request;
    use Inertia\Inertia; 

    class TestController extends Controller 
    {
        public function show() {
            return Inertia::render('Test');
        }
    }



    Route::group([
        "middleware" => ["auth"],
    ], function(){
        Route::get('/test', 'TestController@show');
    });



:end:

# 

<a name="laravel9-crud"></a>
# Laravel 9 CRUD Example Tutorial for Beginners

Use the following steps to create a crud operation app in laravel 9 as follows:

    Step 1 – Download Laravel 9 App
    Step 2 – Setup Database with App
    Step 3 – Create Company Model & Migration For CRUD App
    Step 4 – Create Company Controller By Artisan Command
    Step 5 – Create Routes
    Step 6 – Create Blade Views File
        Make Directory Name Companies
        index.blade.php
        create.blade.php
        edit.blade.php
    Step 7 – Run Laravel CRUD App on Development Server



composer create-project --prefer-dist laravel/laravel:^9.0 laravel-9-crud

Step 2 – Setup Database with App

.env

    DB_CONNECTION=mysql
    DB_HOST=127.0.0.1
    DB_PORT=3306
    DB_DATABASE=database-name
    DB_USERNAME=database-user-name
    DB_PASSWORD=database-password


Step 3 – Create Company Model & Migration For CRUD App

    php artisan make:model Company -m


public function up()
{
    Schema::create('companies', function (Blueprint $table) {
        $table->id();
        $table->string('name');
        $table->string('email');
        $table->string('address');
        $table->timestamps();
    });
}

app/Models/Company.php

    <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Factories\HasFactory;
    use Illuminate\Database\Eloquent\Model;

    class Company extends Model
    {
        use HasFactory;

        protected $fillable = ['name', 'email', 'address'];
    }
    
    php artisan migrate
    
    
Step 4 – Create Company Controller By Artisan Command   

    php artisan make:controller CompanyController
    


    <?php

    namespace App\Http\Controllers;
    use App\Models\Company;
    use Illuminate\Http\Request;

    class CompanyController extends Controller
    {
        /**
        * Display a listing of the resource.
        *
        * @return \Illuminate\Http\Response
        */
        public function index()
        {
            $companies = Company::orderBy('id','desc')->paginate(5);
            return view('companies.index', compact('companies'));
        }

        /**
        * Show the form for creating a new resource.
        *
        * @return \Illuminate\Http\Response
        */
        public function create()
        {
            return view('companies.create');
        }

        /**
        * Store a newly created resource in storage.
        *
        * @param  \Illuminate\Http\Request  $request
        * @return \Illuminate\Http\Response
        */
        public function store(Request $request)
        {
            $request->validate([
                'name' => 'required',
                'email' => 'required',
                'address' => 'required',
            ]);

            Company::create($request->post());

            return redirect()->route('companies.index')->with('success','Company has been created successfully.');
        }

        /**
        * Display the specified resource.
        *
        * @param  \App\company  $company
        * @return \Illuminate\Http\Response
        */
        public function show(Company $company)
        {
            return view('companies.show',compact('company'));
        }

        /**
        * Show the form for editing the specified resource.
        *
        * @param  \App\Company  $company
        * @return \Illuminate\Http\Response
        */
        public function edit(Company $company)
        {
            return view('companies.edit',compact('company'));
        }

        /**
        * Update the specified resource in storage.
        *
        * @param  \Illuminate\Http\Request  $request
        * @param  \App\company  $company
        * @return \Illuminate\Http\Response
        */
        public function update(Request $request, Company $company)
        {
            $request->validate([
                'name' => 'required',
                'email' => 'required',
                'address' => 'required',
            ]);

            $company->fill($request->post())->save();

            return redirect()->route('companies.index')->with('success','Company Has Been updated successfully');
        }

        /**
        * Remove the specified resource from storage.
        *
        * @param  \App\Company  $company
        * @return \Illuminate\Http\Response
        */
        public function destroy(Company $company)
        {
            $company->delete();
            return redirect()->route('companies.index')->with('success','Company has been deleted successfully');
        }
    }
    
    
Step 5 – Create Routes    
    
    use App\Http\Controllers\CompanyController;

    Route::resource('companies', CompanyController::class);    


    
Step 6 – Create Blade Views File
    
    

    Make Directory Name Companies
    index.blade.php
    create.blade.php
    edit.blade.php


index.blade.php:

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Laravel 9 CRUD Tutorial Example</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" >
</head>
<body>
    <div class="container mt-2">
        <div class="row">
            <div class="col-lg-12 margin-tb">
                <div class="pull-left">
                    <h2>Laravel 9 CRUD Example Tutorial</h2>
                </div>
                <div class="pull-right mb-2">
                    <a class="btn btn-success" href="{{ route('companies.create') }}"> Create Company</a>
                </div>
            </div>
        </div>
        @if ($message = Session::get('success'))
            <div class="alert alert-success">
                <p>{{ $message }}</p>
            </div>
        @endif
        <table class="table table-bordered">
            <thead>
                <tr>
                    <th>S.No</th>
                    <th>Company Name</th>
                    <th>Company Email</th>
                    <th>Company Address</th>
                    <th width="280px">Action</th>
                </tr>
            </thead>
            <tbody>
                @foreach ($companies as $company)
                    <tr>
                        <td>{{ $company->id }}</td>
                        <td>{{ $company->name }}</td>
                        <td>{{ $company->email }}</td>
                        <td>{{ $company->address }}</td>
                        <td>
                            <form action="{{ route('companies.destroy',$company->id) }}" method="Post">
                                <a class="btn btn-primary" href="{{ route('companies.edit',$company->id) }}">Edit</a>
                                @csrf
                                @method('DELETE')
                                <button type="submit" class="btn btn-danger">Delete</button>
                            </form>
                        </td>
                    </tr>
                    @endforeach
            </tbody>
        </table>
        {!! $companies->links() !!}
    </div>
</body>
</html>


create.blade.php:

<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Add Company Form - Laravel 9 CRUD</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
</head>

<body>
    <div class="container mt-2">
        <div class="row">
            <div class="col-lg-12 margin-tb">
                <div class="pull-left mb-2">
                    <h2>Add Company</h2>
                </div>
                <div class="pull-right">
                    <a class="btn btn-primary" href="{{ route('companies.index') }}"> Back</a>
                </div>
            </div>
        </div>
        @if(session('status'))
        <div class="alert alert-success mb-1 mt-1">
            {{ session('status') }}
        </div>
        @endif
        <form action="{{ route('companies.store') }}" method="POST" enctype="multipart/form-data">
            @csrf
            <div class="row">
                <div class="col-xs-12 col-sm-12 col-md-12">
                    <div class="form-group">
                        <strong>Company Name:</strong>
                        <input type="text" name="name" class="form-control" placeholder="Company Name">
                        @error('name')
                        <div class="alert alert-danger mt-1 mb-1">{{ $message }}</div>
                        @enderror
                    </div>
                </div>
                <div class="col-xs-12 col-sm-12 col-md-12">
                    <div class="form-group">
                        <strong>Company Email:</strong>
                        <input type="email" name="email" class="form-control" placeholder="Company Email">
                        @error('email')
                        <div class="alert alert-danger mt-1 mb-1">{{ $message }}</div>
                        @enderror
                    </div>
                </div>
                <div class="col-xs-12 col-sm-12 col-md-12">
                    <div class="form-group">
                        <strong>Company Address:</strong>
                        <input type="text" name="address" class="form-control" placeholder="Company Address">
                        @error('address')
                        <div class="alert alert-danger mt-1 mb-1">{{ $message }}</div>
                        @enderror
                    </div>
                </div>
                <button type="submit" class="btn btn-primary ml-3">Submit</button>
            </div>
        </form>
    </div>
</body>

</html>

edit.blade.php:

<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Edit Company Form - Laravel 9 CRUD Tutorial</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
</head>

<body>
    <div class="container mt-2">
        <div class="row">
            <div class="col-lg-12 margin-tb">
                <div class="pull-left">
                    <h2>Edit Company</h2>
                </div>
                <div class="pull-right">
                    <a class="btn btn-primary" href="{{ route('companies.index') }}" enctype="multipart/form-data">
                        Back</a>
                </div>
            </div>
        </div>
        @if(session('status'))
        <div class="alert alert-success mb-1 mt-1">
            {{ session('status') }}
        </div>
        @endif
        <form action="{{ route('companies.update',$company->id) }}" method="POST" enctype="multipart/form-data">
            @csrf
            @method('PUT')
            <div class="row">
                <div class="col-xs-12 col-sm-12 col-md-12">
                    <div class="form-group">
                        <strong>Company Name:</strong>
                        <input type="text" name="name" value="{{ $company->name }}" class="form-control"
                            placeholder="Company name">
                        @error('name')
                        <div class="alert alert-danger mt-1 mb-1">{{ $message }}</div>
                        @enderror
                    </div>
                </div>
                <div class="col-xs-12 col-sm-12 col-md-12">
                    <div class="form-group">
                        <strong>Company Email:</strong>
                        <input type="email" name="email" class="form-control" placeholder="Company Email"
                            value="{{ $company->email }}">
                        @error('email')
                        <div class="alert alert-danger mt-1 mb-1">{{ $message }}</div>
                        @enderror
                    </div>
                </div>
                <div class="col-xs-12 col-sm-12 col-md-12">
                    <div class="form-group">
                        <strong>Company Address:</strong>
                        <input type="text" name="address" value="{{ $company->address }}" class="form-control"
                            placeholder="Company Address">
                        @error('address')
                        <div class="alert alert-danger mt-1 mb-1">{{ $message }}</div>
                        @enderror
                    </div>
                </div>
                <button type="submit" class="btn btn-primary ml-3">Submit</button>
            </div>
        </form>
    </div>
</body>

</html>

If you submit the add or edit form blank. So the error message will be displayed with the help of the code given below:

@error('name')
    <div class="alert alert-danger mt-1 mb-1">{{ $message }}</div>
@enderror

Step 7 – Run Development Server

php artisan serve

http://127.0.0.1:8000/companies



:end:


#


<a name="laravel-breeze-react"></a>

# Laravel Breeze Inertia js CRUD with React Tutorial


Step 1: Install Laravel & Connect Database

Step 2: Install Breeze & Setup Inertia Js React

Step 3: Create Post Model and Resource Controller

Step 4: Create Post Request

Step 5: Create React js view file for CRUD



Step 1: Install Laravel & Connect Database

    composer create-project laravel/laravel inertia-react


.env

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=database_name
DB_USERNAME=database_user_name
DB_PASSWORD=database_password

Step 2: Install Breeze & Setup Inertia Js React

    composer require laravel/breeze --dev
    php artisan breeze:install
    php artisan breeze:install react
    npm install && npm run dev


Step 3: Create Post Model and Resource Controller

    php artisan make:model Post -mcr

app/database/migrations/posts_table.php


   <?php

   use Illuminate\Database\Migrations\Migration;
   use Illuminate\Database\Schema\Blueprint;
   use Illuminate\Support\Facades\Schema;

   class CreatePostsTable extends Migration
   {
       /**
        * Run the migrations.
        *
        * @return void
        */
       public function up()
       {
           Schema::create('posts', function (Blueprint $table) {
               $table->id();
               $table->string('title');
               $table->text('description');
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
           Schema::dropIfExists('posts');
       }
   }



app/Models/Post.php

    <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Factories\HasFactory;
    use Illuminate\Database\Eloquent\Model;

    class Post extends Model
    {
        protected $fillable = [
            'title',
            'description'
        ];

        use HasFactory;
    }



Step 4: Create Post Request

    php artisan make:request StorePostRequest


app/Http/Requests/StorePostRequest.php


    <?php

    namespace App\Http\Requests;

    use Illuminate\Foundation\Http\FormRequest;

    class StorePostRequest extends FormRequest
    {
        /**
         * Determine if the user is authorized to make this request.
         *
         * @return bool
         */
        public function authorize()
        {
            return true;
        }

        /**
         * Get the validation rules that apply to the request.
         *
         * @return array
         */
        public function rules()
        {
            return [
                'title' => 'required',
                'description' => 'required'
            ];
        }
    }


PostController.php

    <?php

    namespace App\Http\Controllers;

    use App\Http\Requests\StorePostRequest;
    use App\Models\Post;
    use Illuminate\Support\Facades\Redirect;
    use Illuminate\Support\Facades\Request;
    use Inertia\Inertia;

    class PostController extends Controller
    {
        /**
         * Display a listing of the resource.
         *
         * @return \Illuminate\Http\Response
         */
        public function index()
        {
            $posts = Post::latest()->get();

            return Inertia::render('Post/Index', ['posts' => $posts]);
        }

        /**
         * Show the form for creating a new resource.
         *
         * @return \Illuminate\Http\Response
         */
        public function create()
        {
            return Inertia::render('Post/Create');
        }

        /**
         * Store a newly created resource in storage.
         *
         * @param  \Illuminate\Http\Request  $request
         * @return \Illuminate\Http\Response
         */
        public function store(StorePostRequest $request)
        {
            Post::create(
                $request->validated()
            );

            return Redirect::route('posts.index');
        }

        /**
         * Display the specified resource.
         *
         * @param  int  $id
         * @return \Illuminate\Http\Response
         */
        public function show($id)
        {
            //
        }

        /**
         * Show the form for editing the specified resource.
         *
         * @param  int  $id
         * @return \Illuminate\Http\Response
         */
        public function edit(Post $post)
        {
            return Inertia::render('Post/Edit', [
                'post' => [
                    'id' => $post->id,
                    'title' => $post->title,
                    'description' => $post->description
                ]
            ]);
        }

        /**
         * Update the specified resource in storage.
         *
         * @param  \Illuminate\Http\Request  $request
         * @param  int  $id
         * @return \Illuminate\Http\Response
         */
        public function update(StorePostRequest $request, Post $post)
        {
            $post->update($request->validated());

            return Redirect::route('posts.index');
        }

        /**
         * Remove the specified resource from storage.
         *
         * @param  int  $id
         * @return \Illuminate\Http\Response
         */
        public function destroy(Post $post)
        {
            $post->delete();

            return Redirect::route('posts.index');
        }
    }


app/routes/web.php

    <?php

    use App\Http\Controllers\PostController;
    use Illuminate\Foundation\Application;
    use Illuminate\Support\Facades\Route;
    use Inertia\Inertia;

    /*
    |--------------------------------------------------------------------------
    | Web Routes
    |--------------------------------------------------------------------------
    |
    | Here is where you can register web routes for your application. These
    | routes are loaded by the RouteServiceProvider within a group which
    | contains the "web" middleware group. Now create something great!
    |
    */

    Route::get('/', function () {
        return Inertia::render('Welcome', [
            'canLogin' => Route::has('login'),
            'canRegister' => Route::has('register'),
            'laravelVersion' => Application::VERSION,
            'phpVersion' => PHP_VERSION,
        ]);
    });

    Route::get('/dashboard', function () {
        return Inertia::render('Dashboard');
    })->middleware(['auth', 'verified'])->name('dashboard');

    Route::resource('posts', PostController::class);
    require __DIR__.'/auth.php';


Step 5: Create React js view file for CRUD

app/resources/js/Pages/Post/Create.js

    import React from "react";
    import { Inertia } from "@inertiajs/inertia";
    import { InertiaLink, useForm } from "@inertiajs/inertia-react";

    const Create = () => {
        const { data, setData, errors, post } = useForm({
            title: "",
            description: "",
        });

        function handleSubmit(e) {
            e.preventDefault();
            post(route("posts.store"));
        }

        return (
            <div className="mt-20">
                <div className="container flex flex-col justify-center mx-auto">
                    <div>
                        <h1 className="mb-8 text-3xl font-bold">
                            <InertiaLink
                                href={route("posts.index")}
                                className="text-indigo-600 hover:text-indigo-700"
                            >
                                Posts
                            </InertiaLink>
                            <span className="font-medium text-indigo-600"> / </span>
                            Create
                        </h1>
                    </div>
                    <div className="max-w-6xl p-8 bg-white rounded shadow">
                        <form name="createForm" onSubmit={handleSubmit}>
                            <div className="flex flex-col">
                                <div className="mb-4">
                                    <label className="">Title</label>
                                    <input
                                        type="text"
                                        className="w-full px-4 py-2"
                                        label="Title"
                                        name="title"
                                        value={data.title}
                                        onChange={(e) =>
                                            setData("title", e.target.value)
                                        }
                                    />
                                    <span className="text-red-600">
                                        {errors.title}
                                    </span>
                                </div>
                                <div className="mb-0">
                                    <label className="">Description</label>
                                    <textarea
                                        type="text"
                                        className="w-full rounded"
                                        label="description"
                                        name="description"
                                        errors={errors.description}
                                        value={data.description}
                                        onChange={(e) =>
                                            setData("description", e.target.value)
                                        }
                                    />
                                    <span className="text-red-600">
                                        {errors.description}
                                    </span>
                                </div>
                            </div>
                            <div className="mt-4">
                                <button
                                    type="submit"
                                    className="px-6 py-2 font-bold text-white bg-green-500 rounded"
                                >
                                    Save
                                </button>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        );
    };

    export default Create;



app/resources/js/Pages/Post/Index.js

    import React from "react";
    import { Inertia } from "@inertiajs/inertia";
    import { InertiaLink, usePage } from "@inertiajs/inertia-react";

    const Index = () => {
        const { posts } = usePage().props;
        const { data } = posts;

        return (
            <div>
                <div className="container mx-auto">
                    <h1 className="mb-8 text-3xl font-bold text-center">Post</h1>
                    <div className="flex items-center justify-between mb-6">
                        <InertiaLink
                            className="px-6 py-2 text-white bg-green-500 rounded-md focus:outline-none"
                            href={route("posts.create")}
                        >
                            Create Post
                        </InertiaLink>
                    </div>

                    <div className="overflow-x-auto bg-white rounded shadow">
                        <table className="w-full whitespace-nowrap">
                            <thead className="text-white bg-gray-600">
                                <tr className="font-bold text-left">
                                    <th className="px-6 pt-5 pb-4">#</th>
                                    <th className="px-6 pt-5 pb-4">Title</th>
                                    <th className="px-6 pt-5 pb-4">Description</th>
                                    <th className="px-6 pt-5 pb-4">Action</th>
                                </tr>
                            </thead>
                            <tbody>
                                {data.map(({ id, title, description }) => (
                                    <tr key={id} className="">
                                        <td className="border-t">
                                            <InertiaLink
                                                href={route("posts.edit", id)}
                                                className="flex items-center px-6 py-4 focus:text-indigo-700 focus:outline-none"
                                            >
                                                {id}
                                            </InertiaLink>
                                        </td>
                                        <td className="border-t">
                                            <InertiaLink
                                                href={route("posts.edit", id)}
                                                className="flex items-center px-6 py-4 focus:text-indigo-700 focus:outline-none"
                                            >
                                                {title}
                                            </InertiaLink>
                                        </td>
                                        <td className="border-t">
                                            <InertiaLink
                                                tabIndex="1"
                                                className="flex items-center px-6 py-4"
                                                href={route("posts.edit", id)}
                                            >
                                                {description}
                                            </InertiaLink>
                                        </td>
                                        <td className="border-t">
                                            <InertiaLink
                                                tabIndex="1"
                                                className="px-4 py-2 text-sm text-white bg-blue-500 rounded"
                                                href={route("posts.edit", id)}
                                            >
                                                Edit
                                            </InertiaLink>
                                        </td>
                                    </tr>
                                ))}
                                {data.length === 0 && (
                                    <tr>
                                        <td
                                            className="px-6 py-4 border-t"
                                            colSpan="4"
                                        >
                                            No contacts found.
                                        </td>
                                    </tr>
                                )}
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        );
    };

    export default Index;



app/resources/js/Pages/Post/Edit.js

    import React from "react";
    import { Inertia } from "@inertiajs/inertia";
    import { InertiaLink, usePage, useForm } from "@inertiajs/inertia-react";

    const Edit = () => {
        const { post } = usePage().props;
        const { data, setData, put, errors } = useForm({
            title: post.title || "",
            description: post.description || "",
        });

        function handleSubmit(e) {
            e.preventDefault();
            put(route("posts.update", post.id));
        }
        function destroy() {
            if (confirm("Are you sure you want to delete this user?")) {
                Inertia.delete(route("posts.destroy", post.id));
            }
        }

        return (
            <div className="mt-20">
                <div className="container flex flex-col justify-center mx-auto">
                    <div>
                        <h1 className="mb-8 text-3xl font-bold">
                            <InertiaLink
                                href={route("posts.index")}
                                className="text-indigo-600 hover:text-indigo-700"
                            >
                                Posts
                            </InertiaLink>
                            <span className="font-medium text-indigo-600"> /</span>
                            Edit
                        </h1>
                    </div>
                    <div className="max-w-3xl p-8 bg-white rounded shadow">
                        <form name="createForm" onSubmit={handleSubmit}>
                            <div className="flex flex-col">
                                <div className="mb-4">
                                    <label className="">Title</label>
                                    <input
                                        type="text"
                                        className="w-full px-4 py-2"
                                        label="Title"
                                        name="title"
                                        value={data.title}
                                        onChange={(e) =>
                                            setData("title", e.target.value)
                                        }
                                    />
                                    <span className="text-red-600">
                                        {errors.title}
                                    </span>
                                </div>
                                <div className="mb-4">
                                    <label className="">Description</label>
                                    <textarea
                                        type="text"
                                        className="w-full rounded"
                                        label="description"
                                        name="description"
                                        errors={errors.description}
                                        value={data.description}
                                        onChange={(e) =>
                                            setData("description", e.target.value)
                                        }
                                    />
                                    <span className="text-red-600">
                                        {errors.description}
                                    </span>
                                </div>
                            </div>
                            <div className="flex justify-between">
                                <button
                                    type="submit"
                                    className="px-4 py-2 text-white bg-green-500 rounded"
                                >
                                    Update
                                </button>
                                <button
                                    onClick={destroy}
                                    tabIndex="-1"
                                    type="button"
                                    className="px-4 py-2 text-white bg-red-500 rounded"
                                >
                                    Delete
                                </button>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        );
    };

    export default Edit;

Laravel Inertia js CRUD with React v3



    npm run watch


:end: 

#

[Top](#top)
<a name="larvel-breeze-vue"></a>

Steps for Laravel 9 Vue JS CRUD App using Vite Example:

    Step 1: Installing fresh new Laravel 9 Application
    Step 2: Creating Database and Configuration
    Step 3: Creating Auth with Breeze
    Step 4: Creating Migration and Model
    Step 5: Creating Route
    Step 6: Creating Controller
    Step 7: Creating Vue Pages
    Step 8: Testing
    Step 9: Conclusion


Step 1: Installing fresh new Laravel 9 Application 


    composer create-project laravel/laravel vuejs-crud-vite
    cd vuejs-crud-vite



Step 2: Creating Database and Configuration 

Create Database & Table 

.env


    DB_CONNECTION=mysql
    DB_HOST=127.0.0.1
    DB_PORT=3306
    DB_DATABASE=vuejs-crud-vite
    DB_USERNAME=root
    DB_PASSWORD=


Step 3: Creating Auth with Breeze 

    composer require laravel/breeze --dev
    php artisan breeze:install vue
    npm install
    npm run dev


    php artisan migrate


Step 4: Creating Migration and Model 

    php artisan make:migration create_posts_table



    <?php
    use Illuminate\Database\Migrations\Migration;
    use Illuminate\Database\Schema\Blueprint;
    use Illuminate\Support\Facades\Schema;
    return new class extends Migration
    {
        /**
         * Run the migrations.
         *
         * @return void
         */
        public function up()
        {
            Schema::create('posts', function (Blueprint $table) {
                $table->id();
                $table->string('title');
                $table->text('body');
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
            Schema::dropIfExists('posts');
        }
    };



    php artisan migrate
    php artisan make:model Post

Post.php


    <?php
    namespace App\Models;
    use Illuminate\Database\Eloquent\Factories\HasFactory;
    use Illuminate\Database\Eloquent\Model;
    class Post extends Model
    {
        use HasFactory;
        /**
         * The attributes that are mass assignable.
         *
         * @var array
         */
        protected $fillable = [
            'title', 'body'
        ];
    }


Step 5: Creating Route

routes/web.php


    <?php
    use Illuminate\Foundation\Application;
    use Illuminate\Support\Facades\Route;
    use Inertia\Inertia;
    use App\Http\Controllers\PostController;
    /*
    |--------------------------------------------------------------------------
    | Web Routes
    |--------------------------------------------------------------------------
    |
    | Here is where you can register web routes for your application. These
    | routes are loaded by the RouteServiceProvider within a group which
    | contains the "web" middleware group. Now create something great!
    |
    */
    Route::get('/', function () {
        return Inertia::render('Welcome', [
            'canLogin' => Route::has('login'),
            'canRegister' => Route::has('register'),
            'laravelVersion' => Application::VERSION,
            'phpVersion' => PHP_VERSION,
        ]);
    });
    Route::get('/dashboard', function () {
        return Inertia::render('Dashboard');
    })->middleware(['auth', 'verified'])->name('dashboard');
    require __DIR__.'/auth.php';
    Route::resource('posts', PostController::class);



Step 6: Creating Controller

 Create a new file PostController.php in app/Http/Controllers folder



    <?php

    namespace App\Http\Controllers;

    use Illuminate\Http\Request;
    use Inertia\Inertia;
    use App\Models\Post;
    use Illuminate\Support\Facades\Validator;

    class PostController extends Controller
    {
        /**
         * Show the form for creating a new resource.
         *
         * @return Response
         */
        public function index()
        {
            $posts = Post::all();
            return Inertia::render('Posts/Index', ['posts' => $posts]);
        }

        /**
         * Write code on Method
         *
         * @return response()
         */
        public function create()
        {
            return Inertia::render('Posts/Create');
        }

        /**
         * Show the form for creating a new resource.
         *
         * @return Response
         */
        public function store(Request $request)
        {
            Validator::make($request->all(), [
                'title' => ['required'],
                'body' => ['required'],
            ])->validate();

            Post::create($request->all());

            return redirect()->route('posts.index');
        }

        /**
         * Write code on Method
         *
         * @return response()
         */
        public function edit(Post $post)
        {
            return Inertia::render('Posts/Edit', [
                'post' => $post
            ]);
        }

        /**
         * Show the form for creating a new resource.
         *
         * @return Response
         */
        public function update($id, Request $request)
        {
            Validator::make($request->all(), [
                'title' => ['required'],
                'body' => ['required'],
            ])->validate();

            Post::find($id)->update($request->all());
            return redirect()->route('posts.index');
        }

        /**
         * Show the form for creating a new resource.
         *
         * @return Response
         */
        public function destroy($id)
        {
            Post::find($id)->delete();
            return redirect()->route('posts.index');
        }
    }



Step 7: Creating Vue Pages

resources/js/Pages 
Index.vue, Edit.vue & Create.vue


resources/js/Pages/Posts/Index.vue

    <script setup>
    import BreezeAuthenticatedLayout from '@/Layouts/Authenticated.vue';
    import { Head, Link, useForm } from '@inertiajs/inertia-vue3';
    defineProps({
        posts: Array,
    });
    const form = useForm();
    function destroy(id) {
        if (confirm("Are you sure you want to Delete")) {
            form.delete(route('posts.destroy', id));
        }
    }
    </script>
    <template>
        <Head title="Dashboard" />
        <BreezeAuthenticatedLayout>
            <template #header>
                <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                    Laravel 9 Vue JS CRUD App using Vite Example - LaravelTuts.com
                </h2>
            </template>
            <div class="py-12">
                <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                    <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                        <div class="p-6 bg-white border-b border-gray-200">
                            <div className="flex items-center justify-between mb-6">
                                <Link
                                    className="px-6 py-2 text-white bg-green-500 rounded-md focus:outline-none"
                                    :href="route('posts.create')"
                                >
                                    Create Post
                                </Link>
                            </div>
                            <table className="table-fixed w-full">
                                <thead>
                                    <tr className="bg-gray-100">
                                        <th className="px-4 py-2 w-20">No.</th>
                                        <th className="px-4 py-2">Title</th>
                                        <th className="px-4 py-2">Body</th>
                                        <th className="px-4 py-2">Action</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr v-for="post in posts">
                                        <td className="border px-4 py-2">{{ post.id }}</td>
                                        <td className="border px-4 py-2">{{ post.title }}</td>
                                        <td className="border px-4 py-2">{{ post.body }}</td>
                                        <td className="border px-4 py-2">
                                            <Link
                                                tabIndex="1"
                                                className="px-4 py-2 text-sm text-white bg-blue-500 rounded"
                                                :href="route('posts.edit', post.id)"
                                            >
                                                Edit
                                            </Link>
                                            <button
                                                @click="destroy(post.id)"
                                                tabIndex="-1"
                                                type="button"
                                                className="mx-1 px-4 py-2 text-sm text-white bg-red-500 rounded"
                                            >
                                                Delete
                                            </button>
                                        </td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </div>
        </BreezeAuthenticatedLayout>
    </template>

resources/js/Pages/Posts/Create.vue

    <script setup>
    import BreezeAuthenticatedLayout from '@/Layouts/Authenticated.vue';
    import BreezeLabel from '@/Components/Label.vue';
    import BreezeInput from '@/Components/Input.vue';
    import BreezeTextArea from '@/Components/Textarea.vue';
    import { Head, Link, useForm } from '@inertiajs/inertia-vue3';
    const form = useForm({
        title: '',
        body: ''
    });
    const submit = () => {
        form.post(route('posts.store'));
    };
    </script>
    <template>
        <Head title="Dashboard" />
        <BreezeAuthenticatedLayout>
            <template #header>
                <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                    Create Post
                </h2>
            </template>
            <div class="py-12">
                <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                    <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                        <div class="p-6 bg-white border-b border-gray-200">
                            <div className="flex items-center justify-between mb-6">
                                <Link
                                    className="px-6 py-2 text-white bg-blue-500 rounded-md focus:outline-none"
                                    :href="route('posts.index')"
                                >
                                    Back
                                </Link>
                            </div>
                            <form name="createForm" @submit.prevent="submit">
                                    <div className="flex flex-col">
                                        <div className="mb-4">
                                            <BreezeLabel for="title" value="Title" />

                                            <BreezeInput 
                                                id="title" 
                                                type="text" 
                                                class="mt-1 block w-full" 
                                                v-model="form.title" 
                                                autofocus />
                                            <span className="text-red-600" v-if="form.errors.title">
                                                {{ form.errors.title }}
                                            </span>
                                        </div>
                                        <div className="mb-4">
                                            <BreezeLabel for="body" value="Body" />

                                            <BreezeTextArea 
                                                id="body" 
                                                class="mt-1 block w-full" 
                                                v-model="form.body" 
                                                autofocus />
                                            <span className="text-red-600" v-if="form.errors.body">
                                                {{ form.errors.body }}
                                            </span>
                                        </div>
                                    </div>

                                    <div className="mt-4">
                                        <button
                                            type="submit"
                                            className="px-6 py-2 font-bold text-white bg-green-500 rounded"
                                        >
                                            Save
                                        </button>
                                    </div>
                                </form>
                        </div>
                    </div>
                </div>
            </div>
        </BreezeAuthenticatedLayout>
    </template>

resources/js/Pages/Posts/Edit.vue

    <script setup>
    import BreezeAuthenticatedLayout from '@/Layouts/Authenticated.vue';
    import BreezeLabel from '@/Components/Label.vue';
    import BreezeInput from '@/Components/Input.vue';
    import BreezeTextArea from '@/Components/Textarea.vue';
    import { Head, Link, useForm } from '@inertiajs/inertia-vue3';
    const props = defineProps({
        post: Object,
    });
    const form = useForm({
        title: props.post.title,
        body: props.post.body
    });
    const submit = () => {
        form.put(route('posts.update', props.post.id));
    };
    </script>
    <template>
        <Head title="Dashboard" />
        <BreezeAuthenticatedLayout>
            <template #header>
                <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                    Edit Post
                </h2>
            </template>
            <div class="py-12">
                <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                    <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                        <div class="p-6 bg-white border-b border-gray-200">
                            <div className="flex items-center justify-between mb-6">
                                <Link
                                    className="px-6 py-2 text-white bg-blue-500 rounded-md focus:outline-none"
                                    :href="route('posts.index')"
                                >
                                    Back
                                </Link>
                            </div>
                            <form name="createForm" @submit.prevent="submit">
                                    <div className="flex flex-col">
                                        <div className="mb-4">
                                            <BreezeLabel for="title" value="Title" />

                                            <BreezeInput 
                                                id="title" 
                                                type="text" 
                                                class="mt-1 block w-full" 
                                                v-model="form.title" 
                                                autofocus />
                                            <span className="text-red-600" v-if="form.errors.title">
                                                {{ form.errors.title }}
                                            </span>
                                        </div>
                                        <div className="mb-4">
                                            <BreezeLabel for="body" value="Body" />

                                            <BreezeTextArea 
                                                id="body" 
                                                class="mt-1 block w-full" 
                                                v-model="form.body" 
                                                autofocus />
                                            <span className="text-red-600" v-if="form.errors.body">
                                                {{ form.errors.body }}
                                            </span>
                                        </div>
                                    </div>

                                    <div className="mt-4">
                                        <button
                                            type="submit"
                                            className="px-6 py-2 font-bold text-white bg-green-500 rounded"
                                        >
                                            Save
                                        </button>
                                    </div>
                                </form>
                        </div>
                    </div>
                </div>
            </div>
        </BreezeAuthenticatedLayout>
    </template>

Create a new file Textaarea.vue inside resources/js/Components

resources/js/Components/Textarea.vue

    <script setup>
        import { onMounted, ref } from 'vue';
        defineProps(['modelValue']);
        defineEmits(['update:modelValue']);
        const input = ref(null);
        onMounted(() => {
            if (input.value.hasAttribute('autofocus')) {
                input.value.focus();
            }
        });
    </script>
    <template>
        <textarea class="border-gray-300 focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm" :value="modelValue" @input="$emit('update:modelValue', $event.target.value)" ref="input"></textarea>
    </template>

Add a Post Navigation in Authenticated.vue inside resources/js/Layouts folder.

    <!-- Navigation Links -->
    <div class="hidden space-x-8 sm:-my-px sm:ml-10 sm:flex">
      <BreezeNavLink :href="route('dashboard')" :active="route().current('dashboard')">Dashboard</BreezeNavLink>
      <BreezeNavLink :href="route('posts.index')" :active="route().current('posts.index')">Posts</BreezeNavLink>
    </div>




Step 8: Testing

Now let’s test our Laravel 9 Vue JS CRUD App using Vite Example. Run the following command to start laravel server.

    php artisan serve

    npm run dev
    npm run build

http://127.0.0.1:8000/


:end:



[Top](#top)
<a name="larvel10-crud"></a>

#Laravel 10 Crud Example


Step 1: Install Laravel 10 App

Let us begin the tutorial by installing a new laravel 10 application. if you have already created the project, then skip the following step.

    composer create-project laravel/laravel example-app

Step 2: Database Configuration

In the second step, we will make a database configuration, we need to add the database name, MySQL username, and password. So let's open the .env file and fill in all details like as below:

.env

  DB_CONNECTION=mysql

  DB_HOST=127.0.0.1

  DB_PORT=3306

  DB_DATABASE=here your database name(blog)

  DB_USERNAME=here database username(root)

  DB_PASSWORD=here database password(root)



    Step 3: Create Migration


<code>
<?php

  

use Illuminate\Database\Migrations\Migration;

use Illuminate\Database\Schema\Blueprint;

use Illuminate\Support\Facades\Schema;

  

return new class extends Migration

{

    /**

     * Run the migrations.

     *

     * @return void

     */

    public function up()

    {

        Schema::create('products', function (Blueprint $table) {

            $table->id();

            $table->string('name');

            $table->text('detail');

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

        Schema::dropIfExists('products');

    }

};


</code>

Now you have to run this migration by the following command:

    php artisan migrate
    php artisan make:migration create_products_table --create=products


After this command you will find one file in the following path "database/migrations" and you have to put below code in your migration file for creating the products table.


Now you have to run this migration by the following command:

    php artisan migrate



Step 4: Create Controller and Model

In this step, now we should create new resource controller as ProductController. So run bellow command and create new controller. bellow controller for create resource controller.

    php artisan make:controller ProductController --resource --model=Product


In this controller will create seven methods by default as bellow methods:

 1)index()

 2)create()

 3)store()

 4)show()

 5)edit()

6)update()

7)destroy()


So, let's copy bellow code and put on ProductController.php file.

app/Http/Controllers/ProductController.php

<code>
<?php

  

namespace App\Http\Controllers;

  

use App\Models\Product;

use Illuminate\Http\RedirectResponse;

use Illuminate\Http\Request;

use Illuminate\Http\Response;

use Illuminate\View\View;

  

class ProductController extends Controller

{

    /**

     * Display a listing of the resource.

     */

    public function index(): View

    {

        $products = Product::latest()->paginate(5);

        

        return view('products.index',compact('products'))

                    ->with('i', (request()->input('page', 1) - 1) * 5);

    }

  

    /**

     * Show the form for creating a new resource.

     */

    public function create(): View

    {

        return view('products.create');

    }

  

    /**

     * Store a newly created resource in storage.

     */

    public function store(Request $request): RedirectResponse

    {

        $request->validate([

            'name' => 'required',

            'detail' => 'required',

        ]);

        

        Product::create($request->all());

         

        return redirect()->route('products.index')

                        ->with('success','Product created successfully.');

    }

  

    /**

     * Display the specified resource.

     */

    public function show(Product $product): View

    {

        return view('products.show',compact('product'));

    }

  

    /**

     * Show the form for editing the specified resource.

     */

    public function edit(Product $product): View

    {

        return view('products.edit',compact('product'));

    }

  

    /**

     * Update the specified resource in storage.

     */

    public function update(Request $request, Product $product): RedirectResponse

    {

        $request->validate([

            'name' => 'required',

            'detail' => 'required',

        ]);

        

        $product->update($request->all());

        

        return redirect()->route('products.index')

                        ->with('success','Product updated successfully');

    }

  

    /**

     * Remove the specified resource from storage.

     */

    public function destroy(Product $product): RedirectResponse

    {

        $product->delete();

         

        return redirect()->route('products.index')

                        ->with('success','Product deleted successfully');

    }

}
</code>

Step 5: Add Resource Route

Here, we need to add resource route for product crud application. so open your "routes/web.php" file and add following route.

    routes/web.php


<code>
<?php

  

use Illuminate\Support\Facades\Route;

  

use App\Http\Controllers\ProductController;

  

/*

|--------------------------------------------------------------------------

| Web Routes

|--------------------------------------------------------------------------

|

| Here is where you can register web routes for your application. These

| routes are loaded by the RouteServiceProvider within a group that

| contains the "web" middleware group. Now create something great!

|

*/

  

Route::resource('products', ProductController::class);
<code>


Step 6: Add Blade Files

In last step. In this step we have to create just blade files. So mainly we have to create layout file and then create new folder "products" then create blade files of crud app. So finally you have to create following bellow blade file:

1) layout.blade.php

2) index.blade.php

3) create.blade.php

4) edit.blade.php

5) show.blade.php

So let's just create following file and put bellow code.

resources/views/products/layout.blade.php


<code>
<!DOCTYPE html>

<html>

<head>

    <title>Laravel 10 CRUD Application - ItSolutionStuff.com</title>

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet">

</head>

<body>

    

<div class="container">

    @yield('content')

</div>

    

</body>

</html>

</code>

resources/views/products/index.blade.php

<code>
@extends('products.layout')

 

@section('content')

    <div class="row">

        <div class="col-lg-12 margin-tb">

            <div class="pull-left">

                <h2>Laravel 10 CRUD Example from scratch</h2>

            </div>

            <div class="pull-right">

                <a class="btn btn-success" href="{{ route('products.create') }}"> Create New Product</a>

            </div>

        </div>

    </div>

   

    @if ($message = Session::get('success'))

        <div class="alert alert-success">

            <p>{{ $message }}</p>

        </div>

    @endif

   

    <table class="table table-bordered">

        <tr>

            <th>No</th>

            <th>Name</th>

            <th>Details</th>

            <th width="280px">Action</th>

        </tr>

        @foreach ($products as $product)

        <tr>

            <td>{{ ++$i }}</td>

            <td>{{ $product->name }}</td>

            <td>{{ $product->detail }}</td>

            <td>

                <form action="{{ route('products.destroy',$product->id) }}" method="POST">

   

                    <a class="btn btn-info" href="{{ route('products.show',$product->id) }}">Show</a>

    

                    <a class="btn btn-primary" href="{{ route('products.edit',$product->id) }}">Edit</a>

   

                    @csrf

                    @method('DELETE')

      

                    <button type="submit" class="btn btn-danger">Delete</button>

                </form>

            </td>

        </tr>

        @endforeach

    </table>

  

    {!! $products->links() !!}

      

@endsection
</code>


<code>
resources/views/products/create.blade.php

@extends('products.layout')

  

@section('content')

<div class="row">

    <div class="col-lg-12 margin-tb">

        <div class="pull-left">

            <h2>Add New Product</h2>

        </div>

        <div class="pull-right">

            <a class="btn btn-primary" href="{{ route('products.index') }}"> Back</a>

        </div>

    </div>

</div>

   

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

   

<form action="{{ route('products.store') }}" method="POST">

    @csrf

  

     <div class="row">

        <div class="col-xs-12 col-sm-12 col-md-12">

            <div class="form-group">

                <strong>Name:</strong>

                <input type="text" name="name" class="form-control" placeholder="Name">

            </div>

        </div>

        <div class="col-xs-12 col-sm-12 col-md-12">

            <div class="form-group">

                <strong>Detail:</strong>

                <textarea class="form-control" style="height:150px" name="detail" placeholder="Detail"></textarea>

            </div>

        </div>

        <div class="col-xs-12 col-sm-12 col-md-12 text-center">

                <button type="submit" class="btn btn-primary">Submit</button>

        </div>

    </div>

   

</form>

@endsection

</code>



resources/views/products/edit.blade.php


<code>
@extends('products.layout')

   

@section('content')

    <div class="row">

        <div class="col-lg-12 margin-tb">

            <div class="pull-left">

                <h2>Edit Product</h2>

            </div>

            <div class="pull-right">

                <a class="btn btn-primary" href="{{ route('products.index') }}"> Back</a>

            </div>

        </div>

    </div>

   

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

  

    <form action="{{ route('products.update',$product->id) }}" method="POST">

        @csrf

        @method('PUT')

   

         <div class="row">

            <div class="col-xs-12 col-sm-12 col-md-12">

                <div class="form-group">

                    <strong>Name:</strong>

                    <input type="text" name="name" value="{{ $product->name }}" class="form-control" placeholder="Name">

                </div>

            </div>

            <div class="col-xs-12 col-sm-12 col-md-12">

                <div class="form-group">

                    <strong>Detail:</strong>

                    <textarea class="form-control" style="height:150px" name="detail" placeholder="Detail">{{ $product->detail }}</textarea>

                </div>

            </div>

            <div class="col-xs-12 col-sm-12 col-md-12 text-center">

              <button type="submit" class="btn btn-primary">Submit</button>

            </div>

        </div>

   

    </form>

@endsection
</code>


resources/views/products/show.blade.php



<code>
@extends('products.layout')

  

@section('content')

    <div class="row">

        <div class="col-lg-12 margin-tb">

            <div class="pull-left">

                <h2> Show Product</h2>

            </div>

            <div class="pull-right">

                <a class="btn btn-primary" href="{{ route('products.index') }}"> Back</a>

            </div>

        </div>

    </div>

   

    <div class="row">

        <div class="col-xs-12 col-sm-12 col-md-12">

            <div class="form-group">

                <strong>Name:</strong>

                {{ $product->name }}

            </div>

        </div>

        <div class="col-xs-12 col-sm-12 col-md-12">

            <div class="form-group">

                <strong>Details:</strong>

                {{ $product->detail }}

            </div>

        </div>

    </div>

@endsection
</code>





All the required steps have been done, now you have to type the given below command and hit enter to run the Laravel app:

    php artisan serve


Now, Go to your web browser, type the given URL and view the app output:

Read Also: Laravel 10 REST API with Passport Authentication Tutorial


    http://localhost:8000/products


:end: 

#

[Top](#top)
<a name="laravel10-autosearch"></a>
#Laravel 10 Select2 Ajax Autocomplete Search Example


Step 1: Install Laravel 10

    composer create-project laravel/laravel example-app


Step 2: Add Dummy Users

First, we need to run default migrations, so we have created new users table. so let's run migration command:

    php artisan migrate

next, we will create some dummy users using tinker factory. so let's create dummy records using bellow command:

    php artisan tinker 
    User::factory()->count(20)->create()


Step 3: Create Controller


app/Http/Controllers/SearchController.php



<code>
<?php

    

namespace App\Http\Controllers;

   

use Illuminate\Http\Request;

use App\Models\User;

use Illuminate\View\View;

use Illuminate\Http\JsonResponse;

    

class SearchController extends Controller

{

    /**

     * Display a listing of the resource.

     *

     * @return \Illuminate\Http\Response

     */

    public function index(): View

    {

        return view('searchDemo');

    }

      

    /**

     * Show the form for creating a new resource.

     *

     * @return \Illuminate\Http\Response

     */

    public function autocomplete(Request $request): JsonResponse

    {

        $data = [];

    

        if($request->filled('q')){

            $data = User::select("name", "id")

                        ->where('name', 'LIKE', '%'. $request->get('q'). '%')

                        ->get();

        }

     

        return response()->json($data);

    }

}
</code>


Step 4: Create Routes

routes/web.php

<code>
<?php

  

use Illuminate\Support\Facades\Route;

  

use App\Http\Controllers\SearchController;

  

/* 

|--------------------------------------------------------------------------

| Web Routes

|--------------------------------------------------------------------------

|

| Here is where you can register web routes for your application. These

| routes are loaded by the RouteServiceProvider within a group which

| contains the "web" middleware group. Now create something great!

|

*/

  

Route::controller(SearchController::class)->group(function(){

    Route::get('demo-search', 'index');

    Route::get('autocomplete', 'autocomplete')->name('autocomplete');

});
</code>


Step 5: Create View File

<code>
resources/views/searchDemo.blade.php

<!DOCTYPE html>

<html>

<head>

    <title>Laravel 10 Select2 JS Autocomplete Search Example - ItSolutionStuff.com</title>

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet">

    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/select2/4.0.13/css/select2.min.css"/>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/select2/4.0.13/js/select2.min.js"></script>

</head>

<body>

     

<div class="container">

    <h1>Laravel 10 Select2 JS Autocomplete Search Example - ItSolutionStuff.com</h1>   

    <select class="form-control" id="search" style="width:500px;" name="user_id"></select>

</div>

     

<script type="text/javascript">

    var path = "{{ route('autocomplete') }}";

  

    $('#search').select2({

        placeholder: 'Select an user',

        ajax: {

          url: path,

          dataType: 'json',

          delay: 250,

          processResults: function (data) {

            return {

              results:  $.map(data, function (item) {

                    return {

                        text: item.name,

                        id: item.id

                    }

                })

            };

          },

          cache: true

        }

      });

  

</script>

     

</body>

</html>
</code>


   php artisan serve
  


http://localhost:8000/demo-search
     


:end:

#



#
[Top](#top)
