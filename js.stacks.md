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

Now, enter into that file directory:

    cd mern-todo

The next step is to initialize the project with a package.json file. This file will contain some information about your app and the dependencies that it needs to run.

You can use:

    npm init

And follow the instructions when prompted. Or you can use:

    npm init -y

To use the default values.


Step 2 — Setting Up the Node Server

To run your JavaScript code on the backend, you need to spin up a server that will compile your code.

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


It’s time to start your server to see if it works. Open your terminal in the same directory as your index.js file and type:

    node index.js

If everything goes well, you will see Server running on port 5000 in your terminal.


Step 3 — Creating the Routes

There are three things that the app needs to do:

    create a task
    view all tasks
    delete a completed task

For each task, you will need to create routes that will define multiple endpoints that the todo app will depend on. So let’s create a folder routes and create a file api.js with the following code in it.

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

This provides placeholder routes for GET, POST, and DELETE.



Step 4 — Defining the Models


To create a schema and a model, install Mongoose which is a Node package that makes working with MongoDB easier.

    # ensure that you are in the `mern-todo` project directory
    npm install mongoose

Create a new folder in your root directory and name it models. Inside it create a file and name it todo.js with the following code in it:

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




Step 5 — Connecting to a Database

You will need a database where you will store your data. For this, you will make use of mLab. Follow the documentation to get started with mLab.

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

Note: In versions prior to Express 4.16+ it was necessary to rely upon middleware like body-parser. However, it is now possible to use the built-in parser.

If you are using an older version of Express, use npm to install body-parser:

    npm install body-parser

In the preceeding code made use of process.env to access environment variables, which need to be created. Create a file in your root directory with the name .env and edit:
.env

     DB = 'mongodb://<USER>:<PASSWORD>@example.mlab.com:port/todo'

Make sure you use your own MongoDB URL from mLab after you created your database and user. Replace <USER> with the username and <PASSWORD> with the password of the user you created.

To work with environment variable you will have to install a Node package called dotenv that makes sure you have access to environment variable stored in the .env file.

    # ensure that you are in the `mern-todo` project directory
    npm install dotenv

Then require and configure it in index.js:

     require('dotenv').config()

Using environment variables instead of writing credentials to the application code directly can hide sensitive information from your versioning system. It is considered a best practice to separate configuration and secret data from application code in this manner.
\
 
 
 Step 6 — Testing the API

This is the part we start trying out things to make sure your RESTful API is working. Since your frontend is not ready yet, you can make use of some API development clients to test your code.

You can use Postman or Insomnia or your preferred client for testing APIs.

Start your server using the command:

    node index.js

Now, open your client, create a GET method and navigate to http://localhost:5000/api/todos.

A screenshot of the Insomnia REST client testing endpoints

Test all the API endpoints and make sure they are working. For the endpoints that require body, send JSON back with the necessary fields since it’s what you set up in your code.

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
 
 
 
Step 7 — Creating the Frontend


In the same root directory as your backend code, which is the mern-todo directory, run:

    npx create-react-app client

This will create a new folder in your mern-todo directory called client, where you will add all the React code.

 

 
 Step 8 — Running the React App

Before testing the React app, there are many dependencies that need to be installed in the project root directory.

First, install concurrently as a dev dependency:

      npm install concurrently --save-dev

Concurrently is used to run more than one command simultaneously from the same terminal window.

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
 
 
 
Step 9 — Creating the React Components


Inside your src folder create another folder called components and inside it create three files Input.js, ListTodo.js, and Todo.js.

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

 
To make use of axios, which is a Promise-based HTTP client for the browser and Node.js, you will need to navigate to your client directory from your terminal:

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

Assuming no errors when saving all these files, the todo app will be ready and fully functional with the functionality discussed earlier: creating a task, deleting a task, and viewing all your tasks.
Conclusion



















[Go To Top](#top)
# Mern Stack 






[Go To Top](#top)
# Mern Stack 










:end:







