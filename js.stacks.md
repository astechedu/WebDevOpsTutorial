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



















[Go To Top](#top)
# Mern Stack 






[Go To Top](#top)
# Mern Stack 










:end:







