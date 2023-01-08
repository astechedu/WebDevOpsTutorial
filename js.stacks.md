# Js Stacks Installations

<a name="top"></a>
Topics
 [MERN STACK Installation](#mern_stack)
 
 [MEVN Stack Installation](#mevn_stack)
 
 [MEAN Stack Installation](#mean_stack)












[Go To Top](#top)
<a name="mern_stack"></a>
# Mern Stack 

Setting Up the Project:

How To Get Started with the MERN Stack

   JavaScript
   React
   MongoDB
   Node.js



Let’s start with the setup. Open your terminal and create a new file directory in any convenient location on your local machine. You can name it anything but in this example, it is called mern-todo.

    mkdir mern-todo
    cd mern-todo
    npm init
    npm init -y
    npm install express
    

Now, create a file index.js and type the following code into it and save:

index.js

     const express = require('express');

     const app = express();

     const port = process.env.PORT || 5000;

     app.use((req, res, next) => {
       res.header('Access-Control-Allow-Origin', '*');
       res.header('Access-Control-Allow-Headers', 'Origin, X-Requested-With, Content-Type, Accept');
       next();
     });

     app.use((req, res, next) => {
       res.send('Welcome to Express');
     });

     app.listen(port, () => {
       console.log(`Server running on port ${port}`);
     });
     
     

     This snippet from the preceeding code helps handle CORS related issues that you might face when trying to access the API from different domains during development and testing:

     app.use((req, res, next) => {
       res.header('Access-Control-Allow-Origin', '*');
       res.header('Access-Control-Allow-Headers', 'Origin, X-Requested-With, Content-Type, Accept');
       next();
     });


    node index.js


Creating the Routes:

    create a task
    view all tasks
    delete a completed task


     mkdir routes


     Edit api.js and paste the following code in it:
     routes/api.js

     const express = require('express');
     const router = express.Router();

     router.get('/todos', (req, res, next) => {
       // get placeholder
     });

     router.post('/todos', (req, res, next) => {
       // post placeholder
     });

     router.delete('/todos/:id', (req, res, next) => {
       // delete placeholder
     });

     module.exports = router;
     



 Defining the Models:


To create a schema and a model, install Mongoose which is a Node package that makes working with MongoDB easier.

    # ensure that you are in the `mern-todo` project directory
    
    npm install mongoose

    mkdir models

Paste the following into todo.js with your text editor:


models/todo.js

     const mongoose = require('mongoose');
     const Schema = mongoose.Schema;

     // Create schema for todo
     const TodoSchema = new Schema({
       action: {
         type: String,
         required: [true, 'The todo text field is required'],
       },
     });

     // Create model for todo
     const Todo = mongoose.model('todo', TodoSchema);

     module.exports = Todo;

     Now, we need to update our routes to make use of the new model.
     routes/api.js

     const express = require('express');
     const router = express.Router();
     const Todo = require('../models/todo');

     router.get('/todos', (req, res, next) => {
       // This will return all the data, exposing only the id and action field to the client
       Todo.find({}, 'action')
         .then((data) => res.json(data))
         .catch(next);
     });

     router.post('/todos', (req, res, next) => {
       if (req.body.action) {
         Todo.create(req.body)
           .then((data) => res.json(data))
           .catch(next);
       } else {
         res.json({
           error: 'The input field is empty',
         });
       }
     });

     router.delete('/todos/:id', (req, res, next) => {
       Todo.findOneAndDelete({ _id: req.params.id })
         .then((data) => res.json(data))
         .catch(next);
     });

     module.exports = router;




 Connecting to a Database:

After setting up your database you need to update index.js file with the following code:

index.js


     const express = require('express');
     const bodyParser = require('body-parser');
     const mongoose = require('mongoose');
     const routes = require('./routes/api');
     require('dotenv').config();

     const app = express();

     const port = process.env.PORT || 5000;

     // Connect to the database
     mongoose
       .connect(process.env.DB, { useNewUrlParser: true })
       .then(() => console.log(`Database connected successfully`))
       .catch((err) => console.log(err));

     // Since mongoose's Promise is deprecated, we override it with Node's Promise
     mongoose.Promise = global.Promise;

     app.use((req, res, next) => {
       res.header('Access-Control-Allow-Origin', '*');
       res.header('Access-Control-Allow-Headers', 'Origin, X-Requested-With, Content-Type, Accept');
       next();
     });

     app.use(bodyParser.json());

     app.use('/api', routes);

     app.use((err, req, res, next) => {
       console.log(err);
       next();
     });

     app.listen(port, () => {
       console.log(`Server running on port ${port}`);
     });
     
     


    npm install body-parser

In the preceeding code made use of process.env to access environment variables, which need to be created. Create a file in your root directory with the name .env and edit:
.env

     DB = 'mongodb://<USER>:<PASSWORD>@example.mlab.com:port/todo'

    # ensure that you are in the `mern-todo` project directory
    npm install dotenv

     require('dotenv').config()
 
 
 Step 6 — Testing the API



    node index.js

Now, open your client, create a GET method and navigate to http://localhost:5000/api/todos.



A screenshot of the Insomnia REST client testing endpoints


Sample POST request:

POST localhost:5000/api/todos
Body
raw

Sample POST value:

     {
       "action": "build a mern stack application"
     }

Sample GET request:

     GET localhost:5000/api/todos

Sample GET response:

  Output
 
     [
       {
         "id": "5bd4edfc89d4c3228e1bbe0a",
         "action": "build a mern stack application"
       }
     ]

Sample DELETE request:

DELETE localhost:5000/api/todos/5bd4edfc89d4c3228e1bbe0ad

Test and observe the results of GET, POST, and DELETE.
 
 
 
Creating the Frontend:

In the same root directory as your backend code, which is the mern-todo directory, run:

    npx create-react-app client

 
  Running the React App:

Before testing the React app, there are many dependencies that need to be installed in the project root directory.
First, install concurrently as a dev dependency:

      npm install concurrently --save-dev

Then, install nodemon as a dev dependency:

      npm install nodemon --save-dev

Nodemon is used to run the server and monitor it as well. If there is any change in the server code, Nodemon will restart it automatically with the new changes.

Next, open your package.json file in the root folder of the app project, and paste the following code:


     package.json

          {
            // ...
            "scripts": {
              "start": "node index.js",
              "start-watch": "nodemon index.js",
              "dev": "concurrently \"npm run start-watch\" \"cd client && npm start\""
            },
            // ...
          }

Enter into the client folder, then locate the package.json file and add the following key-value pair inside it.

 
  client/package.json

         {
           // ...
           "proxy": "http://localhost:5000"
         }


This proxy setup in our package.json file will enable you to make API calls without having to type the full URL, just /api/todos will get all your todos
Open your terminal and run npm run dev and make sure you are in the todo directory and not in the client directory.
Your app will be open and running on localhost:3000.
 
 
 
Creating the React Components:


Open Input.js file and paste the following:
 
 
 
client/src/components/Input.js

     import React, { Component } from 'react';
     import axios from 'axios';

     class Input extends Component {
       state = {
         action: '',
       };

       addTodo = () => {
         const task = { action: this.state.action };

         if (task.action && task.action.length > 0) {
           axios
             .post('/api/todos', task)
             .then((res) => {
               if (res.data) {
                 this.props.getTodos();
                 this.setState({ action: '' });
               }
             })
             .catch((err) => console.log(err));
         } else {
           console.log('input field required');
         }
       };

       handleChange = (e) => {
         this.setState({
           action: e.target.value,
         });
       };

       render() {
         let { action } = this.state;
         return (
           <div>
             <input type="text" onChange={this.handleChange} value={action} />
             <button onClick={this.addTodo}>add todo</button>
           </div>
         );
       }
     }

     export default Input;



    cd client

And run npm install axios:

    npm install axios

After that, open your ListTodo.js file and paste the following code:
 
 
client/src/components/ListTodo.js
 
import React from 'react';

     const ListTodo = ({ todos, deleteTodo }) => {
       return (
         <ul>
           {todos && todos.length > 0 ? (
             todos.map((todo) => {
               return (
                 <li key={todo._id} onClick={() => deleteTodo(todo._id)}>
                   {todo.action}
                 </li>
               );
             })
           ) : (
             <li>No todo(s) left</li>
           )}
         </ul>
       );
     };

     export default ListTodo;

Then, in your Todo.js file you write the following code:
 
 
client/src/components/Todo.js

     import React, { Component } from 'react';
     import axios from 'axios';
     import Input from './Input';
     import ListTodo from './ListTodo';

     class Todo extends Component {
       state = {
         todos: [],
       };

       componentDidMount() {
         this.getTodos();
       }

       getTodos = () => {
         axios
           .get('/api/todos')
           .then((res) => {
             if (res.data) {
               this.setState({
                 todos: res.data,
               });
             }
           })
           .catch((err) => console.log(err));
       };

       deleteTodo = (id) => {
         axios
           .delete(`/api/todos/${id}`)
           .then((res) => {
             if (res.data) {
               this.getTodos();
             }
           })
           .catch((err) => console.log(err));
       };

       render() {
         let { todos } = this.state;

         return (
           <div>
             <h1>My Todo(s)</h1>
             <Input getTodos={this.getTodos} />
             <ListTodo todos={todos} deleteTodo={this.deleteTodo} />
           </div>
         );
       }
     }

     export default Todo;

You will need to make a little adjustment to your React code. Delete the logo and adjust your App.js to look like this:

 client/src/App.js

     import React from 'react';
     import Todo from './components/Todo';
     import './App.css';

     const App = () => {
       return (
         <div className="App">
           <Todo />
         </div>
       );
     };

     export default App;

Then paste the following code into App.css:
 
 
client/src/App.css

     .App {
       text-align: center;
       font-size: calc(10px + 2vmin);
       width: 60%;
       margin-left: auto;
       margin-right: auto;
     }

     input {
       height: 40px;
       width: 50%;
       border: none;
       border-bottom: 2px #101113 solid;
       background: none;
       font-size: 1.5rem;
       color: #787a80;
     }

     input:focus {
       outline: none;
     }

     button {
       width: 25%;
       height: 45px;
       border: none;
       margin-left: 10px;
       font-size: 25px;
       background: #101113;
       border-radius: 5px;
       color: #787a80;
       cursor: pointer;
     }

     button:focus {
       outline: none;
     }

     ul {
       list-style: none;
       text-align: left;
       padding: 15px;
       background: #171a1f;
       border-radius: 5px;
     }

     li {
       padding: 15px;
       font-size: 1.5rem;
       margin-bottom: 15px;
       background: #282c34;
       border-radius: 5px;
       overflow-wrap: break-word;
       cursor: pointer;
     }

     @media only screen and (min-width: 300px) {
       .App {
         width: 80%;
       }

       input {
         width: 100%
       }

       button {
         width: 100%;
         margin-top: 15px;
         margin-left: 0;
       }
     }

     @media only screen and (min-width: 640px) {
       .App {
         width: 60%;
       }

       input {
         width: 50%;
       }

       button {
         width: 30%;
         margin-left: 10px;
         margin-top: 0;
       }
     }

Also in index.css add the following rules:
 
 
client/src/index.css

     body {
       margin: 0;
       padding: 0;
       font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Oxygen", "Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue", sans-serif;
       -webkit-font-smoothing: antialiased;
       -moz-osx-font-smoothing: grayscale;
       box-sizing: border-box;
       background-color: #282c34;
       color: #787a80;
     }

     code {
       font-family: source-code-pro, Menlo, Monaco, Consolas, "Courier New", monospace;
     }










2.
[Go To Top](#top)
# Mern Stack 

What is the MERN:

    MongoDB: A cross-platform document-oriented database program
    Express.js: A web application framework for Node.js
    React: JavaScript library for building user interfaces
    Node.js: An open source, cross-platform, JavaScript run-time environment that executes JavaScript code outside of a browser



Server setup with Express.js and Node.js:


npm package initialization:

      npm init

Installing the dependencies:

      npm i express mongoose body-parser config



Here’s what we get in the code above:

    body-parser: Allows us to get the data throughout the request
    express: Is our main framework
    mongoose: Is used to connect and interact with MongoDB
    config: 

npm i -D nodemon


Now, we’ll add nodemon as a dev dependency. If you don’t want to add this, you can skip it — it’s optional. Install it with $ npm i -D nodemon. To use nodemon, add "app": "nodemon app.js" to your scripts tag under the package.json file.


The app.js is the entry point for the application.


"start": "node app.js"


Open and check package.json file


Setting the entry point

Now, create a file named app.js for our entry point. You can create this from the project folder with the 
     
       touch app.js command 




/ app.js


        const express = require('express');

        const app = express();

        app.get('/', (req, res) => res.send('Hello world!'));

        const port = process.env.PORT || 8082;

        app.listen(port, () => console.log(`Server running on port ${port}`));




After that, run the $ node app command. You will see Server running on port 8082. You can also check it from the browser by opening the browser and entering http://localhost:8082.


// package.json

{
  "name": "mern_a_to_z",
  "version": "1.0.0",
  "description": "",
  "main": "app.js",
  "scripts": {
    "start": "node app.js",
    "app": "nodemon app.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/nurislam03/MERN_A_to_Z.git"
  },
  "author": "Nur Islam",
  "license": "MIT",
  "bugs": {
    "url": "https://github.com/nurislam03/MERN_A_to_Z/issues"
  },
  "homepage": "https://github.com/nurislam03/MERN_A_to_Z#readme",
  "dependencies": {
    "body-parser": "^1.19.0",
    "express": "^4.17.1",
    "mongoose": "^5.5.15",
    "validation": "0.0.1"
  },
  "devDependencies": {
    "nodemon": "^1.19.1"
  }
}




      npm install
      npm run app
      
      
      
  Database management with MongoDB:
  
  
  
  Adding the database to our project: 
  
  
  
  
  Add the following code:

// default.json

{
  "mongoURI":
    "mongodb+srv://mern123:<password>@mernatoz-9kdpd.mongodb.net/test?retryWrites=true&w=majority"
}
 /* Replace <password> with your database password */
// db.js

const mongoose = require('mongoose');
const config = require('config');
const db = config.get('mongoURI');

const connectDB = async () => {
  try {
    mongoose.set('strictQuery', true);
    await mongoose.connect(db, {
      useNewUrlParser: true,
    });

    console.log('MongoDB is Connected...');
  } catch (err) {
    console.error(err.message);
    process.exit(1);
  }
};

module.exports = connectDB;
 
 
 
// app.js

const express = require('express');
const connectDB = require('./config/db');

const app = express();

// Connect Database
connectDB();

app.get('/', (req, res) => res.send('Hello world!'));

const port = process.env.PORT || 8082;

app.listen(port, () => console.log(`Server running on port ${port}`));


 
 
 
 npm run app
 
 
 
 Building RESTful APIs with the MERN stack: 
 
 
 
 To get started, create a folder named routes. In it, create another folder named api, which will hold all our APIs. Inside the api folder, create a file named books.js. We will create some APIs here to show how it works in a moment.
 
 
 
 
 
 Now, update your books.js with the following code:

// routes/api/books.js

const express = require('express');
const router = express.Router();

// Load Book model
const Book = require('../../models/Book');

// @route GET api/books/test
// @description tests books route
// @access Public
router.get('/test', (req, res) => res.send('book route testing!'));

// @route GET api/books
// @description Get all books
// @access Public
router.get('/', (req, res) => {
  Book.find()
    .then(books => res.json(books))
    .catch(err => res.status(404).json({ nobooksfound: 'No Books found' }));
});

// @route GET api/books/:id
// @description Get single book by id
// @access Public
router.get('/:id', (req, res) => {
  Book.findById(req.params.id)
    .then(book => res.json(book))
    .catch(err => res.status(404).json({ nobookfound: 'No Book found' }));
});

// @route GET api/books
// @description add/save book
// @access Public
router.post('/', (req, res) => {
  Book.create(req.body)
    .then(book => res.json({ msg: 'Book added successfully' }))
    .catch(err => res.status(400).json({ error: 'Unable to add this book' }));
});

// @route GET api/books/:id
// @description Update book
// @access Public
router.put('/:id', (req, res) => {
  Book.findByIdAndUpdate(req.params.id, req.body)
    .then(book => res.json({ msg: 'Updated successfully' }))
    .catch(err =>
      res.status(400).json({ error: 'Unable to update the Database' })
    );
});

// @route GET api/books/:id
// @description Delete book by id
// @access Public
router.delete('/:id', (req, res) => {
  Book.findByIdAndRemove(req.params.id, req.body)
    .then(book => res.json({ mgs: 'Book entry deleted successfully' }))
    .catch(err => res.status(404).json({ error: 'No such a book' }));
});

module.exports = router;

 
 
 
 
 
 
Database model:
 
 
 
// models/Book.js

const mongoose = require('mongoose');

const BookSchema = new mongoose.Schema({
  title: {
    type: String,
    required: true
  },
  isbn: {
    type: String,
    required: true
  },
  author: {
    type: String,
    required: true
  },
  description: {
    type: String
  },
  published_date: {
    type: Date
  },
  publisher: {
    type: String
  },
  updated_date: {
    type: Date,
    default: Date.now
  }
});

module.exports = Book = mongoose.model('book', BookSchema);


 
 
 
 Authentication and authorization: 
 
 
 
 
 
 
 
 Building the frontend: 
 
 
 Setting up Create React App
 
       npx create-react-app my-app
 
 
 
 You can replace my-app with whatever you’d like to use as your project name. For example, my project name is mern_a_to_z_client, and my command is 
 
           npx create-react-app mern_a_to_z_client
 
           cd mern_a_to_z_client

           yarn start 
    or     npm start
 
 
 
  http://localhost:3000
 

 
 Adding Bootstrap and Font Awesome to your React appP: 
 
 
 Open the file called index.html, which is in the public folder mern_a_to_z_client/public/index.html, and replace everything with the following code:
 
 
 
 <!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="shortcut icon" href="%PUBLIC_URL%/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="theme-color" content="#000000" />
    <!--
      manifest.json provides metadata used when your web app is installed on a
      user's mobile device or desktop. See https://developers.google.com/web/fundamentals/web-app-manifest/
    -->
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
    <!--
      Notice the use of %PUBLIC_URL% in the tags above.
      It will be replaced with the URL of the `public` folder during the build.
      Only files inside the `public` folder can be referenced from the HTML.

      Unlike "/favicon.ico" or "favicon.ico", "%PUBLIC_URL%/favicon.ico" will
      work correctly both with client-side routing and a non-root public URL.
      Learn how to configure a non-root public URL by running `npm run build`.
    -->

    <!-- bootstrap css cdn -->
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">

    <!-- fontawesome cdn -->
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.2.0/css/all.css" integrity="sha384-hWVjflwFxL6sNzntih27bfxkr27PmbbK/iSvJ+a4+0owXq79v+lsFkW54bOGbiDQ" crossorigin="anonymous">

    <title>MERN A to Z</title>
  </head>
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
    <!--
      This HTML file is a template.
      If you open it directly in the browser, you will see an empty page.

      You can add webfonts, meta tags, or analytics to this file.
      The build step will place the bundled scripts into the <body> tag.

      To begin the development, run `npm start` or `yarn start`.
      To create a production bundle, use `npm run build` or `yarn build`.
    -->

    <!-- bootstrap JS cdn -->
    <script src="https://code.jquery.com/jquery-3.2.1.slim.min.js" integrity="sha384-KJ3o2DKtIkvYIK3UENzmM7KCkRr/rE9/Qpg6aAZGJwFDMVNA/GpGFF93hXpG5KkN" crossorigin="anonymous"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.12.9/umd/popper.min.js" integrity="sha384-ApNbgh9B+Y1QKtv3Rn7W3mgPxhU9K/ScQsAP7hUibX39j7fakFPskvXusvfa0b4Q" crossorigin="anonymous"></script>
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/js/bootstrap.min.js" integrity="sha384-JZR6Spejh4U02d8jOt6vLEHfe/JQGiRRSQQxSfFWpi1MquVdAyjUar5+76PVCmYl" crossorigin="anonymous"></script>

  </body>
</html>


 
 Our frontend will have the following features:

    Add, create, or save a new book
    Show all the books we have stored in the database
    Show a single book
    Update a book
    Delete a book

 
 

          npm install --save react-router-dom
          npm install --save axios

 
 
 
 The Package.json file
 
 
 
 // MERN_A_to_Z_Client - package.json

{
  "name": "mern_a_to_z_client",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "@testing-library/jest-dom": "^5.16.5",
    "@testing-library/react": "^13.4.0",
    "@testing-library/user-event": "^13.5.0",
    "axios": "^1.2.1",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-router-dom": "^6.4.5",
    "react-scripts": "5.0.1",
    "web-vitals": "^2.1.4"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
  "eslintConfig": {
    "extends": [
      "react-app",
      "react-app/jest"
    ]
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  }
}
 
 
 
 
 
 
Creating the component file

Inside the src folder (mern_a_to_z_client/src/), create another folder called components, and inside it, create five different files:

    CreateBook.js
    ShowBookList.js
    BookCard.js
    ShowBookDetails.js
    UpdateBookInfo.js

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 https://blog.logrocket.com/mern-stack-tutorial/
 
 
 
 
 
      





[Go To Top](#top)
# Mevn Stack 






[Go To Top](#top)
# Mean Stack 










:end:







