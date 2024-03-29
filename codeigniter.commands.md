$$\colorbox{Cyan}{\large{\color{white}{Codeigniter \ Framework}}}$$

<img src="#" alt="Docker Image Loading....." width="10%">

:link:[Home](all-file-links.md)     



<a name="top"></a>
Topic: 
#
 [Codeigniter All Commands](#codeigniter-cmds) 
 
 [Codeigniter 4 CRUD with Bootstrap and MySQL Example](#ci-crud) 
 
 [Codeigniter 4 CSS & JS Links](#css-js-links)
 
 [Codeigniter 4 Calling Helper Classes](#helpers)
 
 [Codeigniter 4 Contact Form & Save Data Example](#ci4-form)
  
 [Codeigniter 4 Config User and Admin Modules Config](#ci4-modules-config) 


#
Codeignier 4 Basic Commands: 

Migrations: 


	php spark migrate
	For Unix:
	php spark migrate -g test -n Acme\\Blog

	For Windows:
	php spark migrate -g test -n Acme\Blog
	php spark migrate:rollback               // -g -b -f
	php spark migrate:refresh               // -g -n --all -f
	php spark migrate:status
	php spark make:migration <class> [options]    // --session  --table   --dbgroup  --namespace  --suffix



#
[Top](#top)
<a name="ci-crud"></a>

**Codeigniterm 4 Bootstrap CRUD Application Example (Not Tested)

    Step 1: Download or Install Codeigniter 4
    Step 2: Enable Codeigniter Errors
    Step 3: Set Up Database
    Step 4: Create New Model
    Step 5: Create CRUD Controller
    Step 6: Create Routes
    Step 7: Insert Data into Database
    Step 8: Show Data List & Delete
    Step 9: Edit and Update Data


	composer create-project codeigniter4/appstarter
	cd codeigniter-crud-example


Open app/Config/Boot/development.php file and set the display_errors to 1 instead of 0. Repeat the same process in app/Config/Boot/production.php file.



	ini_set('display_errors', '1');



DB Config: 

<code>
public $default = [
        'DSN'      => '',
        'hostname' => 'localhost',
        'username' => 'root',
        'password' => 'root',
        'database' => 'demo',
        'DBDriver' => 'MySQLi',
        'DBPrefix' => '',
        'pConnect' => false,
        'DBDebug'  => (ENVIRONMENT !== 'development'),
        'cacheOn'  => false,
        'cacheDir' => '',
        'charset'  => 'utf8',
        'DBCollat' => 'utf8_general_ci',
        'swapPre'  => '',
        'encrypt'  => false,
        'compress' => false,
        'strictOn' => false,
        'failover' => [],
        'port'     => 3306,
	];

</code>

	# MAMPP
	public $default = [
	  ...
	     'hostname' => '/Applications/MAMP/tmp/mysql/mysql.sock',
	  ...
	]
	# XAMPP
	public $default = [
	  ...
	     'hostname' => '/Applications/XAMPP/xamppfiles/var/mysql/mysql.sock',
	  ...
	]

Create New Model:

	<?php 
	namespace App\Models;
	use CodeIgniter\Model;
	class UserModel extends Model
	{
	    protected $table = 'users';
	    protected $primaryKey = 'id';

	    protected $allowedFields = ['name', 'email'];
	}


#
Create CRUD Controller:

app/Controllers/UserCrud.php


	<?php 
	namespace App\Controllers;
	use App\Models\UserModel;
	use CodeIgniter\Controller;
	class UserCrud extends Controller
	{
	    // show users list
	    public function index(){
		$userModel = new UserModel();
		$data['users'] = $userModel->orderBy('id', 'DESC')->findAll();
		return view('user_view', $data);
	    }
	    // add user form
	    public function create(){
		return view('add_user');
	    }

	    // insert data
	    public function store() {
		$userModel = new UserModel();
		$data = [
		    'name' => $this->request->getVar('name'),
		    'email'  => $this->request->getVar('email'),
		];
		$userModel->insert($data);
		return $this->response->redirect(site_url('/users-list'));
	    }
	    // show single user
	    public function singleUser($id = null){
		$userModel = new UserModel();
		$data['user_obj'] = $userModel->where('id', $id)->first();
		return view('edit_user', $data);
	    }
	    // update user data
	    public function update(){
		$userModel = new UserModel();
		$id = $this->request->getVar('id');
		$data = [
		    'name' => $this->request->getVar('name'),
		    'email'  => $this->request->getVar('email'),
		];
		$userModel->update($id, $data);
		return $this->response->redirect(site_url('/users-list'));
	    }

	    // delete user
	    public function delete($id = null){
		$userModel = new UserModel();
		$data['user'] = $userModel->where('id', $id)->delete($id);
		return $this->response->redirect(site_url('/users-list'));
	    }    
	}


Create Routes in Codeigniter:

<code>
 app/Config/Routes.php
<code>


	// CRUD RESTful Routes
	$routes->get('users-list', 'UserCrud::index');
	$routes->get('user-form', 'UserCrud::create');
	$routes->post('submit-form', 'UserCrud::store');
	$routes->get('edit-view/(:num)', 'UserCrud::singleUser/$1');
	$routes->post('update', 'UserCrud::update');
	$routes->get('delete/(:num)', 'UserCrud::delete/$1');



Codeigniter Insert Data in Database Example:


app/Views/add_user.php

	<!DOCTYPE html>
	<html>
	<head>
	  <title>Codeigniter 4 Add User With Validation Demo</title>
	  <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css">
	  <style>
	    .container {
	      max-width: 500px;
	    }
	    .error {
	      display: block;
	      padding-top: 5px;
	      font-size: 14px;
	      color: red;
	    }
	  </style>
	</head>
	<body>
	  <div class="container mt-5">
	    <form method="post" id="add_create" name="add_create" 
	    action="<?= site_url('/submit-form') ?>">
	      <div class="form-group">
		<label>Name</label>
		<input type="text" name="name" class="form-control">
	      </div>
	      <div class="form-group">
		<label>Email</label>
		<input type="text" name="email" class="form-control">
	      </div>
	      <div class="form-group">
		<button type="submit" class="btn btn-primary btn-block">Update Data</button>
	      </div>
	    </form>
	  </div>
	  <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"></script>
	  <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-validate/1.19.2/jquery.validate.js"></script>
	  <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-validate/1.19.2/additional-methods.min.js"></script>
	  <script>
	    if ($("#add_create").length > 0) {
	      $("#add_create").validate({
		rules: {
		  name: {
		    required: true,
		  },
		  email: {
		    required: true,
		    maxlength: 60,
		    email: true,
		  },
		},
		messages: {
		  name: {
		    required: "Name is required.",
		  },
		  email: {
		    required: "Email is required.",
		    email: "It does not seem to be a valid email.",
		    maxlength: "The email should be or equal to 60 chars.",
		  },
		},
	      })
	    }
	  </script>
	</body>
	</html>


//Show Data List & Delete

app/Views/user_view.php


	<!doctype html>
	<html lang="en">
	  <head>
	  <meta charset="utf-8">
	  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
	  <title>Codeigniter 4 CRUD App Example - positronx.io</title>
	  <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css">
	</head>
	<body>
	<div class="container mt-4">
	    <div class="d-flex justify-content-end">
		<a href="<?php echo site_url('/user-form') ?>" class="btn btn-success mb-2">Add User</a>
		</div>
	    <?php
	     if(isset($_SESSION['msg'])){
		echo $_SESSION['msg'];
	      }
	     ?>
	  <div class="mt-3">
	     <table class="table table-bordered" id="users-list">
	       <thead>
		  <tr>
		     <th>User Id</th>
		     <th>Name</th>
		     <th>Email</th>
		     <th>Action</th>
		  </tr>
	       </thead>
	       <tbody>
		  <?php if($users): ?>
		  <?php foreach($users as $user): ?>
		  <tr>
		     <td><?php echo $user['id']; ?></td>
		     <td><?php echo $user['name']; ?></td>
		     <td><?php echo $user['email']; ?></td>
		     <td>
		      <a href="<?php echo base_url('edit-view/'.$user['id']);?>" class="btn btn-primary btn-sm">Edit</a>
		      <a href="<?php echo base_url('delete/'.$user['id']);?>" class="btn btn-danger btn-sm">Delete</a>
		      </td>
		  </tr>
		 <?php endforeach; ?>
		 <?php endif; ?>
	       </tbody>
	     </table>
	  </div>
	</div>

	<script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"></script>
	<link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.10.21/css/jquery.dataTables.min.css">
	<script type="text/javascript" src="https://cdn.datatables.net/1.10.21/js/jquery.dataTables.min.js"></script>
	<script>
	    $(document).ready( function () {
	      $('#users-list').DataTable();
	  } );
	</script>
	</body>
	</html>



//Edit and Update Data

app/Views/edit_view.php


	<!DOCTYPE html>
	<html>
	<head>
	  <title>Codeigniter 4 CRUD - Edit User Demo</title>
	  <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css">
	  <style>
	    .container {
	      max-width: 500px;
	    }
	    .error {
	      display: block;
	      padding-top: 5px;
	      font-size: 14px;
	      color: red;
	    }
	  </style>
	</head>
	<body>
	  <div class="container mt-5">
	    <form method="post" id="update_user" name="update_user" 
	    action="<?= site_url('/update') ?>">
	      <input type="hidden" name="id" id="id" value="<?php echo $user_obj['id']; ?>">
	      <div class="form-group">
		<label>Name</label>
		<input type="text" name="name" class="form-control" value="<?php echo $user_obj['name']; ?>">
	      </div>
	      <div class="form-group">
		<label>Email</label>
		<input type="email" name="email" class="form-control" value="<?php echo $user_obj['email']; ?>">
	      </div>
	      <div class="form-group">
		<button type="submit" class="btn btn-danger btn-block">Save Data</button>
	      </div>
	    </form>
	  </div>
	  <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"></script>
	  <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-validate/1.19.2/jquery.validate.js"></script>
	  <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-validate/1.19.2/additional-methods.min.js"></script>
	  <script>
	    if ($("#update_user").length > 0) {
	      $("#update_user").validate({
		rules: {
		  name: {
		    required: true,
		  },
		  email: {
		    required: true,
		    maxlength: 60,
		    email: true,
		  },
		},
		messages: {
		  name: {
		    required: "Name is required.",
		  },
		  email: {
		    required: "Email is required.",
		    email: "It does not seem to be a valid email.",
		    maxlength: "The email should be or equal to 60 chars.",
		  },
		},
	      })
	    }
	  </script>
	</body>
	</html>



	php spark serve
	
	
http://localhost:8080/index.php/users-list

#
:end:

#
[Top](#top)
<a name="css-js-links"></a>

## Codeigniter 4 CSS & JS Files Paths

	public/assets/css/my.css
	public/assets/js/my.js

Links In View Files: 

	<link href="<?php echo base_url(); ?>/assets/css/my.css" rel="stylesheet">
	<script src="<?php echo base_url(); ?>/assets/js/my.js"type="text/javascript"></script>
	OR
	<link href="<?php echo base_url(); ?>assets/css/my.css" rel="stylesheet">
	<script src="<?php echo base_url(); ?>assets/js/my.js"type="text/javascript"></script>  


:end:


#
[Top](#top)
<a name="helpers"></a>
## Codeigniter 4 Calling Helper Classes: 

Location: 

	app/Helpers
        app/Helpers/my_helper.php

Loading in BaseController:


	class BaseController extends Controller{

	   protected $request;
	   protected $helpers = ['custom1_helper'];
	   public function initController(RequestInterface $request, ResponseInterface $response, LoggerInterface $logger)
	   {

	       parent::initController($request, $response, $logger);

	   }
	}


Loading in Controller:

	php spark make:controller PageController
	

   public function index(){
      
      helper('my_helper'); // Loading single helper
      helper(['custom1_helper','custom2_helper']);      //Or Multiple Helpers
   }



Loading in View:

	<body>
	   <?php 
	   // helper("custom1_helper"); // Single helper loading
	   helper(["custom1_helper","custom2_helper"]); // Multiple helper loading
	   ?>
	<body>


:end:
	
#
[Top](#top)
<a name="ci4-form"></a>
# Codeigniter 4 Form Validation, Contact Form & Save Data Example

Files: 
		
//1. FormController
//2. FormModel
//3. contact_form.php


FormController.php
		
	namespace App\Controllers;
	use App\Models\FormModel;
	use CodeIgniter\Controller;
	class FormController extends Controller
	{
	    public function index() {
		helper(['form']);
		$data = [];
		return view('contact_form');
	    }

	    public function store() {
		helper(['form']);
		$rules = [
		    'name' => 'required|min_length[3]',
		    'email' => 'required|valid_email',
		    'phone' => 'required|numeric|max_length[10]'
		];

		if($this->validate($rules)){
		    $formModel = new FormModel();
		    $data = [
			'name'  => $this->request->getVar('name'),
			'email'  => $this->request->getVar('email'),
			'phone'  => $this->request->getVar('phone'),
		    ];
		    $formModel->save($data);
		    return redirect()->to('/contact-form');
		}else{
		    $data['validation'] = $this->validator;
		    echo view('contact_form', $data);
		}        
	    }
	}


FormModel.php
		
	<?php 
	namespace App\Models;
	use CodeIgniter\Model;
	class FormModel extends Model
	{
	    protected $table = 'users';
	    protected $primaryKey = 'id';
	    protected $allowedFields = ['name', 'email', 'phone'];
	}


contact_form.php

	<!doctype html>
	<html lang="en">
	<head>
	  <meta charset="utf-8">
	  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
	  <title>Codeigniter 4 Form Validation Example - positronx.io</title>
	  <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css">
	  <style>
	    .container {
	      max-width: 550px;
	    }
	  </style>
	</head>
	<body>
	  <div class="container mt-5">
	    <h1>Register</h1>
	    <?php $validation = \Config\Services::validation(); ?>
	    <form action="<?php echo base_url(); ?>/FormController/store" method="post">

	      <div class="form-group">
		<label>Name</label>
		<input type="text" name="name" class="form-control">
		<!-- Error -->
		<?php if($validation->getError('name')) {?>
		    <div class='alert alert-danger mt-2'>
		      <?= $error = $validation->getError('name'); ?>
		    </div>
		<?php }?>
	      </div>

	      <div class="form-group">
		<label>Email</label>
		<input type="text" name="email" class="form-control">
		<!-- Error -->
		<?php if($validation->getError('email')) {?>
		    <div class='alert alert-danger mt-2'>
		      <?= $error = $validation->getError('email'); ?>
		    </div>
		<?php }?>
	      </div>

	      <div class="form-group">
		<label>Phone</label>
		<input type="text" name="phone" class="form-control">
		<!-- Error -->
		<?php if($validation->getError('phone')) {?>
		    <div class='alert alert-danger mt-2'>
		      <?= $error = $validation->getError('phone'); ?>
		    </div>
		<?php }?>
	      </div>

	      <div class="form-group">
		<button type="submit" class="btn btn-primary btn-block">Submit</button>
	      </div>

	    </form>

	  </div>
	</body>
	</html>
	
:end:

#

[Top](#top)
<a name="ci4-modules-config"></a>
# Codeigniter 4 Modules Configration: 

1. Modules in root dir

codeigniter4/
app/
modules/
   -> User
       -> Config -> routes.php
       -> Controllers -> User.php
       -> Models -> User.php
       -> Views  -> index.php

Config Module: 

app/config/Autoload.php

    public $psr4 = [
        APP_NAMESPACE => APPPATH, // For custom app namespace
        'Config'      => APPPATH . 'Config',
        'Modules'     => ROOTPATH . 'modules',
    ];


app/config/routes.php
      
// include Outer User module 
if (file_exists(ROOTPATH . 'modules/User/Config/Routes.php')){
  require ROOTPATH . 'modules/User/Config/Routes.php';
}

//Modules/User/Config/routes.php

<?php

namespace Modules\User\Config;

    $routes->group('/user', ['namespace' => 'Modules\User\Controllers'], function($routes)
    {
         $routes->get('/', 'User::index');
    });
?>

//Modules/User/Controllers

<?php 

namespace Modules\User\Controllers;

use App\Controllers\BaseController;

class User extends BaseController
{    
    public  function __construct()
    {    	
    	echo " Outer User Module"."<br>";
    }
 
    public function index(){          

        return view('index');
    }
}


//Modules/User/Models

    <?php
     
    namespace Modules\User\Models;
     
    use CodeIgniter\Model;
     
    class User extends Model
    {
        // Table
        protected $table = 'users';
    }

//Modules/User/Views

  <h1>This is outer User module</h1>
       
        //Calling User Module index function
        //In Controller or in any
        //$mUser = new User();
        //$mUser->index();
        //OR
        //User::index();

2. Modules in app dir

//Codeigniter4/app/config/routes.php   (All are same as given above)
//Onlly this is added to...

// include Admin module 
if (file_exists(ROOTPATH . 'modules/Admin/Config/Routes.php')){
  require ROOTPATH . 'modules/Admin/Config/Routes.php';
}

:end:
