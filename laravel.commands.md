$$\colorbox{pink}{\large{\color{red}{Laravel \ Framework \ Commands}}}$$

<img src="https://laravel.com/img/logomark.min.svg" alt="Loading image....." width="10%">

:link:[Home](all-file-links.md)     


<a name="top"></a>
Topic: 
#
 [Laravel Installation CMDS](#laravel-installation-cmds) 
 
 [Installing Inertia - React in Laravel Project](#laravel-intertial-react) 
 
 [Laravel 9 CRUD Example Tutorial for Beginners](#laravel9-crud) 
 
  
  
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

