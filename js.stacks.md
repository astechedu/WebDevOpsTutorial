# Js Stacks Installations

<a name="top"></a>
Topics
 [MERN STACK Installation](#mern_stack)
 [MEVN Stack Installation](#mevn_stack)
 [MEAN Stack Installation](#mean_stack)








[Go To Top](#top)
# Mern Stack 

Setting Up the Project:

    mkdir mern
    cd mern
    npx create-react-app client
    mkdir server

    cd server
    npm init -y

    npm install mongodb express cors dotenv



The command above uses a couple of keywords:

    mongodb command installs MongoDB database driver that allows your Node.js applications to connect to the database and work with data.
    express installs the web framework for Node.js. (It will make our life easier.)
    cors installs a Node.js package that allows cross origin resource sharing.
    dotenv installs the module that loads environment variables from a .env file into process.env file. This lets you separate configuration files from the code.



mern/server/server.js

    const express = require("express");
    const app = express();
    const cors = require("cors");
    require("dotenv").config({ path: "./config.env" });
    const port = process.env.PORT || 5000;
    app.use(cors());
    app.use(express.json());
    app.use(require("./routes/record"));
    // get driver connection
    const dbo = require("./db/conn");

    app.listen(port, () => {
      // perform a database connection when server starts
      dbo.connectToServer(function (err) {
        if (err) console.error(err);

      });
      console.log(`Server is running on port: ${port}`);
    });
    mern/server/server.js

    const express = require("express");
    const app = express();
    const cors = require("cors");
    require("dotenv").config({ path: "./config.env" });
    const port = process.env.PORT || 5000;
    app.use(cors());
    app.use(express.json());
    app.use(require("./routes/record"));
    // get driver connection
    const dbo = require("./db/conn");

    app.listen(port, () => {
      // perform a database connection when server starts
      dbo.connectToServer(function (err) {
        if (err) console.error(err);

      });
      console.log(`Server is running on port: ${port}`);
    });




Connecting to MongoDB Atlas:


ATLAS_URI=mongodb+srv://<username>:<password>@sandbox.jadwj.mongodb.net/employees?retryWrites=true&w=majority
PORT=5000
 
 
 
 mern/server/db/conn.js

    const { MongoClient } = require("mongodb");
    const Db = process.env.ATLAS_URI;
    const client = new MongoClient(Db, {
      useNewUrlParser: true,
      useUnifiedTopology: true,
    });

    var _db;

    module.exports = {
      connectToServer: function (callback) {
        client.connect(function (err, db) {
          // Verify we got a good "db" object
          if (db)
          {
            _db = db.db("employees");
            console.log("Successfully connected to MongoDB."); 
          }
          return callback(err);
             });
      },

      getDb: function () {
        return _db;
      },
    };




Server API Endpoints:
 

    cd ../server
    mkdir routes
    touch routes/record.js

 
 
 
 mern/server/routes/record.js

const express = require("express");
 
// recordRoutes is an instance of the express router.
// We use it to define our routes.
// The router will be added as a middleware and will take control of requests starting with path /record.
const recordRoutes = express.Router();
 
// This will help us connect to the database
const dbo = require("../db/conn");
 
// This help convert the id from string to ObjectId for the _id.
const ObjectId = require("mongodb").ObjectId;
 
 
// This section will help you get a list of all the records.
recordRoutes.route("/record").get(function (req, res) {
 let db_connect = dbo.getDb("employees");
 db_connect
   .collection("records")
   .find({})
   .toArray(function (err, result) {
     if (err) throw err;
     res.json(result);
   });
});
 
// This section will help you get a single record by id
recordRoutes.route("/record/:id").get(function (req, res) {
 let db_connect = dbo.getDb();
 let myquery = { _id: ObjectId(req.params.id) };
 db_connect
   .collection("records")
   .findOne(myquery, function (err, result) {
     if (err) throw err;
     res.json(result);
   });
});
 
// This section will help you create a new record.
recordRoutes.route("/record/add").post(function (req, response) {
 let db_connect = dbo.getDb();
 let myobj = {
   name: req.body.name,
   position: req.body.position,
   level: req.body.level,
 };
 db_connect.collection("records").insertOne(myobj, function (err, res) {
   if (err) throw err;
   response.json(res);
 });
});
 
// This section will help you update a record by id.
recordRoutes.route("/update/:id").post(function (req, response) {
 let db_connect = dbo.getDb();
 let myquery = { _id: ObjectId(req.params.id) };
 let newvalues = {
   $set: {
     name: req.body.name,
     position: req.body.position,
     level: req.body.level,
   },
 };
 db_connect
   .collection("records")
   .updateOne(myquery, newvalues, function (err, res) {
     if (err) throw err;
     console.log("1 document updated");
     response.json(res);
   });
});
 
// This section will help you delete a record
recordRoutes.route("/:id").delete((req, response) => {
 let db_connect = dbo.getDb();
 let myquery = { _id: ObjectId(req.params.id) };
 db_connect.collection("records").deleteOne(myquery, function (err, obj) {
   if (err) throw err;
   console.log("1 document deleted");
   response.json(obj);
 });
});
 
module.exports = recordRoutes;
 
 
 
 
 
 
 
 
 
 

 
 
























[Go To Top](#top)
# Mern Stack 






[Go To Top](#top)
# Mern Stack 










:end:







