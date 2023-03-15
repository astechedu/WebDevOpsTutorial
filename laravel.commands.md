$$\colorbox{Cyan}{\large{\color{white}{Laravel \ Framework}}}$$

<img src="https://laravel.com/img/logomark.min.svg" alt="Loading image....." width="10%">

:link:[Home](all-file-links.md)     


<a name="top"></a>
Topic: 
#
 [Laravel Installation CMDS](#laravel-installation-cmds) 
 
 [Installing Inertia - React in Laravel Project](#laravel-intertial-react) 
 
  
#  

[Top](#top)
<a name="laravel-intertial-react"></a>
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
