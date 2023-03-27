$$\colorbox{Cyan}{\large{\color{white}{Cakephp \ Framework}}}$$

<img src="#" alt="Docker Image Loading....." width="10%">

:link:[Home](all-file-links.md)     


<a name="top"></a>
Topic: 
#
 [Cakephp 4 All Commands](#cakephp-cmds) 
 
 [Cakephp 4 MVC](#cakephp4-mvc)
 
 [Cakephp 4 Form](#cakephp4-form)
 
#  


<a name="cakephp4-mvc"></a>
### Cakephp 4 MVC

Table: 

ArticlesTAble

 Model/Table
 
    <?php
    namespace App\Model\Table;

    use Cake\ORM\Table;

    class ArticlesTable extends Table
    {
        public function initialize(array $config): void
        {
            $this->setTable('articles');
        }
    }


Model:

Model/Entity:

    <?php
    namespace App\Model\Entity;

    use Cake\ORM\Entity;

    class Article extends Entity
    {
    }


Controller: 

    <?php
    // src/Controller/ArticlesController.php

    namespace App\Controller;
    use App\Controller\AppController;
    class ArticlesController extends AppController
    {

        public function initialize(): void
        {
            parent::initialize();

            $this->loadComponent('Paginator');
            $this->loadComponent('Flash'); // Include the FlashComponent
        }

        public function index()
        {
            //$this->loadComponent('Paginator');
            $articles = $this->Paginator->paginate($this->Articles->find());    
            $this->set(compact('articles'));

        }
    }


:end: 
#


[Top](#top)
<a name="cakephp4-form"></a>

## Cakephp 4 Form 

Form: 

    echo $this->Form->create($user);
    // The following generates a Text input
    echo $this->Form->control('username');
    // The following generates a Password input
    echo $this->Form->control('password');
    // Assuming 'approved' is a datetime or timestamp field the following
    //generates an input of type "datetime-local"
    echo $this->Form->control('approved');
    // The following generates a Textarea element
    echo $this->Form->control('quote');

    echo $this->Form->button('Add');
    echo $this->Form->end();


:end:




